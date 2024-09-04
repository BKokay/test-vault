---
created: 2024-08-15T13:44
updated: 2024-09-03T11:17
---
[[Notes from Georg]] | [[Fuel saver user stories]] [[Methods for use cases final]]

-   I want to see the time and date of a fuel stop
	-  FuelStopService.get(int id) -> this will already be implemented, do I want to *only* return the fuel_stop.stop_timestamp? 
-  I want to see the location of a gas station - show lat/lon 
```java
	public Point getLocation(int gasStationId) {
		String sql = "SELECT latitude, longitude FROM fuel_saver.gas_station WHERE id = ?";
		//prepare statement here/ try catch
		Point p = new Point();
		p.setLocation(rs.getDouble("longitude"), rs.getDouble("latitude"));
		return p	
	} 
```

-   I want to see the price per liter of a gas station
```java
public Map<LocalDateTime, double> getPricePerLiter(int gasStationId) {
	String sql = "SELECT fs.price_per_liter, fs.stop_timestamp FROM fuel_saver.fuel_stop fs JOIN fuel_saver.gas_station gs ON fs.station_id = gs.id WHERE gs.id = ?"
	Map<LocalDateTime, double> fuelStopsPrice = new Map<>();
	//prepare statement here/ try/catch
	LocalDateTime stopTimestamp = rs.getTimestamp("stop_timestamp").toLocalDate();
	double pricePerLiter = rs.getDouble("price_per_liter");
	fuelStopsPrice.put(stopTimestamp, pricePerLiter);
	return fuelStopsPrice;
}
```
-  I want to see the average price per liter of other gas stations along the route
	- this is complicated... do I check the lat/lon of a station in relation to the route?
```java

```
-  I want to see the number of liters filled at a gas station 
```sql
SELECT gs.id, SUM(fs.number_of_liters) AS total_liters
FROM fuel_saver.gas_station gs
JOIN fuel_saver.fuel_stop fs ON gs.id = fs.station_id
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = ?
GROUP BY gs.id;
```
```java
public Map<long, double> getTotalLitersFilled(int gasStationId){
	String sql = "" 
	Map<long, double> totalLitersFilled = new Map<>();
	//prepare statement w/ try/catch
	long gasStationId = rs.getLong("id");
	double totalLiters = rs.getLong("total_liters");
	totalLitersFilled.put(gasStationId, totalLiters);
	return totalLitersFilled 
	
}
```

-  I want to see the total savings of a fuel stop
```sql 
SELECT fs.id, fs.total_savings
FROM fuel_saver.fuel_stop fs
WHERE fs.id = ?;

```
```java
public Map<long, double> getTotalSavings(int fuelStopId){
	String sql = "";
	Map<long, double> totalSavings = new Map<>();
	//prepare stateent w/ try/catch
	long fuelStopId = rs.getLong("id");
	DecimalFormat df = new DecimalFormat("#.##");
	df.setRoundingMode(RoundingMode.CEILING);
	double totalLiters = df.format(rs.getLong("total_savings"));
	totalSavings.put(fuelStopId, totalLiters);
	return totalSavings;
	

}
```

-  I want to see the users name and user id of who filled up
```sql
SELECT d.id AS driver_id, 
       d.first_name || ' ' || d.last_name AS driver_name, 
       fs.stop_timestamp
FROM fuel_saver.fuel_stop fs
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE fs.id = ?;
```
```java
public Map<long, String> getDriverForFuelStop(int fuelStopId){
	String sql = "";
	Map<long, string> driverIdAndName = new Map<>();
	// prepare statement w/ try/catch
	long driverId = rs.getLong("id");
	String driverName = rs.getString("driver_name");
	driverIdAndName.put(driverId, driverName);
	return driverIDAndName; 
}
```

- I want to see total savings per custom time period of using the fuel-saver per driver or for all drivers
	- For a company, there would need to be a company table?
	- Replace d.id = ? with d.maptrip_manager_company = ? 
```SQL
SELECT d.id AS driver_id, 
       d.first_name || ' ' || d.last_name AS driver_name, 
       SUM(fs.total_savings) AS total_savings
FROM fuel_saver.fuel_stop fs
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = ?
AND fs.stop_timestamp BETWEEN '2024-07-01' AND '2024-07-31' //replace with ? 
GROUP BY d.id, d.first_name, d.last_name;
```
```java
public double getTotalSavingsForDriver(int driverId, String startDate, String endDate){ //string? What else is more type safe? 
	double totalSavings = 0.0;
	String sql = "";
	//prepare statement with try/catch
	//asign rs.getDouble("total_savings") to totalSavings and use #.## format
	return totalSavings
}
```


- I want to see which of my drivers is saving the most per month/per year on fuel
```sql
SELECT d.id AS driver_id, 
                       d.first_name || ' ' || d.last_name AS driver_name,
                       EXTRACT(YEAR FROM fs.stop_timestamp) AS year, 
                       EXTRACT(MONTH FROM fs.stop_timestamp) AS month, 
                       SUM(fs.total_savings) AS total_savings 
                       FROM fuel_saver.fuel_stop fs 
                       JOIN fuel_saver.device dev ON fs.device_id = dev.id 
                       JOIN fuel_saver.driver d ON dev.driver_id = d.id 
                       WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = ? AND EXTRACT(MONTH FROM fs.stop_timestamp) = ? AND d.id = ?
                       GROUP BY d.id, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp), EXTRACT(MONTH FROM fs.stop_timestamp) 
                       ORDER BY total_savings DESC;
```

```java
public Array getMonthlySavingsForDriver(int month, int year, long driverId){
	String sql = "";
	JSONArray result = new JSONArray();
	
		try (
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setInt(1, year);
            pstmt.setInt(2, month);
            pstmt.setInt(3, driverId);
            ResultSet rs = pstmt.executeQuery();

            while (rs.next()) {
                JSONObject row = new JSONObject();
                row.put("driver_id", rs.getInt("driver_id"));
                row.put("driver_name", rs.getString("driver_name"));
                row.put("year", rs.getInt("year"));
                row.put("month", rs.getInt("month"));
                row.put("total_savings", rs.getDouble("total_savings"));

                result.add(row);
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }

        return result;
    }
}

```
 - I want to be able to see my organization as a whole but also see individual drivers
 
```java
//don't yet have an organization, so that doesn't work 
//for individual driver -> return total_savings
```
-  I want to see how much I've spent on fuel each month/year
```sql
SELECT d.id AS driver_id,
	d.maptrip_manager_company,
       d.first_name || ' ' || d.last_name AS driver_name,
       EXTRACT(YEAR FROM fs.stop_timestamp) AS year, 
       SUM(fs.number_of_liters * fs.price_per_liter) AS total_spent 
FROM fuel_saver.fuel_stop fs 
JOIN fuel_saver.device dev ON fs.device_id = dev.id 
JOIN fuel_saver.driver d ON dev.driver_id = d.id 
WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = 2024 
AND d.maptrip_manager_company = 2
GROUP BY d.maptrip_manager_company, d.id, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp) 
ORDER BY total_spent DESC;
```
```java
//for monthly, add another parameter and add to sql statement
public double getYearlySavingsForCompany(int year, long maptripManagerCompany){
	String sql = "";
	List<Map<String, Object>> result = new ArrayList<>();
	
		try (
             PreparedStatement pstmt = conn.prepareStatement(sql)) {

            pstmt.setInt(1, year);
            pstmt.setInt(2, driverId);
            ResultSet rs = pstmt.executeQuery();

            while (rs.next()) {
                Map<String, Object> row = new HashMap<>();
                row.put("driver_id", rs.getInt("driver_id"));
                row.put("driver_name", rs.getString("driver_name"));
                row.put("year", rs.getInt("year"));
                row.put("total_savings", rs.getDouble("total_savings"));

                result.add(row);
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }

        return result;
    }
}

```

 - I want to see my monthly, yearly, and lifetime savings using fuel-saver
```sql
#yearly
SELECT d.maptrip_manager_company, 
                       d.first_name || ' ' || d.last_name AS driver_name,
                       EXTRACT(YEAR FROM fs.stop_timestamp) AS year, 
                       SUM(fs.total_savings) AS total_savings 
                       FROM fuel_saver.fuel_stop fs 
                       JOIN fuel_saver.device dev ON fs.device_id = dev.id 
                       JOIN fuel_saver.driver d ON dev.driver_id = d.id 
                       WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = ? 
						AND d.maptrip_manager_company = ?
                       GROUP BY d.id, d.maptrip_manager_company, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp)
                       ORDER BY total_savings DESC

#monthly
SELECT d.maptrip_manager_company, 
                       d.first_name || ' ' || d.last_name AS driver_name,
                       EXTRACT(YEAR FROM fs.stop_timestamp) AS year, 
                       EXTRACT(MONTH FROM fs.stop_timestamp) AS month,
                       SUM(fs.total_savings) AS total_savings 
                       FROM fuel_saver.fuel_stop fs 
                       JOIN fuel_saver.device dev ON fs.device_id = dev.id 
                       JOIN fuel_saver.driver d ON dev.driver_id = d.id 
                       WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = ?
						AND d.maptrip_manager_company = ?
                       GROUP BY d.id, d.maptrip_manager_company, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp), EXTRACT(MONTH FROM fs.stop_timestamp)
                       ORDER BY year, month, total_savings DESC
```
```java
public JSONObject getYearlySavings(int year, int companyId){
	String sql = "SELECT d.maptrip_manager_company, \r\n"
	+ " d.first_name || ' ' || d.last_name AS driver_name,\r\n"
	+ " EXTRACT(YEAR FROM fs.stop_timestamp) AS year, \r\n"
	+ " d.id AS driver_id, \r\n "
	+ " SUM(fs.total_savings) AS total_savings \r\n"
	+ " FROM fuel_saver.fuel_stop fs \r\n"
	+ " JOIN fuel_saver.device dev ON fs.device_id = dev.id \r\n"
	+ " JOIN fuel_saver.driver d ON dev.driver_id = d.id \r\n"
	+ " WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = ? \r\n"
	+ " AND d.maptrip_manager_company = ?\r\n"
	+ " GROUP BY d.id, d.maptrip_manager_company, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp)\r\n"
	+ " ORDER BY total_savings DESC";
	
	JSONArray arr = new JSONArray();

	try (PreparedStatement pstmt = connection.prepareStatement(sql)) {
		pstmt.setInt(1, year);
		pstmt.setInt(2, companyId);

		ResultSet rs = pstmt.executeQuery();
		while (rs.next()) {
			JSONObject ob = new JSONObject();
			ob.put("maptrip_manager_company", rs.getInt("maptrip_manager_company"));
			ob.put("driver_id", rs.getInt("driver_id"));
			ob.put("driver_name", rs.getString("driver_name"));
			ob.put("year", rs.getInt("year"));
			ob.put("total_savings", rs.getDouble("total_savings"));
			
			arr.put(ob);
			}

	  } catch (SQLException e) {
			e.printStackTrace();
			}
	System.out.println(arr);
}

```
- I want my boss to see how much I have saved him
-  I want to receive a tip from my boss
-  I want to be able to sort by name of driver and amount saved
-  I want to see which driver has saved and which hasn't
-  I want to see details of a driver: Where/when has he filled up? How many liters did he fill? What was the fuel type? At what price did he fill up?
```sql
SELECT gs.station_name, gs.latitude, gs.longitude, fs.stop_timestamp, fs.fuel_type, fs.number_of_liters, fs.price_per_liter, fs.total_savings
FROM fuel_saver.gas_station gs
JOIN fuel_saver.fuel_stop fs ON gs.id = fs.station_id
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = 2
GROUP BY gs.station_name, gs.latitude, gs.longitude, fs.stop_timestamp, fs.fuel_type, d.id, fs.number_of_liters, fs.price_per_liter, fs.total_savings;
```



```sql
SELECT gs.station_name, gs.latitude, gs.longitude, SUM(fs.number_of_liters) AS total_liters, SUM(fs.price_per_liter) AS total_price, SUM(fs.total_savings) AS total_savings
FROM fuel_saver.gas_station gs
JOIN fuel_saver.fuel_stop fs ON gs.id = fs.station_id
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = 2
GROUP BY gs.station_name, gs.latitude, gs.longitude; //get price, liters, savings, location by driver

SELECT d.id AS driver_id, gs.station_name, gs.latitude, gs.longitude, SUM(fs.number_of_liters) AS total_liters, fs.id AS fuel_stop_id
FROM fuel_saver.gas_station gs
JOIN fuel_saver.fuel_stop fs ON gs.id = fs.station_id
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = 2
GROUP BY d.id, fs.id, gs.station_name, gs.latitude, gs.longitude; //get driver id, fs.id, gs.name, & lat lon
```
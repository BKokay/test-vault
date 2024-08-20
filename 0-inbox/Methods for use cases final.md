---
created: 2024-08-20T09:36
updated: 2024-08-20T13:39
---
Generally, the method will have this format:
```java
public JSONArray returnAnArrayOfObjects(int foo, String bar){
	String sql = "SELECT ? FROM fuel_saver.table_name" 
				+ "WHERE d.id = ?";//just an example 
	JSONArray result = new JSONArray();
	try(PreparedStatement pstmt = conn.prepareStatement(sql)){
		pstmt.setString(1, bar);
		pstmt.setInt(2, foo);

		ResultSet rs = pstmt.executeQuery();

		while(rs.next()){
			JSONObject row = new JSONObject();
			row.put("row_name_1", rs.getString("row_name_1"));
			row.put("row_name_2", rs.getInt("row_name_2"));

			result.add(row);
		}
	} catch (SQLException e){
		e.printStackTrace();
	}

	return result; 
}
```

As a fleet owner...
- I want to see the location of a fuel station
	- in GasStationDaoImpl
	- parameters: gas_station.id
	- returns: Point (long, lat) 
```java
public Point getGasStationLocation(int gasStationId){
	String sql = "SELECT latitude, longitude FROM fuel_saver.gas_station WHERE id = ?";
	Point p = new Point();
	try(PreparedStatement pstmt = conn.prepareStatement(sql)){
		pstmt.setInt(1, gasStationId);

		while(rs.next()){
			p.setLocation(rs.getDouble("longitude"), rs.getDouble("latitude"));
		}
	} catch(SQLException e){
		e.printStackTrace();
	}

	return p; 
}
```

-  [x] I want to see the time and the date of a fuel stop
	- in FuelStopDaoImpl
	- parameters: fuel_stop.id
	- returns: [{stop_timestamp: "", year: "", month: "", formatted_time:""}]
```sql
SELECT stop_timestamp, 
	EXTRACT (YEAR FROM stop_timestamp) AS year, 
	EXTRACT (MONTH FROM stop_timestamp) AS month,
	TO_CHAR(stop_timestamp, 'HH24:MI:SS') AS formatted_time
	FROM fuel_saver.fuel_stop 
	WHERE id = ?
```
| stop_timestamp         | year | month | formatted_time |
|------------------------|------|-------|----------------|
| 2024-07-19 13:00:00+02 | 2024 | 7     | 13:00:00       |

- I want to see the price per liter of a fuel station
	- in GasStationDaoImpl
	-  parameters: gas_station.id
	- returns:  [{price_per_liter: "", station_id: "", station_name: ""}]
```sql
SELECT fs.price_per_liter, fs.station_id, gs.station_name
	FROM fuel_saver.fuel_stop fs 
	JOIN fuel_saver.gas_station gs ON fs.station_id = gs.id 
	WHERE gs.id = ?
```

- I want to see the average price per liter of other fuel stations along the route *I don't know where to start with this*

- I want to see the number of liters filled at a fuel station 
	- in DriverDaoImpl
	- this is assuming that we want it per fuel stop, not just a sum of all fuel stops at that gas station
	- parameters: driver.id
	- returns: [{gas_station_id: "", liters_filled: "", stop_timestamp: ""}]
```sql
SELECT gs.id AS gas_station_id, 
	fs.number_of_liters AS liters_filled,
	TO_CHAR(fs.stop_timestamp, 'YYYY-MM-DD HH24:MI:SS') AS stop_timestamp
FROM fuel_saver.gas_station gs
JOIN fuel_saver.fuel_stop fs ON gs.id = fs.station_id
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = 2
GROUP BY gs.id, fs.number_of_liters, fs.stop_timestamp;
```

- [x] I want to see the total savings of a fuel stop
	- in FuelStopDaoImpl
	- parameters: fuel_stop.id
	- returns: {fuel_stop_id: "", total_savings: ""}
```sql
SELECT fs.id AS fuel_stop_id, fs.total_savings
FROM fuel_saver.fuel_stop fs
WHERE fs.id = ?;
```

- [x] I want to see the user's name and user id of who filled up 
	- in FuelStopDaoImpl
	- parameters fuel_stop.id
	- returns: {driver_id: "", driver_name: "", stop_timestamp: "" } //return timestamp here? 
```sql 
SELECT d.id AS driver_id, 
       d.first_name || ' ' || d.last_name AS driver_name, 
       TO_CHAR(fs.stop_timestamp, 'YYYY-MM-DD HH24:MI:SS') AS stop_timestamp
FROM fuel_saver.fuel_stop fs
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE fs.id = ?;
```

- I want to see total savings per custom time period of using the fuel-saver per driver or for all drivers
	- in DriverDaoImpl //should be two methods or could just be one with a param for companyOrDriver
	- parameters: id, startTimeString, endTimeString, companyOrDriver
	- returns: {driver_id: "", driver_name: "", total_savings: ""} if using driver id
	- returns: {company_id: "", total_savings: ""} if using company id
```sql
using driver id
SELECT d.id AS driver_id, 
       d.first_name || ' ' || d.last_name AS driver_name, 
       SUM(fs.total_savings) AS total_savings
FROM fuel_saver.fuel_stop fs
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = ?
AND fs.stop_timestamp BETWEEN ? AND ? 
GROUP BY d.id, d.first_name, d.last_name;

using company id 
SELECT d.maptrip_manager_company AS company_id, 
       SUM(fs.total_savings) AS total_savings 
FROM fuel_saver.fuel_stop fs 
JOIN fuel_saver.device dev ON fs.device_id = dev.id 
JOIN fuel_saver.driver d ON dev.driver_id = d.id 
WHERE fs.stop_timestamp BETWEEN ? AND ?  
AND d.maptrip_manager_company = ? 
GROUP BY d.maptrip_manager_company
ORDER BY total_savings DESC;

```

- I want to see which of my drivers is saving the most per month/year on fuel 
	- in DriverDaoImpl
	- params: companyId, startTimeString, endTimeString
	- returns: {driver_id: "", driver_name: "", total_savings: ""}
```sql
SELECT d.id AS driver_id, 
       d.first_name || ' ' || d.last_name AS driver_name,
       SUM(fs.total_savings) AS total_savings
FROM fuel_saver.fuel_stop fs
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.maptrip_manager_company = ? 
AND fs.stop_timestamp BETWEEN ? AND ? 
GROUP BY d.id, d.first_name, d.last_name
ORDER BY total_savings DESC;
```

- I want to be able to see my organization as a whole but also see individual drivers
	- the three queries above will cover this use case

- I want to see how much I've spent on fuel each year
	- in DriverDaoImpl? CompanyDao doesn't exist - should it? 
	- parameters: companyID, year
	- returns: [{driver_id: "", maptrip_manager_company: "", driver_name: "", year: "", total_spent: ""}]
```sql
SELECT d.id AS driver_id,
	d.maptrip_manager_company,
       d.first_name || ' ' || d.last_name AS driver_name,
       EXTRACT(YEAR FROM fs.stop_timestamp) AS year, 
       SUM(fs.number_of_liters * fs.price_per_liter) AS total_spent 
FROM fuel_saver.fuel_stop fs 
JOIN fuel_saver.device dev ON fs.device_id = dev.id 
JOIN fuel_saver.driver d ON dev.driver_id = d.id 
WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = ? 
AND d.maptrip_manager_company = ?
GROUP BY d.maptrip_manager_company, d.id, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp) 
ORDER BY total_spent DESC;
```

- I want to see how much I've spend on fuel each month 
	- in DriverDaoImpl/CompanyDaoImpl
	- parameters: companyId, year, month(int)
	- returns: [{driver_id: "", maptrip_manager_company: "", driver_name: "", year: "", month: "", total_spent: ""}]
```sql
SELECT d.id AS driver_id,
	d.maptrip_manager_company,
       d.first_name || ' ' || d.last_name AS driver_name,
       EXTRACT(YEAR FROM fs.stop_timestamp) AS year, 
		EXTRACT(MONTH FROM fs.stop_timestamp) AS month,
       SUM(fs.number_of_liters * fs.price_per_liter) AS total_spent 
FROM fuel_saver.fuel_stop fs 
JOIN fuel_saver.device dev ON fs.device_id = dev.id 
JOIN fuel_saver.driver d ON dev.driver_id = d.id 
WHERE EXTRACT(YEAR FROM fs.stop_timestamp) = ? AND EXTRACT(MONTH FROM fs.stop_timestamp) = ?
AND d.maptrip_manager_company = ?
GROUP BY d.maptrip_manager_company, d.id, d.first_name, d.last_name, EXTRACT(YEAR FROM fs.stop_timestamp), EXTRACT(MONTH FROM fs.stop_timestamp) 
ORDER BY total_spent DESC;
```

- I want to see my monthly, yearly, lifetime savings using fuel-saver
	- this is covered by the above use cases
-  I want my boss to see how much I have saved him
	- query savings by driver as above
-  I want to receive a tip from my boss
	- this is implemented later
-  I want to be able to sort by name of driver and amount saved
	- this is done on the company savings query above
-  I want to see which driver has saved and which hasn't
	- same as above - you can see the total savings per driver in a company 
-  I want to see details of a driver: Where/when has he filled up? How many liters did he fill? What was the fuel type? At what price did he fill up?
	- DriverDaoImpl
	- parameters: driverId
	- returns: [{fuel_stop_id: "", stop_timestamp: "", number_of_liters: "", price_per_liter: "", total_savings: "", station_id: "" station_name: "", fuel_type: "" }]
```sql
SELECT fs.id AS fuel_stop_id, 
       TO_CHAR(fs.stop_timestamp, 'YYYY-MM-DD HH24:MI:SS') AS stop_timestamp, 
       fs.number_of_liters, 
       fs.price_per_liter, 
       fs.total_savings, 
       fs.station_id, 
	fs.fuel_type,
       gs.station_name
FROM fuel_saver.fuel_stop fs
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
JOIN fuel_saver.gas_station gs ON fs.station_id = gs.id
WHERE d.id = ?;
```
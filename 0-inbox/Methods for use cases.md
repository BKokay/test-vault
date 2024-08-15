---
created: 2024-08-15T13:44
updated: 2024-08-15T15:09
---
[[Notes from Georg]] | [[Fuel saver user stories]] 

- [ ]  I want to see the time and date of a fuel stop
	-  FuelStopService.get(int id) -> this will already be implemented, do I want to *only* return the fuel_stop.stop_timestamp? 
- [ ]  I want to see the location of a gas station - show lat/lon 
```java
	public Point getLocation(int id) {
		String sql = "SELECT latitude, longitude FROM fuel_saver.gas_station WHERE id = ?";
		//prepare statement here/ try catch
		Point p = new Point();
		p.setLocation(rs.getDouble("longitude"), rs.getDouble("latitude"));
		return p	
	} 
```

- [ ]  I want to see the price per liter of a gas station //GasStationDao & Impl
```java
public Double getPricePerLiter(int id) {
	String sql = "SELECT fs.price_per_liter, fs.stop_timestamp FROM fuel_saver.fuel_stop fs JOIN fuel_saver.gas_station gs ON fs.station_id = gs.id WHERE gs.id = ?"
	Map<LocalDateTime, double> fuelStopsPrice = new HashMap<>();
	//prepare statement here/ try/catch
	LocalDateTime stopTimestamp = rs.getTimestamp("stop_timestamp").toLocalDate();
	double pricePerLiter = rs.getDouble("price_per_liter");
	fuelStopsPrice.put(stopTimestamp, pricePerLiter);
	return fuelStops;
}
```
- [ ] I want to see the average price per liter of other gas stations along the route
	- this is complicated... do I check the lat/lon of a station in relation to the route?
```java

```
- [ ] I want to see the number of liters filled at a gas station - for a certain stop? For a certain driver?  
```sql
SELECT gs.station_name, gs.latitude, gs.longitude, SUM(fs.number_of_liters) AS total_liters, SUM(fs.price_per_liter) AS total_price, SUM(fs.total_savings) AS total_savings
FROM fuel_saver.gas_station gs
JOIN fuel_saver.fuel_stop fs ON gs.id = fs.station_id
JOIN fuel_saver.device dev ON fs.device_id = dev.id
JOIN fuel_saver.driver d ON dev.driver_id = d.id
WHERE d.id = 2
GROUP BY gs.station_name, gs.latitude, gs.longitude;
```
```java
public double getLitersFilled(int id){
	String sql = 
}
```
1. I want to see the total savings of a fuel stop
2. I want to see the users name and user id of who filled up
3. I want to see total savings per custom time period of using the fuel-saver per driver or for all drivers
4. I want to see which of my drivers is saving the most per month/per year on fuel
5. I want to be able to see my organization as a whole but also see individual drivers
6. I want to see how much I've spent on fuel each month/year
7. I want to see my monthly, yearly, and lifetime savings using fuel-saver
8. I want my boss to see how much I have saved him
9. I want to receive a tip from my boss
10. I want to be able to sort by name of driver and amount saved
11. I want to see which driver has saved and which hasn't
12. I want to see details of a driver: Where/when has he filled up? How many liters did he fill? What was the fuel type? At what price did he fill up?
13. 
A set of practice problems from Georg
-  give me a list of all gas station names which are between 51.02499, 6.77267 and 50.68641, 7.31435, sorted alphabetically
	1.  SELECT station_name
			FROM fuel_saver.gas_station gs //rename to gs
			WHERE longitude BETWEEN 6.77267 AND 7.31435
			AND latitude BETWEEN 50.68641 AND 51.02499
			ORDER BY station_name ASC
-  what are the names of the drivers who did a fuel stop yesterday?
	1. SELECT drivers.first_name, drivers.last_name
			FROM fuel_saver.drivers d
			JOIN fuel_saver.fuel_stops fs ON d.devices_id = fs.device_id
			WHERE DATE(fs.stop_timestamp) = '2024-07-22'
 - what gas stations did the driver with ID 12345 already stop at?
	1. SELECT gas_station.station_name, drivers.id, drivers.first_name || '  ' || drivers.last_name full_name //make this the name of  the column joining those two together
			FROM fuel_saver.gas_station
			JOIN fuel_saver.fuel_stops ON gas_station.id = fuel_stops.station_id
			JOIN fuel_saver.drivers ON fuel_saver.drivers.devices_id = fuel_saver.fuel_stops.device_id
			WHERE fuel_saver.drivers.id = 1
- Calculate the total number of liters of fuel consumed by each driver, and list the driver ID and the total fuel consumption, sorted by the total fuel consumption in descending order.
	1. SELECT fuel_saver.drivers.id AS driver_id, SUM(fuel_saver.fuel_stops.number_of_liters) AS total_fuel_consumed 
			FROM fuel_saver.fuel_stops
			JOIN fuel_saver.devices ON fuel_stops.device_id = devices.id
			JOIN fuel_saver.drivers ON devices.id = drivers.devices_id
			GROUP BY drivers.id
			ORDER BY total_fuel_consumed DESC
- Calculate the total savings of each driver 
	 1. SELECT d.id AS driver_id, SUM(fs.total_savings) as total_savings
		 FROM fuel_saver.fuel_stops fs
		 JOIN fuel_saver.devices dev ON fs.device_id = dev.id
		 JOIN fuel_saver.drivers d ON dev.id = d.devices_id
		 GROUP BY d.id
		 ORDER BY total_savings DESC

Commands used:
[[SELECT]], [[FROM]], [[JOIN]], [[SUM]], [[GROUP BY]], [[ORDER BY]], [[AS]], [[ON]], [[WHERE]]
 


#edit device_id and devices_id is not the same for fuel_stops and drivers. Plural in one and not the other 

[[postgresql]]
[[practice]]
[[sql]]
[[databases]]
## Links:


2024-07-23 13:51

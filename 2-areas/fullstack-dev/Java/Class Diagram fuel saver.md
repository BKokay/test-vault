---
created: 2024-08-01T13:20
updated: 2024-08-01T14:09
---
Need classes for every table:
Where do the [[getter and setter methods]] belong?
- drivers: //should I keep all of these plural? #question
	- DriverDao: `public interface DriverDao`
	- DriverDaoImpl: ` public class DriverDaoImpl implements DriverDao`
	- Driver `public class Driver`
- fuel_stops
	- FuelStopDao `public interface FuelStopDao`
	- FuelStopDaoImpl: `public class FuelStopDaoImpl implements FuelStopDao`
	- FuelStop `public class FuelStop`
- gas_stations
	- GasStationDao `public interface GasStationDao`
	- GasStationDaoImpl `public class GasStationDaoImpl implements GasStationDao`
	- GasStation `public class GasStation`


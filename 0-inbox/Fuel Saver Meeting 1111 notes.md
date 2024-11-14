#### Open Questions:

#### TODO: 
1. Add endpoints for device to be showing fuel savings ( because currently don't have a driver )
	1. /api/driver/id/financialsummary - do in device. 
		1. FinancialSummaryDTO should have the year and month queried. 
	2. /api/device/{id}/stophistory 
	3. /api/device/{id}/financialsummary
	4. 
Issue with financial summary: Check in DAO and see what I did about the timestamp 
 PreparedStatementCallback; bad SQL grammar [SELECT fs.id AS fuel_stop_id, TO_CHAR(fs.stop_timestamp, 'YYYY-MM-DD HH24:MI:SS') AS stop_timestamp, fs.number_of_liters, fs.price_per_liter, fs.total_savings, fs.gas_station_id, fs.fuel_type, gs.gas_station_name FROM fuel_saver.fuel_stop fs JOIN fuel_saver.device dev ON fs.device_id = dev.id JOIN fuel_saver.driver d ON dev.driver_id = d.id JOIN fuel_saver.gas_station gs ON fs.gas_station_id = gs.id WHERE d.id = ?] 
 *The DB dump set the time to time with timezone rather than timestamp with timezone *

Hard coded the dbsetup rather than using the db dump 

1. Add methods for DeviceDaoImpl
	- [x] getStopHistory
	- [x] getFinancialSummaryByMonth
	- [x] getFinancialSummaryByYear
2. Add methods for DeviceService 
	- [x] getStopHistory
	- [x] getFinancialSummaryByMonth
	- [x] getFinancialSummaryByYear
4. Add methods for DeviceController
	- [x] getStopHistory
	- [x] getFinancialSummaryByMonth
	- [x] getFinancialSummaryByYear
5. ~~All get methods should be an optional in the dao layer and then unpacked in the service layer - right? Look at the get method and see what you see~~ 
		1. Already check for null and then throw emptyresult
6. Add tests for new methods
7. Go back and clean up logs
8. Figure out how to not show DriverController and all Driver models in swagger-ui
9. Run ansible script to have updated DB without driver table
10. Test locally
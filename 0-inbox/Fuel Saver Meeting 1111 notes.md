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
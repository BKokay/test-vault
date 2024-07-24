2024-07-24 12:56

[[create tables]] [[sql]] #database [[fuel-saver ER model]] [[enum type]]
``` SQL
CREATE TYPE fuel_type AS ENUM ('diesel', 'petrol', 'electric', 'lpg', 'cng');

CREATE TABLE driver (
	id BIGINT PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	oauth_id BIGINT,
	oauth_provider BIGINT,
	company_id BIGINT NOT NULL,
	device_id BIGINT NOT NULL,
	FOREIGN KEY (company_id) REFERENCES companies(id), --- what will this reference? 
	FOREIGN KEY (device_id) REFERENCES devices(id),	 
);

CREATE TABLE devices (
	id BIGINT PRIMARY KEY,
	driver_id BIGINT NOT NULL,
	FOREIGN KEY (driver_id) REFERENCES driver(id)
);

CREATE TYPE gas_station (
	id BIGINT PRIMARY KEY,
	street VARCHAR(100),
	street_number INTEGER,
	zip_code VARCHAR(20),
	city VARCHAR(50),
	country_code VARCHAR(3),
	station_name VARCHAR(200) NOT NULL,
	latitude NUMERIC(8,6) NOT NULL,
	longitude NUMERIC(9,6) NOT NULL
)

CREATE TABLE fuel_stops (
	id BIGINT PRIMARY KEY,
	device_id BIGINT NOT NULL,
	station_id BIGINT NOT NULL,
	stop_timestamp TIMESTAMP WITH TIME ZONE NOT NULL,
	price_per_liter NUMERIC NOT NULL,
	number_of_liters NUMERIC NOT NULL,
	total_savings NUMERIC NOT NULL,
	fuel_type fuel_saver.fuel_type,
	FOREIGN KEY (device_id) REFERENCES devices(id),
	FOREIGN KEY (station_id) REFERENCES gas_station(id)
);

```

## Links:




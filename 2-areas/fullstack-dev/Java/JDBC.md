---
created: 2024-07-26T13:40
updated: 2024-07-31T12:00
---
JDBC - Java Database Connectivity

In order to connect to a database, the database has to be turned on/connected in postgres

Then you need to have a class that establishes the connection. 
```java
package de.infoware.test;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DB {
	public static Connection connect() {
		
		try {
			// Get database credentials from DatabaseConfig class
			String jdbcUrl = "jdbc:postgresql://localhost:5432/test";
			String user = "postgres";
			String password = "";

			// Open a connection
			return DriverManager.getConnection(jdbcUrl, user, password);
		} catch (SQLException e) {
			System.err.println(e.getMessage());
			return null;
		}
	}
}
```

Then [[Connect to database | create a connector class]] which uses this class. 

[[java]]
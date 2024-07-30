---
created: 2024-07-25T15:19
updated: 2024-07-30T13:51
---
``` java
package de.infoware.test;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger; 

public class Test {

	public static void main(String[] args) {
		Connection connection = DB.connect(); //establish connection
		if (connection == null) { //error handling
			System.out.println("Database not available");
			System.exit(0);
		}
		System.out.println(connection);//org.postgresql.jdbc.PgConnection@db57326
		String sql = "SELECT * FROM fuel_saver.gas_station";
		try {
			Statement stmt = connection.createStatement();
			ResultSet rs = stmt.executeQuery(sql);
			while (rs.next()) {
				System.out.println(rs.getLong("id"));
			}
		} catch (SQLException e) {
			e.printStackTrace();
		} finally { 
		// will always run even if connection is made. At the end of running
			if (connection != null) {
				try {
					connection.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}
	}
}
```

use [[JDBC]] to establish a connection to a database
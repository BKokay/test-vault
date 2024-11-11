---
created: 2024-08-13T10:11
updated: 2024-08-13T10:30
---
Java update method to send an SQL update statement

```java
@Override

public void update(Driver driver, Map<String, Object> fieldsToUpdate) {

	if (fieldsToUpdate == null || fieldsToUpdate.isEmpty()) {

	throw new IllegalArgumentException("No fields provided to update."); //More specific error message
	}

	StringBuilder sql = new StringBuilder("UPDATE fuel_saver.driver SET "); //StringBuilder allows you to dynamically build a String

	int index = 0; //start here

	for (String key : fieldsToUpdate.keySet()) { //for-each loop syntax the `:` separates the loop variable `key` from the collection being iterated over `fieldsToUpdate.keySet()`

		sql.append(key).append(" = ?"); //add the key name and a `= ?` to the StringBuilder

		if (index < fieldsToUpdate.size() - 1) {
			sql.append(", "); //if current column is last one in the map, you need to add a comma after the SQL statement 
		}

		index++; 

	}
	sql.append(" WHERE id = ?"); //last bit after going through all columns

  

	try (PreparedStatement pstmt = this.connection.prepareStatement(sql.toString())) {

	int paramIndex = 1; //PreparedStatements are indexed at 1

	for (Object value : fieldsToUpdate.values()) {
		pstmt.setObject(paramIndex++, value); //sets the current value from the map to the corresponding `?` in the SQL query and the index for the PreparedStatement
	}
	pstmt.setLong(paramIndex, driver.getId()); //set the final index to the driver id in the WHERE statement
 
	int rowsUpdated = pstmt.executeUpdate(); // this is needed to actually execute the update

	if (rowsUpdated > 0) {
		logger.info("Driver with id " + driver.getId() + " updated.");
	} else {
		logger.warn("No driver found with id " + driver.getId());
	} //Add logging

	} catch (SQLException e) {

		e.printStackTrace();

	}

}
```

[[java]] [[database]] [[sql]]
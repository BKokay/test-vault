---
created: 2024-08-19T11:26
<<<<<<< HEAD
updated: 2024-09-04T08:49
=======
updated: 2024-09-23T11:57
>>>>>>> 9bdce39565b602fd1e4387e0e8dddea923455ea8
---
A package to create JSON data in java

https://github.com/stleary/JSON-java?tab=readme-ov-file

https://mvnrepository.com/artifact/org.json/json/20240303

```java
public JSONArray returnAnArrayOfObjects(int foo, String bar){
	String sql = "SELECT ? FROM fuel_saver.table_name" 
				+ "WHERE d.id = ?";//just an example 
	JSONArray result = new JSONArray();
	try(PreparedStatement pstmt = conn.prepareStatement(sql)){
		pstmt.setString(1, bar);
		pstmt.setInt(2, foo);

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

[[java]] [[apache maven]]
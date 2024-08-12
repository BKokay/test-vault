---
created: 2024-08-12T14:14
updated: 2024-08-12T14:22
---
**PreparedStatement** is a pre-compiled SQL statement which allow for more security because hackers cannot use SQL injection attacks. Instead of hard-coding queries, PreparedStatement object provides a feature to execute a parameterized query. 
So rather than 
```
select * from students where age>10 and name ='Chhavi'
```
We can use 
```
PreparedStatement pstmt;
String sql = "select * from students where age> ? and name = ?";
pstmt = connection.prepareStatement(sql);
pstmt.setInt(1, 10);
pstmt.setString(2, "Chhavi");
ResultSet rs = pstmt.executeQuery();
```

**Methods of PreparedStatement:**

- **setInt(int, int):** This method can be used to set integer value at the given parameter index.
- **setString(int, string):** This method can be used to set string value at the given parameter index.
- **setFloat(int, float):** This method can be used to set float value at the given parameter index.
- **setDouble(int, double):** This method can be used to set a double value at the given parameter index.
- **executeUpdate():** This method can be used to create, drop, insert, update, delete etc. It returns int type.
- **executeQuery():** It returns an instance of ResultSet when a select query is executed.
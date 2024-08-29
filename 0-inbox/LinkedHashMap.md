---
created: 2024-08-22T13:07
updated: 2024-08-22T18:57
---
```java
public Optional<JSONArray> getPricePerLiter(int id) throws IOException {
    String sql = "";
    JSONArray arr = new JSONArray();

    try (PreparedStatement pstmt = this.connection.prepareStatement(sql)) {
        pstmt.setInt(1, id);
        ResultSet rs = pstmt.executeQuery();

        while (rs.next()) {
            // Use LinkedHashMap to maintain insertion order
            Map<String, Object> map = new LinkedHashMap<>();

            double pricePerLiter = rs.getDouble("price_per_liter");
            map.put("pricePerLiter", pricePerLiter);

            String stopDate = rs.getString("stop_date");
            map.put("stopDate", stopDate);

            String stopTime = rs.getString("stop_time");
            map.put("stopTime", stopTime);

            JSONObject obj = new JSONObject(map);
            arr.put(obj);
        }

        logger.info("Price per liter for station " + id + ": " + arr);
        System.out.println(arr);
        return arr.length() > 0 ? Optional.of(arr) : Optional.empty();
    } catch (SQLException e) {
        e.printStackTrace();
        logger.error("Failed to fetch price per liter for id " + id + ": ", e);
        throw new IOException("Database error occurred", e);
    }
}


```

[[Map Methods]][[java]][[Notes from Georg]]
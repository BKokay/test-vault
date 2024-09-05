---
created: 2024-09-05T09:13
updated: 2024-09-05T09:23
---
in [[posgresql]], you can generate UUIDs using the `uuid-ossp` extension. When creating your table, add 
```sql
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

CREATE TABLE IF NOT EXISTS some_db.test_table (
	id UUID PRIMARY KEY DEFUALT uuid_generate_v4(),
	other VARCHAR(10) NOT NULL,
	etc... 
)
```
[[sql]]
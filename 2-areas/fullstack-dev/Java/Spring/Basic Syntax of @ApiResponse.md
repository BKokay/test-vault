[[Swagger UI]] [[Springdoc]]

```
@ApiResponse(
    responseCode = "200",                   // The HTTP response code (required)
    description = "Operation successful",   // A brief description of the response (required)
    content = @Content(                     // The content of the response (optional)
        mediaType = "application/json",     // The media type (e.g., "application/json", "application/xml")
        schema = @Schema(                   // The schema describing the response body (optional)
            implementation = YourClass.class,   // Maps the schema to a class (optional)
            example = "{ \"key\": \"value\" }"  // Optional example value in JSON format
        )
    ),
    headers = @Header(                      // Describes any response headers (optional)
        name = "X-Rate-Limit",              // Header name
        description = "Rate limit header",  // Description of the header
        schema = @Schema(type = "integer")  // Header data type
    ),
    links = @Link(                          // Adds links to the response (optional)
        name = "getDetails", 
        operationId = "getDetailsById"
    )
)

```

### Elements You Can Use in `@ApiResponse`:

1. **`responseCode` (Required)**:
    
    - The **HTTP status code** returned by the operation, such as `"200"`, `"404"`, `"400"`, etc.
    - Example: `responseCode = "200"`
2. **`description` (Required)**:
    
    - A brief **description** of the response, which explains what it means.
    - Example: `description = "Operation successful"`
3. **`content` (Optional)**:
    
    - Defines the **content type** of the response and the **schema** that describes the response body.
    - **`mediaType`**: The type of content (e.g., `"application/json"`, `"application/xml"`).
    - **`schema`**: Defines the structure of the response body (e.g., linking to a class like `YourClass.class`).
    - **`arraySchema`** : if you return an array of objects, rather than using `@Schema` you would do the following:
```java
@ApiResponse(
    responseCode = "200", 
    description = "Price history found", 
    content = @Content(
        mediaType = "application/json", 
        array = @ArraySchema(schema = @Schema(implementation = GasStationPriceHistoryDTO.class))
    )
)
```

1. **`headers` (Optional)**:

- Describes any **HTTP headers** that may be returned with the response.
2. **`links` (Optional)**:

- Provides **hypermedia links** related to the response. This can include links to other operations.

3. **`ref` (Optional)**:

- You can reference a predefined response object using the **OpenAPI spec** by its reference name.
- Example: `ref = "#/components/responses/YourResponse"`

## Complete example:
```
@ApiResponse(
    responseCode = "200", 
    description = "Successful operation",
    content = @Content(
        mediaType = "application/json", 
        schema = @Schema(implementation = YourClass.class)
    ),
    headers = @Header(
        name = "X-Rate-Limit", 
        description = "Rate limit for this API", 
        schema = @Schema(type = "integer", example = "100")
    ),
    links = @Link(
        name = "getDetails",
        operationId = "getDetailsById"
    )
)
```

### Summary of Key Fields:

- **`responseCode`**: The HTTP status code (e.g., `"200"`, `"404"`, `"500"`).
- **`description`**: A brief explanation of the response.
- **`content`**: Describes the body of the response.
    - **`mediaType`**: The content type (e.g., `"application/json"`).
    - **`schema`**: Describes the structure of the response body, linking to a class or custom schema.
- **`headers`**: Optional HTTP headers that are returned with the response.
- **`links`**: Optional links related to the response, using **HATEOAS**-style links.
- **`ref`**: A reference to a predefined response in the OpenAPI spec (optional).
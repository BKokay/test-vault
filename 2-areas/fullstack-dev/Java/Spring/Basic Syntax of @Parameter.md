[[Swagger UI]] [[Springdoc]]

Basic Syntax : 
```
@Parameter(
    name = "id",                      // The name of the parameter (optional if using @PathVariable/@RequestParam)
    description = "ID of the entity", // A brief description of the parameter
    required = true,                  // Whether the parameter is required (true/false)
    in = ParameterIn.PATH,            // Specifies where the parameter is located (path, query, header, etc.)
    schema = @Schema(type = "string", format = "uuid", example = "550e8400-e29b-41d4-a716-446655440000")  // Describes the parameter type and provides an example
)
@PathVariable String id               // The actual Spring MVC parameter binding
```

### Elements You Can Use in `@Parameter`:

1. **`name` (Optional)**:
    
    - The **name** of the parameter (usually omitted if using `@PathVariable`, `@RequestParam`, etc.).
    - Example: `name = "id"`
2. **`description` (Optional)**:
    
    - A **brief description** of the parameter, explaining what it represents.
    - Example: `description = "ID of the entity"`
3. **`required` (Optional)**:
    
    - Defines whether the parameter is **required** or **optional**. Defaults to `true` for path variables and query parameters unless specified otherwise.
    - Example: `required = true`
4. **`in` (Optional)**:
    
    - Specifies the location of the parameter:
        - `ParameterIn.PATH` for path variables.
        - `ParameterIn.QUERY` for query parameters.
        - `ParameterIn.HEADER` for headers.
        - `ParameterIn.COOKIE` for cookies.
    - Example: `in = ParameterIn.PATH`
5. **`schema` (Optional)**:
    
    - Describes the **schema** of the parameter. You can define the type, format, and even provide an example for better Swagger documentation.
    - Example:
```java
schema = @Schema(type = "string", format = "uuid", example = "550e8400-e29b-41d4-a716-446655440000")
```
        
6. **`allowEmptyValue` (Optional)**:
    
    - Determines if the parameter allows an empty value (applicable for query parameters).
    - Example: `allowEmptyValue = true`
7. **`example` (Optional)**:
    
    - Provides an **example** value that will appear in the Swagger UI for the parameter.
    - Example: `example = "123"`
8. **`deprecated` (Optional)**:
    
    - Marks the parameter as **deprecated** if it’s no longer in use.
    - Example: `deprecated = true`

### Complete Example of `@Parameter` Annotation:

Here’s a comprehensive example of using the `@Parameter` annotation for a method parameter:
```java 
@Parameter(     
	name = "id",     
	description = "UUID of the gas station to be fetched",      
	required = true,      
	in = ParameterIn.PATH,      
	schema = @Schema(type = "string", format = "uuid", example = "550e8400-e29b-41d4-a716-446655440000") 
) 
@PathVariable String id`
```

This describes a **UUID** path variable that is required, and it also provides an example value in **Swagger UI**.

### Parameters in Different Locations:

1. **Path Parameters** (`@PathVariable`):
    
    - These are part of the URL path (e.g., `/stations/{id}`).
    - Example:
```java
@Parameter(     
	description = "ID of the gas station",      
	required = true,      
	schema = @Schema(type = "string", format = "uuid", example = "550e8400-e29b-41d4-a716-446655440000") 
) 
@PathVariable String id`
```
        
2. **Query Parameters** (`@RequestParam`):
    
    - These are appended to the URL as key-value pairs (e.g., `/stations?id=123`).
    - Example:
```java
@Parameter(     
	description = "The year for the financial summary",      
	required = true,      
	schema = @Schema(type = "integer", example = "2023") 
) 
@RequestParam Integer year`
```
        
        
3. **Header Parameters** (`@RequestHeader`):
    
    - These are passed in the HTTP headers (e.g., `Authorization: Bearer token`).
    - Example:
```java
@Parameter(     
	description = "Authorization token",      
	required = true,      
	schema = @Schema(type = "string", example = "Bearer abc123") 
) 
@RequestHeader String authorization`
```
        
4. **Request Body** (`@RequestBody`):
    
    - Although not technically a parameter, you can use **`@RequestBody`** to document the body of a POST/PUT request.
    - Example:
```java
@io.swagger.v3.oas.annotations.parameters.RequestBody(     
	description = "Details of the gas station to create",      
	required = true,      
	content = @Content(         
		mediaType = "application/json",          
		schema = @Schema(implementation = GasStationCreateDTO.class)     
	) 
) 
@RequestBody GasStationCreateDTO gasStationCreateDTO`
```
        
        

### Example with Multiple Parameters:

Let’s say you have a method with a **path parameter**, a **query parameter**, and a **header parameter**. Here’s how you would annotate them:
```java
@GetMapping("/stations/{id}")
@Operation(summary = "Get gas station by ID", description = "Fetch gas station details by ID")
@ApiResponses(value = {
    @ApiResponse(responseCode = "200", description = "successful operation", content = @Content(mediaType = "application/json", schema = @Schema(implementation = GasStation.class))),
    @ApiResponse(responseCode = "404", description = "No gas station found"),
    @ApiResponse(responseCode = "400", description = "Invalid ID format")
})
public ResponseEntity<GasStation> getGasStation(
    
    @Parameter(
        description = "ID of the gas station", 
        required = true, 
        schema = @Schema(type = "string", format = "uuid", example = "550e8400-e29b-41d4-a716-446655440000")
    )
    @PathVariable String id,
    
    @Parameter(
        description = "Year for which the financial summary is requested", 
        required = false, 
        schema = @Schema(type = "integer", example = "2023")
    )
    @RequestParam(required = false) Integer year,

    @Parameter(
        description = "Authorization token for API access", 
        required = true, 
        schema = @Schema(type = "string", example = "Bearer abc123")
    )
    @RequestHeader String authorization
) {
    // Method logic...
}

```
### Explanation:

1. **Path Parameter**: The `id` is passed in the URL path, described as a `UUID`.
2. **Query Parameter**: The `year` is optional and passed as a query parameter (`?year=2023`).
3. **Header Parameter**: The `authorization` token is passed as a header (e.g., `Authorization: Bearer abc123`).

### Summary:

Here’s a breakdown of how you can document your parameters using the `@Parameter` annotation in **SpringDoc**:

- **Path Parameters**: Use `@Parameter` to describe `@PathVariable` fields, such as IDs.
- **Query Parameters**: Use `@Parameter` to describe `@RequestParam` fields, such as filters or pagination.
- **Header Parameters**: Use `@Parameter` to describe `@RequestHeader` fields, such as authorization tokens.
- **Request Body**: Use `@RequestBody` to describe the structure of complex objects sent in the request body.

These annotations help generate clear, user-friendly **Swagger documentation** for your API, ensuring that clients understand what inputs they need to provide.
Check the ID parameter using Spring validation annotation [[Spring Annotations]]
```java
@Parameter(description = ID_OF_DEVICE, required = true, schema = @Schema(type = "string", format = "uuid", example = UUID_EXAMPLE))

@PathVariable @NotBlank @Pattern(regexp = "^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}$", message = "Invalid UUID format") String id
```
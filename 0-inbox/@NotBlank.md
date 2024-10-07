The _@NotBlank_ annotation uses the [_NotBlankValidator_](https://docs.jboss.org/hibernate/validator/6.0/api/org/hibernate/validator/internal/constraintvalidators/hv/NotBlankValidator.html) class, which checks that a character sequence’s trimmed length is not empty:

```java
public boolean isValid(
  CharSequence charSequence, 
  ConstraintValidatorContext constraintValidatorContext)
    if (charSequence == null ) {
        return false; 
    } 
    return charSequence.toString().trim().length() > 0;
}
```
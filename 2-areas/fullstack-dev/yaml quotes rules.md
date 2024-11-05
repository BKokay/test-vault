Let me help you with YAML quoting conventions since you didn't include the YAML code in your message. Here are the general rules for quoting in YAML:

1. Numbers:

- Don't quote: integers and floats (e.g., 42, 3.14)
- Quote: when you want to preserve leading zeros or treat numbers as strings

2. Strings:

- Don't quote: Simple strings with no special characters
- Quote: Strings that contain any of these:
    - Special characters (: { } [ ] , & * # ? | - < > = ! % @ )
    - Leading/trailing whitespace
    - Could be interpreted as numbers/booleans
    - Multi-word strings with spaces
```yaml
# Numbers
port: 8080          # No quotes needed
version: 2.1        # No quotes needed
zip: "00123"        # Quoted to preserve leading zeros

# Simple strings
name: john          # No quotes needed
title: developer    # No quotes needed

# Strings that need quotes
message: "Hello: World"     # Contains special character ':'
path: "/usr/local/bin"     # Contains special character '/'
description: "This is a longer text with spaces"
command: "git push -f"      # Contains special character '-'
status: "true"             # Quoted because it could be interpreted as boolean
id: "123"                  # Quoted because it could be interpreted as number

# Arrays and objects
tags:
  - simple-tag      # No quotes needed
  - "tag:with:colon" # Contains special character
```
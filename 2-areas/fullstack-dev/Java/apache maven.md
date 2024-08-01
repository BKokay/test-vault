---
created: 2024-07-24T13:38
updated: 2024-08-01T10:52
---
all dependencies go into a [[pom.xml]] file. This will be auto generated. You can start a new Maven project in [[Eclipse IDE]] 
[[java]]
resources folder will get env var and if you wanted to put sample sql data or something ** 
logger.debug()
add more info if really logging to server in the <PatternLayout> section of the [[pom.xml]] file

### Correct Steps to Set Up a Maven Project in Eclipse:

1. **Create a New Maven Project**:
    
    - Go to `File -> New -> Maven Project`.
    - Select your workspace location (you can leave it as the default if desired).
    - Check the box for "Create a simple project (skip archetype selection)" if available, then click `Next`. If you don't see this option, proceed to step 4.
    - If you checked "Create a simple project", proceed to step 7.
2. **Select an Archetype**:
    
    - **Skip this step** if you selected "Create a simple project". Otherwise, in the archetype selection screen, type `maven-archetype-quickstart` in the filter box.
    - Select `maven-archetype-quickstart` from the list (this is a basic archetype that sets up the standard Maven project structure).
    - Click `Next`.
3. **Enter Project Details**:
    
    - **Group ID**: Enter `de.infoware.fuelsaver`.
    - **Artifact ID**: Enter a name for your project (e.g., `fuelsaver`).
    - **Version**: Leave as default (`1.0-SNAPSHOT`).
    - **Package**: Enter `de.infoware.fuelsaver`.
    - Click `Finish`.

---
created: 2024-09-27T14:35
updated: 2024-09-27T14:36
---
# Technologies / Topics

## HTML, CSS
- Bootstrap
- Responsive Design
- **SASS?**

## JavaScript
- node.js / NPM
- Object Oriented Programming
- Testing: Which framework?
- TypeScript
- **jQuery**
- vue.js
- **Angular**
- JSDoc

## Java
- Data types
- Control structures
- Object Oriented Programming
- Generics
- **Lambdas**
- Stream API
- **Multithreading**
- Java WebApps
- JUnit
- Maven and **Gradle**
- Spring / Spring Boot

## Databases
- SQL
- Access from Java with JDBC and **SQ**
- **ORM / Hibernate**
- **NoSQL Databases?**

## Miscellaneous
- Tools like SonarQube and **Sentry**
- GitLab CI/CD
- OpenAPI
- **Linux and Windows Servers**
- Administration with Ansible
- **Docker?**
- **MQTT / Mosquitto?**


# Tasks

## ✅ Geocoder Test Page 

- Technology: JS, HTML, CSS
- Complete the task from May
- See 2023-05-22 Geocoder Support Map.md

## ✅ MapTrip Remote Tracking

- Website with a login (MapTrip Manager credentials)
- After login, the page shows a map with all (active?) MapTrip devices of the user
- The page queries the position(s) of the device(s) every minute
- For every device, there is a list of tracking results (time and position)
- The track of positions of a device is shown on the map with markers (larger marker for the current position)
- Every device uses markers in an individual color
- Optional additional task: The tracks are stored in the local history of the browser to make them persistent

## Test Application for vue.js Components

- Technology: vue.js
- DreamDev is creating the new MapTrip Remote Editor with vue.js
- Various components such as address input or route planning should be usable as components
- This test application serves two purposes:
  - Ensure that the components created by DreamDev can be easily used in other applications
  - Provide improved demos for maptrip.de

## MapTrip Server API / openapi-generator (Georg did this)

- Technology: Any, e.g., Java
- Tools like openapi-generator or swagger-codegen generate code from the API specification
- They can generate API clients for dozens of languages
- Software created this way can communicate with the Server API, e.g., via a Java library, instead of via HTTP
- This is used by SafetyCT (C#/.NET?)
- We should test this and also provide our own tutorial

## Reporting Tool for the MapTrip Server API (Georg just did this?)

- Technology: Java, Spring Boot, Database
- Some customers should be billed not by device licenses, but based on usage, such as routes
- Actual usage needs to be counted
- A web application will be implemented to evaluate the logs of the Server API
- Monthly reports will be created, showing usage per company and function (e.g., route, geocoder, matrix, etc.)
- The reports will be generated as PDFs and sent via email to configured addresses (e.g., sales, management)
- Usage data will be stored in a database, so older reports can also be retrieved
- Additionally, a web application will display the current figures and older reports
- The content of the reports and the website will be coordinated with the sales team

## Display Vector Maps in LeafletJS (Georg did this)

- Technology: JavaScript
- Our maps should be displayed in other APIs like LeafletJS
- Our maps are provided by the DataServer as GeoJSON
- The MapAPI:
  - Loads one GeoJSON per tile
  - Creates a canvas
  - Draws the data from the GeoJSON into the canvas
  - Uses a JSON config with colors, line widths, zoom levels, etc.
  - Adds this canvas as a tile into the map
- This function should be ported to LeafletJS

## Web Application for Fuel Savings from MapTrip (Fuel Saver API in progress)

- MapTrip shows the savings when refueling compared to the average price along the route
- So far, this info is stored on the device ("savings this month")
- Instead, it should be transferred to a backend
- The data should be retrievable for all vehicles of a company

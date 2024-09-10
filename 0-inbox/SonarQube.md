---
created: 2024-09-09T10:50
updated: 2024-09-10T11:24
---
Token: 
**sqp_81796c6d4313dea0dd17beecba41ee5837bd06ef**

mvn clean verify sonar:sonar \
  -Dsonar.projectKey=fuel-saver-api \
  -Dsonar.projectName='fuel-saver-api' \
  -Dsonar.host.url=https://sonarqube.infoware.de \
  -Dsonar.token=sqp_81796c6d4313dea0dd17beecba41ee5837bd06ef


In the run configurations tab on Eclipes, add this in the goals:
```
clean verify sonar:sonar  -Dsonar.projectKey=fuel-saver-api   -Dsonar.projectName='fuel-saver-api' 
  -Dsonar.host.url=https://sonarqube.infoware.de   -Dsonar.token=sqp_81796c6d4313dea0dd17beecba41ee5837bd06ef
```
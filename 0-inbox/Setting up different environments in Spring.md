If you have an application-dev.properties and an application-prod.properties, set up eclipse to use -dev as the default. 
In the run configurations, in the VM Arguments section add:
```
-Dspring.profiles.active=dev
```

Then set the active profile in an application.properties file. 
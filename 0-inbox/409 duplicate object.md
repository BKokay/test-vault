Added a new Global Exception called `DuplicateObjectException`. In the save method of the `service` class, I check to see if the device is already present in the db.
```java
Optional<Device> existingDevice = deviceDao.get(device.getId());  
if(existingDevice.isPresent()) {  
    throw new DuplicateObjectException("Device with id " + device.getId() + " already exists");  
}
```
 Then in the controller, I catch the exception to show to the user:
```java
 catch (DuplicateObjectException e) {  
    return ResponseEntity.status(HttpStatus.CONFLICT).body(e.getMessage());  
}
```
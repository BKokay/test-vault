## The problem
The API already has codes and descriptions for the returned errors:
![[Pasted image 20241125115806.png]]
RFCs 7807 and 9457 define the content type application/problem+json and a JSON format to return error messages with details. The server API is to be converted to this.

Do only additional fields have to be added / can the existing fields be retained?
Should the responses always be adapted or only if Accept: application/json, application/problem+json is set?
Generate corresponding URIs for type from the codes? e.g. DETOUR_ERROR_FILE_DOES_NOT_EXIST-> https://api.maptrip.de/problems/detour/file-does-not-exist
Mapping that resolves these error URIs and returns the description? More details later if necessary?


### Notes:
*Problem Details for HTTP APIs* via RFC 7807 is a standard way for conveying machine-readable error details in an HTTP response. In RFC 9457, new dimensions and updates were added to the framework. 

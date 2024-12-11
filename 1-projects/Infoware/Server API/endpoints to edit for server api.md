### /detour
~~GET /detour/attribute/description Get a detour attributes which describes a segment~~
~~PUT /detour/fiel/{fileid}/road/{roadid} Update the attributes of a road from a detour file~~
~~POST /detour/file/{fileid}/segment Create a Detour segment~~
		~~need an array of coordinates and more attributes~~
~~PUT /detour/file/{fileid}/segment/{segmentid} Update the attributes of a segment from a detour file~~
		~~need to add created at and any meta data~~
~~POST /detour/file/{fileid}/segment/match Match a polyline of coordinates..~~ 
		~~need more than one coordinate (OPTIONAL)~~
~~POST /detour/file/{fileid}/segments Create multiple detour segments~~
		~~this needs multiple segments added~~ 
		- [ ] should this have something besides direction 1 priority 10 again?  


##### already edited:
- DetourSegmentRequest - added array of coords and two attributes
- updateDetourSegment- added attributes
- Create a Detour segment - edited DetourSegmentRequest
- Update the attributes of a road from a detour file - added attributes name map_type RS & FCB
- descriptionParam - typo 




```javascript
function transformCoordinates(coordinates) {
  // Split the input string into lines and remove empty lines
  const lines = coordinates.split('\n').filter(line => line.trim());
  
  // Initialize result array
  const formattedCoords = [];
  let currentCoord = [];
  
  // Process each line
  for (const line of lines) {
    // Remove whitespace and brackets
    const cleanLine = line.trim().replace('[', '').replace('],', '').replace(']', '').replace(',', '');
    
    // If line contains numbers, add to current coordinate
    if (cleanLine.match(/[\d.]/)) {
      currentCoord.push(cleanLine);
      
      // When we have a complete coordinate pair
      if (currentCoord.length === 2) {
        const formatted = `{
  "lat": "${currentCoord[0]}",
  "lng": "${currentCoord[1]}"
}`;
        formattedCoords.push(formatted);
        currentCoord = []; // Reset for next coordinate pair
      }
    }
  }
  
  // Join all coordinates with comma and newline
  return formattedCoords.join(',\n');
}
```
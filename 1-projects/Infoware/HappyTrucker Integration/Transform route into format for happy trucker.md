```javascript
import { route } from "./exampleRoute.js";
import * as fs from "node:fs/promises";

function transformCoordinates(coordinates) {
  return coordinates.map(([lat, lng]) => {
    return {
      lat: String(lat),
      lng: String(lng),
    };
  });
}

function convertMapIntoJson(callback) {
  return JSON.stringify(callback, null, 2);
}

const data = transformCoordinates(route);
const dataInJson = convertMapIntoJson(data);

fs.writeFile("results.txt", dataInJson, (err) => {
  if (err) throw err;
});

```
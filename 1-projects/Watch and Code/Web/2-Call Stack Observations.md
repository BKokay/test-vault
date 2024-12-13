The call stack always has whatever function is currently running at the top. 

```javascript
function one() {
    // at the start of console.log, one & (anonymous)
    (2)console.log('start one'); 
    // at the start of two, one & (anonymous)
    (3)two();
    // start of console.log, one, (anonymous)
    (6)console.log('end one')
    // end, one (anonymous)
(7)}

function two() {
    // at the start of console.log, two, one, (anonymous)
    (4)console.log('start two')
    // at the end, two one (anonymous)
(5)}

// at the start of one, (anonymous)
(1)one();(8) // (anonymous)
```
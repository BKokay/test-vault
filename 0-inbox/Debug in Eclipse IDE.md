---
created: 2024-09-26T09:13
updated: 2024-09-26T09:14
---
# Eclipse IDE Debugging Guide
[[Eclipse IDE]]
## Setting Breakpoints

1. Open the Java file you want to debug.
2. In the left margin of the editor (also called the gutter), double-click next to the line number where you want to pause execution. A blue dot will appear, indicating a breakpoint.

## Starting the Debugger

1. Right-click on your test class or method in the Package Explorer.
2. Select "Debug As" > "JUnit Test".

## Using the Debugger

Once the debugger hits a breakpoint, you'll see several useful views:

- **Debug view**: Shows the call stack and allows you to control the debugging process.
- **Variables view**: Displays current values of variables in the selected stack frame.
- **Breakpoints view**: Lists all set breakpoints.
- **Expressions view**: Allows you to evaluate expressions in the current context.

### Debug Controls

In the Debug view, you'll see several control buttons:

- Resume (F8): Continues execution until the next breakpoint.
- Terminate (Ctrl+F2): Stops the debugging session.
- Step Into (F5): Steps into a method call.
- Step Over (F6): Executes the current line and moves to the next one.
- Step Return (F7): Completes the execution of the current method and returns to the caller.

### Inspecting Variables

1. In the Variables view, you can see the values of all variables in the current scope.
2. To watch a specific expression, right-click in the editor and choose "Watch" to add it to the Expressions view.


### Modifying Variables

1. In the Variables view, right-click on a variable and select "Change Value".
2. Enter the new value and press Enter.

### Conditional Breakpoints

1. Right-click on a breakpoint (the blue dot in the gutter).
2. Select "Properties".
3. Enter a condition. The breakpoint will only pause execution when this condition is true.

## Tips

- Use "Run to Line" (Ctrl+R) to run the program until a specific line without setting a breakpoint.
- The "Display" view (Window > Show View > Other > Debug > Display) allows you to evaluate expressions on the fly.
- Use "Step Filtering" (in Debug view preferences) to skip stepping into library code you're not interested in.

Remember, practice makes perfect. The more you use the debugger, the more comfortable and proficient you'll become with it.
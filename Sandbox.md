# Notes de rédaction.



## User Requirements Specification (URS)

| ID  | Requirement                                                                                  |
|-----|---------------------------------------------------------------------------------------------|
| 1   | Read a variable in Node-RED.                                                                |
| 2   | Write a variable in Node-RED.                                                               |
| 3   | Use the Inject node to generate a value.                                                    |
| 4   | Use the Debug node to display a value.                                                      |
| 5   | Use FlowFuse to display a value.                                                            |
| 6   | Use FlowFuse to generate a value.                                                           |
| 6.1 | Use a function to generate a value.                                                         |
| 6.2 | Generate an array.                                                                          |
| 7   | Connect Node-RED with the PLC.                                                              |
| 8   | Read a value from the PLC.                                                                  |
| 9   | Subscribe to a value from the PLC.                                                          |
| 10  | Write a value to a log.                                                                     |
| 11  | Use the concept of a global variable.                                                       |
| 12  | Write a structure to a file.                                                                |
| 13  | Read this structure back from the file.                                                     |


## FAQ

### Is Node-RED compiled?

No, Node-RED is not compiled. It is a flow-based development tool built on Node.js, which is an interpreted JavaScript runtime. Node-RED flows are executed directly by the Node.js engine without a separate compilation step.

### How Node.js works, where is the compiler ?

Node.js works by using the V8 JavaScript engine (the same engine used by Google Chrome) to execute JavaScript code. V8 is responsible for parsing, interpreting, and compiling JavaScript into machine code at runtime.

**Where is the compiler?**
- The "compiler" in this context is built into the V8 engine.
- When you run a Node.js application, your JavaScript code is first parsed and interpreted by V8.
- V8 uses a Just-In-Time (JIT) compiler to convert frequently used JavaScript code into optimized machine code while the program is running.
- This process is invisible to you as a developer; you just write JavaScript, and Node.js (via V8) handles the rest.

**Summary:**  
Node.js does not require you to compile your code manually. The V8 engine inside Node.js automatically compiles JavaScript to machine code at runtime using JIT compilation.

# How works a Just-In-Time (JIT) compiler ?

A Just-In-Time (JIT) compiler is a system that improves program performance by compiling code at runtime, rather than before execution.


## How it works:

### Interpretation:
When your program starts, the code is first interpreted (executed line by line) by the runtime (like V8 in Node.js).

### Hot Spot Detection:
The JIT compiler monitors which parts of the code are used most often ("hot spots").

### Compilation:
When a hot spot is found, the JIT compiler translates that frequently used code from an intermediate language (like JavaScript bytecode) into optimized machine code specific to your CPU.

### Execution:
The next time that code runs, the program uses the compiled machine code, which is much faster than interpreting it again.

### Optimization:
The JIT can further optimize code based on how it’s used, making repeated operations even faster.

### Key points:

-   JIT compilation happens while the program runs, not before.
-   It combines the flexibility of interpretation with the speed of compiled code.
-   This is why JavaScript (and other languages using JIT) can run quickly, even though it’s not compiled ahead of time.

### Analogy:
Think of a chef who first follows a recipe step by step (interpreting), but after making the dish several times, memorizes and streamlines the process (compiling and optimizing).

Let me know if you want a deeper technical example!

```js
const dataArray = [
    { id: 1, name: "Alpha", value: Math.random() * 100 },
    { id: 2, name: "Bravo", value: Math.random() * 100 },
    { id: 3, name: "Charlie", value: Math.random() * 100 },
    { id: 4, name: "Delta", value: Math.random() * 100 },
    { id: 5, name: "Echo", value: Math.random() * 100 },
    { id: 6, name: "Foxtrot", value: Math.random() * 100 },
    { id: 7, name: "Golf", value: Math.random() * 100 },
    { id: 8, name: "Hotel", value: Math.random() * 100 },
    { id: 9, name: "India", value: Math.random() * 100 },
    { id: 10, name: "Juliet", value: Math.random() * 100 }
];
```

```js
var newMsg = {}
var myArray = msg.payload.listDiagnosisIdentificationWithTimestamp
newMsg.payload = "Pending diagnostics:<br>"
for (let index = 0; index < (myArray.length -1); ++index) {
    newMsg.payload += index + ": " 
    + myArray[index].diagnosisIdentification.mainDiagnosisNumber 
    + ", " + myArray[index].diagnosisIdentification.detailedDiagnosisNumber 
    + ", " + myArray[index].diagnosisIdentification.entity + ";<br>"
}
return newMsg;
```

```js
const names = ["Alpha", "Bravo", "Charlie", "Delta", "Echo", "Foxtrot", "Golf", "Hotel", "India", "Juliet"];
const dataArray = [];
for (let i = 0; i < names.length; i++) {
    dataArray.push({
        id: i + 1,
        name: names[i],
        value: Math.random() * 100
    });
}
```

## Example of pending diagnostics

```js
var newMsg = {}
var myArray = msg.payload.listDiagnosisIdentificationWithTimestamp
var newDiagArray = [];

for (let index = 0; index < (myArray.length -1); ++index) {
    newDiagArray.push({
        TimeStamp: myArray[index].timestamp,
        MainDiagNumber: myArray[index].diagnosisIdentification.mainDiagnosisNumber,
        DetailledDiagNumber: myArray[index].diagnosisIdentification.detailedDiagnosisNumber,
        Entity: myArray[index].diagnosisIdentification.entity
    });
}

newMsg.payload = newDiagArray;

return newMsg;
```

```
var position = msg.payload;

msg.payload = {Action:"Z axis message",value:position};
return msg;

```
# Launch.json

```json showLineNumbers
// pehle referesh kro debugger ko then check kro break point red hi hain na or
//  botton status bar orange hojae to api call kro postman se phr break point work karnge
// make shure you have app.js file opened
// f5 se next break point pe jata hy
// f10 se line by line chalta hy inner procress ignore krta hy
// f11 se line by line bhe jata hy or ander tk bhe jata hy process se bhe

{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach",
      "port": 9229,
      "restart": true,
      "sourceMaps": true,
      "protocol": "inspector"
    }
  ]
}

// Skip to content
// Using NextGenINet Mail with screen readers

// 1 of 148
// Nodejs debugging launch.json file

// moiz
// 2:12 AM (8 hours ago)
// to me

// {
//   // Use IntelliSense to learn about possible attributes.
//   // Hover to view descriptions of existing attributes.
//   // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
//   "version": "0.2.0",
//   "configurations": [
//     {
//       "name": "Launch app.js via nodemon",
//       "type": "node",
//       "request": "launch",
//       // "runtimeExecutable": "nodemon",
//       "program": "${workspaceFolder}/app.js",
//       "restart": true,
//       "console": "integratedTerminal",
//       "internalConsoleOptions": "neverOpen"
//     },
//     {
//       "type": "node",
//       "request": "launch",
//       "name": "Launch Program",
//       "program": "${workspaceFolder}/app.js"
//     }
//   ]
// }

// selected this file as config and change index.js to app.jsLaunch index.js via nodemon

// {
//   // Use IntelliSense to learn about possible attributes.
//   // Hover to view descriptions of existing attributes.
//   // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
//   "version": "0.2.0",
//   "configurations": [
//     {
//       "type": "node",
//       "request": "launch",
//       "name": "nodemon",
//       "runtimeExecutable": "nodemon",
//       "program": "${workspaceFolder}/app.js",
//       "restart": true,
//       "console": "integratedTerminal",
//       "internalConsoleOptions": "neverOpen",
//       "skipFiles": ["<node_internals>/**"]
//     },
//     {
//       "type": "node",
//       "request": "launch",
//       "name": "Launch Program",
//       "skipFiles": ["<node_internals>/**"],
//       "program": "${workspaceFolder}/app.js"
//     }
//   ]
// }
```

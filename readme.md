# csgo-mirv_pgl

This is a package for [HLAE mirv_pgl](https://www.advancedfx.org/download/)
that parses the data from the mirv_pgl plugin and returns it as a JSON object.

## Installation

Prerequisites:
- [HLAE](https://www.advancedfx.org/download/)

```bash
npm install csgo-mirv-pgl
```
or
```bash
yarn add csgo-mirv-pgl
```

## Usage

```js
const {parseMIRV} = require('csgo-mirv-pgl');
const ws = require('ws');
const http = require('http');

const server = http.createServer();
const wss = new ws.Server({ server, path: '/mirv_pgl' });

wss.on('connection', (ws) => {
  console.log('Client connected');
  ws.on('message', (data)=> {
    const parsedData = parseMIRV(data);
    console.log(parsedData);
  });
});

server.listen(3000, () => {
  console.log('Server started onPort 3000');
});

```

### Sending console commands to cs:go

```js
const{ mirvPgl, sendCommand} = require('csgo-mirv-pgl');
const ws = require('ws');
const http = require('http');

const server = http.createServer();
const wss = new ws.Server({ server, path: '/mirv_pgl' });

wss.on('connection', (ws) => {
  console.log('Client connected');
  ws.on('message', (data)=> {
    const parsedData = parseMIRV(data);
    if(parsedData.name === 'hello'){
        // the function sendCommand takes the websocket and the command as a string
        sendCommand(ws,'echo "connected to websocket"');
        // It should send the command to the console of cs:go
    }
  });
});

server.listen(3000, () => {
  console.log('Server started onPort 3000');
});

```


## License
MIT


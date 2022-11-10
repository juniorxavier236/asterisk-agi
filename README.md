# asterisk-agi



node.js lib for Fast AGI (Asterisk Gateway Interface) server

[Fork of node-agi](http://github.com/brianc/node-agi)


Use asterisk-agi
=============


## Install

```
npm install asterisk-agi

```

`````javascript

const AGIServer = require('asterisk-agi');

const handler = (context) => {
    context.onEvent('variables')
        .then((vars) => {
            return context.streamFile('beep');
        })
        .then((result) => {
            return context.setVariable('RECOGNITION_RESULT', 'I\'m your father, Luc');
        })
        .then((result) => {
            return context.close();
        });
};

var agi = new AGIServer(handler, {port: 3000});
agi.init();

`````

### Add to Asterisk extensions.conf

`````
[default]
exten = > 1000,1,AGI(agi://localhost:3000)
`````

## API 

see [API.md](API.md)


## Links

[Asterisk AGI](https://wiki.asterisk.org/wiki/display/AST/Asterisk+13+AGI+Commands)
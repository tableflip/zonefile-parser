# zonefile-parser

A DNS zonefile parser module with no runtime dependencies, generated from the [PEG.js](https://github.com/pegjs/pegjs) grammar https://github.com/tableflip/zonefile-pegjs

Handles **multi-line SOA and TXT records**, as well as **SRV, MX, CNAME, NS, AAAA, A** and friends.

## Install

```sh
npm install zonefile-parser
```

## Usage

The parser comes in two flavors:

 **fast.js**, the default module exported:

```js
var parser = require('zonefile-parser')
parser.parse('tableflip.io. 21599 IN A 178.62.82.182')
// { origin: null, ttl: null, records:[ { name:'tableflip.io.', ttl: '21599', type:'A', data: '178.62.82.182' } ] }
```

and **small.js** in case you're browserifying and want to shave a few bytes:

```js
var parser = require('zonefile-parser/small')
parser.parse('tableflip.io. 21599 IN A 178.62.82.182')
// { origin: null, ttl: null, records:[ { name:'tableflip.io.', ttl: '21599', type:'A', data: '178.62.82.182' } ] }
```

## Command line tool

Install it globally

 ```sh
 npm install -g zonefile-parser
 ```

and use it from your shell as `zonefile` to convert a zonefile to JSON on stdout:

```sh
$ zonefile ../zonefile-pegjs/test/example.zone
{
  "origin": "example.org.",
  "ttl": "2d",
  "records": [
    {
      "name": "@",
      "ttl": null,
      "type": "SOA",
      "data": {
        "nameServer": "ns1.example.org.",
        "email": "hostmaster.example.org.",
        "serial": "2003080800",
        "refresh": "12h",
        "retry": "15m",
        "expiry": "3w",
        "minimum": "3h"
      }
    }
  ]
}
```

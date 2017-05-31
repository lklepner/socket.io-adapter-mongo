# socket.io-adapter-mongo

[![Build Status](https://secure.travis-ci.org/modit/socket.io-adapter-mongo.png)](http://travis-ci.org/modit/socket.io-adapter-mongo)
[![NPM version](https://badge.fury.io/js/socket.io-adapter-mongo.png)](http://badge.fury.io/js/socket.io-adapter-mongo)

*This module is modified from [socket.io-redis](https://github.com/Automattic/socket.io-redis)

Update 5/31/2017 - Versions prior to 1.0 allowed an object to be passed which was used to build a URI. This caused problems when using replica sets and caused warnings when MongoDB change the client API. In the interest of simplicity and futureproofing the internal URI construction has been eliminated and it is now required that a valid mongo URI be passed.

## How to use

```js
var io = require('socket.io')(3000);
var mongoAdapter = require('socket.io-adapter-mongo');
io.adapter(mongoAdapter( 'mongodb://localhost:27017' ));
```

By running socket.io with the `socket.io-adapter-mongo` adapter you can run
multiple socket.io instances in different processes or servers that can
all broadcast and emit events to and from each other.


## API

### adapter(uri[, opts])

`uri` is a string that matches a mongodb connection string
```
mongodb://localhost:27017/test
mongodb://user:pass@localhost:27017/test
mongodb://user:pass@host1:27017,host2:27017,host3:27017/test
```

### adapter(opts)

The following options are allowed:

- `key`: the name of the key to pub/sub events on as prefix (`socket.io`)
- `socket`: unix domain socket to connect to mongo (`"/tmp/mongo.sock"`). Will
  be used instead of the mongo URI if specified.
- `client`: optional, the mubsub client to publish events on

If you decide to supply a client, make sure you use [mubsub](https://github.com/scttnlsn/mubsub) as a client or one with an equivalent API.

## License

MIT

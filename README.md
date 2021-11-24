# SOCKETIO

Provides a form-fit-functional replacement for the notoriously buggy [socket.io](https://www.npmjs.com/package/socket.io) 
and its [socket.io-client](https://www.npmjs.com/package/socket.io-client) client counterpart.  Like its socket.io predecessors, 
**SocketIO** provides json-based web sockets, though it also has hooks to support binary sockets (for VoIP, video, etc) applications.
**SocketIO** provides both a server-side and client-side modules that mimic the [socket.io](https://socket.io/docs/v3/client-initialization/)
specification (less the bugs of course).

## Server side usage

On the server:

	const SIO = require("socketio");
	
	IO = SIO(server);					// connects socketIO to your nodejs server
	
	IO.on( "connect", socket => {		// the client automatically emits a "connect" request when it calls io()  
	
		socket.on(  "CHANNEL", (req,socket) => {			// intercepts client request made on socket to this CHANNEL
			console.log( "here is the client's request", req ); 
			socket.emit({ message: "a response" });
			IO.emit({ message: "a message for everyone!" });
			IO.emitOthers("SkipThisClient", { message: "a message for everyone!" });		// useful emit extension
			IO.clients["someone@totem.org"].emit({ message: "you get an extra message"});
		});
		
		/* etc for other CHANNELs */
		
	});
	
	IO.emit({ .... })  			// to emit a request to all clients

## Client side usage

On the client-side:

	<script type="text/javascript, src="/socketio/socketio-client.js"></script>

	const
		ioSocket = io();			// connect to socketIO by emitting a "connect" request
		ioClient = "myClientName"

	ioSocket.emit("CHANNEL", {		// send request to server side on its CHANNEL
		...
	});
	
	ioSocket.on("CHANNEL", req => {
		console.log("server sent this request", req);
	});
	
## Installation

Clone **SOCKETIO** from one of its repos:

	git clone https://github.com/totemstan/socketio
	git clone https://sc.appdev.proj.coe/acmesds/socketio
	git clone https://gitlab.west.nga.ic.gov/acmesds/socketio

## Modules

<dl>
<dt><a href="#module_SOCKETIO">SOCKETIO</a></dt>
<dd><p>Replaces the buggy socket.io and socket.io-client modules.
Documented in accordance with <a href="https://jsdoc.app/">jsdoc</a>.</p>
<p>ref: <a href="https://medium.com/hackernoon/implementing-a-websocket-server-with-node-js-d9b78ec5ffa8">https://medium.com/hackernoon/implementing-a-websocket-server-with-node-js-d9b78ec5ffa8</a></p>
</dd>
<dt><a href="#module_SOCKETIO-CLIENT">SOCKETIO-CLIENT</a></dt>
<dd><p>Replaces the buggy socket.io and socket.io-client modules.</p>
</dd>
</dl>

<a name="module_SOCKETIO"></a>

## SOCKETIO
Replaces the buggy socket.io and socket.io-client modules.
Documented in accordance with [jsdoc](https://jsdoc.app/).

ref: https://medium.com/hackernoon/implementing-a-websocket-server-with-node-js-d9b78ec5ffa8

**Requires**: <code>module:CRYPTO</code>  
<a name="module_SOCKETIO-CLIENT"></a>

## SOCKETIO-CLIENT
Replaces the buggy socket.io and socket.io-client modules.


## Contacting, Contributing, Following

Feel free to 
* submit and status **TOTEM** issues (
[WWW](http://totem.zapto.org/issues.view) 
[COE](https://totem.west.ile.nga.ic.gov/issues.view) 
[SBU](https://totem.nga.mil/issues.view)
)  
* contribute to **TOTEM** notebooks (
[WWW](http://totem.zapto.org/shares/notebooks/) 
[COE](https://totem.west.ile.nga.ic.gov/shares/notebooks/) 
[SBU](https://totem.nga.mil/shares/notebooks/)
)  
* revise **TOTEM** requirements (
[WWW](http://totem.zapto.org/reqts.view) 
[COE](https://totem.west.ile.nga.ic.gov/reqts.view) 
[SBU](https://totem.nga.mil/reqts.view), 
)  
* browse **TOTEM** holdings (
[WWW](http://totem.zapto.org/) 
[COE](https://totem.west.ile.nga.ic.gov/) 
[SBU](https://totem.nga.mil/)
)  
* or follow **TOTEM** milestones (
[WWW](http://totem.zapto.org/milestones.view) 
[COE](https://totem.west.ile.nga.ic.gov/milestones.view) 
[SBU](https://totem.nga.mil/milestones.view)
).

## License

[MIT](LICENSE)

* * *

&copy; 2012 ACMESDS

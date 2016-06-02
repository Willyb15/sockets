### Small Application Built with socket.io in Node.js 
####Created two files - index.htl and server.js
####In html used socket cdn
```html
<script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
```
####Dowload socket.io from npm to get node modules folder.
```
npm install socket.io
nodemon server.js   

```
###This is the server.js file
```js
var http = require('http');
var fs = require('fs');
var server = http.createServer(function(req, res){
	fs.readFile('index.html', "utf-8", function(err, data){
		res.writeHead(200,{'content-type': 'text/html'});
		res.write(data);
		res.end();
	});

});

var io = require('socket.io').listen(server);
io.sockets.on('connect', function(socket){
	console.log(socket);
	socket.on('message_to_server', function(data){
		io.sockets.emit('message_to_client',{message: data.message});
		console.log(data.message);
	});

});

server.listen(8000);
console.log("Listening on port 8000, suckit");
```

this is the html
```html
<!DOCTYPE html>
<html>
<head>
	<title>Socket IO</title>
	<script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>

	<script type="text/javascript">
		console.log(io.connect);
		var socketio = io.connect('http://127.0.0.1:8000');
		socketio.on('message_to_client', function(data){
			document.write(data.message);
		});
		
		function sendMessage(){
			var userMessage = document.getElementById('message').value;
			socketio.emit('message_to_server',{
			message: userMessage
			});
			event.preventDefault();
		}
	</script>

</head>
<body>
	<h1> This is the index file Bitch!!</h1>

	<div id="chat-wondow"></div>
	<form onsubmit="sendMessage()">
		<input type="text" id="message" placeholder="Type your message here">
		<input type="submit">
	</form>
	
</body>
</html>
```

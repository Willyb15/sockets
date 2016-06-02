### Small Application Built with socket.io in Node.js 


this is the html
```

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

# phpwebsocket
Automatically exported from http://code.google.com/p/phpwebsocket

**I don't take any credit for the code.**


**PHP and WebSockets**

**Changelog**

010.02.16 - Added basic demo and chatbot

010.02.16 - Added users list to keep track of handshakes

010.02.16 - Organized everything in a reusable websocket class

010.02.16 - Minor cosmetic changes

**Client side**
```php
var host = "ws://localhost:12345/websocket/server.php";
try{
  socket = new WebSocket(host);
  log('WebSocket - status '+socket.readyState);
  socket.onopen    = function(msg){ log("Welcome - status "+this.readyState); };
  socket.onmessage = function(msg){ log("Received: "+msg.data); };
  socket.onclose   = function(msg){ log("Disconnected - status "+this.readyState); };
}
catch(ex){ log(ex); }
```


**Server side**
```php
log("Handshaking...");
list($resource,$host,$origin) = getheaders($buffer);
$upgrade = "HTTP/1.1 101 Web Socket Protocol Handshake\r\n" .
           "Upgrade: WebSocket\r\n" .
           "Connection: Upgrade\r\n" .
           "WebSocket-Origin: " . $origin . "\r\n" .
           "WebSocket-Location: ws://" . $host . $resource . "\r\n" .
           "\r\n";
$handshake = true;
socket_write($socket,$upgrade.chr(0),strlen($upgrade.chr(0)));
```

**Steps to run the test:**

Save both files, client.php and server.php, in a folder in your local server running Apache and PHP.

From the command line, run the server.php program to listen for socket connections.

Open Google Chrome (dev build) and point to the client.php page

Done, your browser now has a full-duplex channel with the server.

Start sending commands to the server to get some responses.

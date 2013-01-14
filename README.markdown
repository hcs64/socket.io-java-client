[![Flattr this git repo](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=Gottox&url=https://github.com/Gottox/socket.io-java-client&title=socket.io-java-client&language=&tags=github&category=software)

# Socket.IO-Client for Java

socket.io-java-client is an easy to use implementation of [socket.io](http://socket.io) for Java.

Forked to rely on only an improved XHR-Transport, seems to work ok but not heavily tested.

The API is inspired by [java-socket.io.client](https://github.com/benkay/java-socket.io.client).

__Status:__ XHR is in beta.


## How to use

Using socket.io-java-client is quite simple. But lets see:

Checkout and compile the project:

``` bash
git clone git://github.com/Gottox/socket.io-java-client.git
cd socket.io-java-client
ant jar
mv jar/socketio.jar /path/to/your/libs/project
```

If you're using ant, change your build.xml to include socketio.jar. If you're eclipse, add the jar to your project buildpath.

Afterwards, you'll be able to use this library: 

``` java

		SocketIO socket = new SocketIO("http://127.0.0.1:3001/");
		socket.connect(new IOCallback() {
			@Override
			public void onMessage(JSONObject json, IOAcknowledge ack) {
				try {
					System.out.println("Server said:" + json.toString(2));
				} catch (JSONException e) {
					e.printStackTrace();
				}
			}

			@Override
			public void onMessage(String data, IOAcknowledge ack) {
				System.out.println("Server said: " + data);
			}

			@Override
			public void onError(SocketIOException socketIOException) {
				System.out.println("an Error occured");
				socketIOException.printStackTrace();
			}

			@Override
			public void onDisconnect() {
				System.out.println("Connection terminated.");
			}

			@Override
			public void onConnect() {
				System.out.println("Connection established");
			}

			@Override
			public void on(String event, IOAcknowledge ack, Object... args) {
				System.out.println("Server triggered event '" + event + "'");
			}
		});
		
		// This line is cached until the connection is establisched.
		socket.send("Hello Server!");

```

For further informations, read the [Javadoc](http://s01.de/hgexport/socket.io-java-client/).

 * [Class SocketIO](http://s01.de/~tox/socket.io-java-client/io/socket/SocketIO.html)
 * [Interface IOCallback](http://s01.de/~tox/socket.io-java-client/io/socket/IOCallback.html)
 
## Building

to build a jar-file:

	cd $PATH_TO_SOCKETIO_JAVA
	ant jar
	ls jar/socketio.jar

You'll find the socket.io-jar in jar/socketio.jar 

## Frameworks

This Library was designed with portability in mind.

* __Android__ is fully supported.
* __JRE__ is fully supported.
* __GWT__ does not work at the moment, but a port would be possible.
* __Java ME__ does not work at the moment, but a port would be possible.
* ... is there anything else out there?

## Testing

There comes a JUnit test suite with socket.io-java-client. Currently it's tested with Eclipse.

You need node installed in PATH.

 * open the project with eclipse
 * open tests/io.socket/AllTests.java
 * run it as JUnit4 test.

## TODO

* Socket.io needs more unit-tests.
* XhrTransport needs to pass all tests.
* If websockets are failing (due to proxy servers e.g.), use XHR automaticly instead.

## License - the boring stuff...

This library is distributed under MIT Licence.


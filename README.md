# mesh-chat
Chat protocol for secure communication over a mesh network over the internet.


## Clients

[Spiced Gracken](https://github.com/NullVoxPopuli/spiced_gracken) (ruby gem)  
[Pyna Collada](https://github.com/etkirsch/pyna-collada) (python)

## Internal Protocol
Each message will be a serialized (to JSON) hash.
Every hash must include:

    {
      type: <MessageClassName>, # This will tell each client how to read the rest of the keys
      client: <String>, # name of the client that sent the message
      client_version: <String>, # version of the client that sent the message
      sender: {
        name: <String>,
        location: <IpAddress>,
        time_connected: <Time> # Time connected to the mesh network
      },
      message: <Indeterminant> # Variable type, can be string or json object (see below)
    }

A recieving client deserializes the JSONized hash, and can do whatever with it.

#### Message
The `message` field in the hash is of variable type. Its type is determined by the `type` field as follows.

 * **chat**: A string containing the message body
 * **whisper**: A string containing the message body
 * **connect**: A json object containing the identifier for the connecting party and a hash of all of its authorized servers
 * **disconnect**: Unused
 * **authorization**: Milestone 2

## Message Types
There are various types of messages used by Rum. They each have various functionalities as described below.

* **chat**: A message broadcast to all of a client's active servers
* **whisper**: A message broadcast to a single active server, e.g. `@evan hello`
* **connect**: Informs all authorized servers that this client/server pair has come online
* **disconnect**: Informs all active servers that this client has gone offline
* **authorization**: Milestone 2

## Responsibility Breakdown
The client is responsible for sending all messages to servers. It is only permitted to send messages on its own behalf, and not for any other party. It will keep track of the active list of authorized servers.

The server is responsible for configuration of authorized servers and handling of all message receipts. When a message arrives, it is then relayed to the local client for display. In Milestone 2, the server will also handle authorization and server exchange.

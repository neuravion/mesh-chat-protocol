# mesh-chat

[![Join the chat at https://gitter.im/neuravion/mesh-chat](https://badges.gitter.im/neuravion/mesh-chat.svg)](https://gitter.im/neuravion/mesh-chat?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
Chat protocol for secure communication over a mesh network over the internet.

#### Topics / Reference
[Routing Across the Mesh Network](routing-across-the-meshnet.md)  
[Message Types](message-types.md)  
[Server/Node List Sync](server-list-sync.md)  
[Require Commands](required-commands.md)  

## Recognized `mesh-chat` Clients
Clients have been built in multiple languages. Interpretations between these clients are very unique, but the `mesh-chat` protocol is always consistent.

* [PyÑa Colada v0.9.0](https://github.com/etkirsch/pyna-colada) (Python 3.4)  
* [Spiced Rumby](https://github.com/NullVoxPopuli/spiced_rumby) (Ruby 2.3), based on [MeshChat Core](https://github.com/NullVoxPopuli/meshchat) (Ruby 2.3)

## Planned `mesh-chat` Clients
* [Otra Vez Gose](https://github.com/etkirsch/otra-vez) (Go 1.6.2)
* [Untitled NodeJS client](https://github.com/ecollis6/mesh-chat-node) (NodeJS)
* [Emberclear](https://github.com/nullvoxpopuli/emberclear) (Ember 2.5)

## `mesh-chat` Relay
There is currently only one server-side relay. All clients can connect to this server. Many instances of this server across the internet are vital to the survival of a mesh-network and allow p2p communication across the globe.

* [mesh-relay](https://github.com/NullVoxPopuli/mesh-relay) (Ruby on Rails 5)

### Responsibility Breakdown
The client is responsible for sending all messages to servers. It is only permitted to send messages on its own behalf, and not for any other party. It will keep track of the active list of authorized servers.

The server is responsible for configuration of authorized servers and handling of all message receipts. When a message arrives, it is then relayed to the local client for display. In Milestone 2, the server will also handle authorization and server exchange.


## Mesh-Chat Protocol
Each message will be a serialized JSON hash.
Every hash must include:

    {
      type: <MessageClassName>, # This will tell each client how to read the rest of the keys
      client: <String>, # name of the client that sent the message
      client_version: <String>, # version of the client that sent the message
      time_sent: <UTC DateTime String>, # time at the packaging of this message
      sender: {
        name: <String>,
        location: <IpAddress>,
        uid: <String> # Uinque ID generated by your client
      },
      message: <Indeterminant> # Variable type, can be string or json object (see below)
    }

A receiving client deserializes the JSONized hash, and can do whatever with it.


## Encryption
`mesh-chat` applications should use the NaCl library's public key encryption algorithms. Nodes which are new to the system must generate a public/private key pair, and have imported one other node's identity before it can begin participating in the mesh network.

Note that NaCl is an opinionated crytography library whos public key encryption consists of

Encryption: XSalsa20 stream cipher
Authentication: Poly1305 MAC
Public Keys: Curve25519 high-speed elliptic curve cryptography

See the [RbNaCl public key encryption](https://github.com/cryptosphere/rbnacl/wiki/Public-Key-Encryption) overview for details, explanation and usage.

- [More Information on NaCl](http://nacl.cr.yp.to/)
- [C Implementation](https://github.com/jedisct1/libsodium)
- [Ruby Bindings](https://github.com/cryptosphere/rbnacl)

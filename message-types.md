# Message Types

### Message Types
There are various types of messages used in mesh-chat applications. They each have various functionalities as described below.

* **chat**: A message broadcast to all of a client's active servers
* **emote**: A specialized chat message which is broadcasted to all of a client's active servers
* **whisper**: A message broadcast to a single active server, e.g. `@evan hello`
* **disconnect**: Informs all active servers that this client has gone offline
* **nodelisthash**: Used to check for discrepancies in node lists between one node and another
* **nodelist**: Used to send a full server list from one node to another; occurs in one of two circumstances...
  * The node received a nodelisthash message which contains a differing hash
  * The node is importing a new node into the mesh network
* **nodelistdiff**: Response to `nodelist` type message, sends all servers unique to a node not contained in the `nodelist` message
* **ping**: Used to ask a user for an update of their basic information (alias, location, uid)
* **pingreply**: A response to a ping

#### Message Field Contents
The `message` field in the hash is of variable type. Its type is determined by the `type` field as follows.

 * **chat**: A string containing the message body
 * **whisper**: A string containing the message body
 * **nodelisthash**: A hash for checking for differences in nodelists between a connecting node and a connected node. This hash must be in SHA512 format
 * **disconnect**: If the sender of this message is manually disconnecting, the message field is empty. Otherwise, it contains the uid of the user which has disconnected but not yet notified other nodes
 * **nodelist**: Contains the full server list from an authorized node
 * **nodelistdiff**: Contains a truncated server list with only unique entities from a connected node to a connecting node
 * **pingreply**: Contains all optimal routes used by a pinged server; the updated alias/location/uid are inferred based on the `sender` field

#### Node List Entry
An entry in the `nodelist` and `nodelistdiff` messages must follow the following format:

```
{
    "alias": <string>, # The user's current alias (transient)
    "location": <string>:<num>, # the user's current ip address and port (transient)
    "uid": <string>, # the user's identifier (static)
    "publickey": <string> # This user's public key (RSA? undecided at the moment) (static)
}
```

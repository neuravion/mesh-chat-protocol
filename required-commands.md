#Required Commands

 - `/who` - lists all active (or known to be active) users
 - `/servers` - lists all active (or known to be active) servers
 - `@<user-alias>` - sends a whisper (only <user-alias> can see the message)
 - `/quit` or `/exit` - quits the chat client
 - `/listen` - starts listening for incoming connections / messages
 - `/stoplistening` - stops listening for incoming connections / messages
 
# Application-Optional Commands
 - `/@<user-alias>` - drops out of all chat and the following messages can only be seen by <user-alias>
 - `/all` - drops out of whisper mode, and back in to all chat.
 
###PyÑa Colada Command Correlates
Syntactically, PyÑa Colada v0.1.5's commands are a bit different. The differences are as follows.

# Variations

##### Implemented as of PyÑa Colada v0.1.5
 - `/who` - as above
 - `/servers` - as above
 - `@<user-alias>` - `/w <user-alias>`
 - `/quit` or `exit` - `/x`
 - `/listen` - automatic

##### Not Implemented as of PyÑa Colada v0.1.5
 - `/stoplistening`
 - `/@<user-alias>`
 - `/all`

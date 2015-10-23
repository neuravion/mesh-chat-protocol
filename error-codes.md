# Error Codes
When sending and receiving within the mesh-chat mesh network, clients must use specific HTTP status codes.

* **100 Continue** - As necessary (usually automated)
* **200 OK** - When a message has been received appropriately from one source
* **400 Bad Request** - When a node receives a POST but cannot decrypt the message or it was in plaintext
* **403 Forbidden** - When a node can encrypt for another appropriately, but the recipient does not recognize the sender

# Wrapping in HTTP
HTTP provides ease of message frame handling (only receiving X number of bits at a time) and frame order.
It also allows us to send files if we so choose.

Each node should have an HTTP server that listens for incoming messages.

All messages sending data should use the `POST` action.
For example, a `ping` would use `GET`, but `chat` or `nodelist` would use `POST`. 


An example request could look something like this

```bash
curl -H "Content-Type: application/json" \
     -X POST \
     -d '{"message":"encrypted message"}' \
     http://ip.or.address:3000
```

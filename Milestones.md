#Milestones
### Milestone 2: Serverlist Exchange
* Send `nodelisthash` using SHA512 Hash exchange
```
  sha512.value = 'publickey1,publickey2,publickey3,...,publickeyn'
```
* If received `nodelisthash` differs, send full node list back to sender
```
  [{alias1,address1,uid1,publickey1},{alias2,address2,uid2,publickey2},etc.]
```
* Receiver of full node list diffs the incoming list and sends all not in the intersection (`nodelistdiff` message)
```
  [{alias1,address1,uid1,publickey1},{alias2,address2,uid2,publickey2},etc.]
```

### Milestone 3: Auth
* Uses dual RSA (PKCS1 v1.5) and AES-256 (CBC)
* Client is responsible for creating and maintaining keys
* Public Keys need to be imported manually for insertion into the mesh network, after which they are exchanged using `nodelist`

### Milestone 4: Relays
* See `Relay Strategies`

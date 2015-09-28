#Milestones 
### Milestone 2: Serverlist Exchange
* Send `serverlisthash` using SHA512 Hash exchange
```
  sha512.value = 'publickey1,publickey2,publickey3,...,publickeyn'
```
* If received `serverlisthash` differs, send jsonized full server list back to hash sender (`serverlist` message)
```
  {"servers": [{alias1,address1,uid1,publickey1},{alias2,address2,uid2,publickey2},etc.]}
```
* Receiver of full server list diffs the incoming list and sends all not in the intersection (`serverlistdiff` message)
```
  {"servers": [{alias1,address1,uid1,publickey1},{alias2,address2,uid2,publickey2},etc.]}
```

### Milestone 3: Auth
* Uses RSA
* Need process for creating pub/priv keys
* Need an easy way to create a keyfile and have another client import that file

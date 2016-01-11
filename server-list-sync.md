![Server List Sync](http://www.websequencediagrams.com/cgi-bin/cdraw?lz=U2VydmVyIExpc3QgU3luYwoKQ2xpZW50QS0-AAIHOiBBZGQgABAGQidzIGluZm8gKGlwLCBhbGlhcywgdXVpZCwgcHVibGljIGtleSkAMxFCOiBDaGF0IE1lc3NhZ2UAXAdCABQLAFkKQSB0byB0aGUgbGlzdCBvZiBhY3RpdmUgcwCBJAVzACwQQTogU2VuZAAYBwAvBmhhc2ggKHNoYSwgZXRjKQCBPxNVcGRhdGVzAIFLCwCBRwUKCm9wdAA6EWVzIGRpZmZlcgogICAAgR4IAIFQCwB7BWZ1bGwAeQwAIQsAgVwMRGlmZnMACCAAgU0HABsNAH4FIHRvAIIeCAplbmQK&s=default)

https://www.websequencediagrams.com/
```
Server List Sync

ClientA->ClientA: Add ClientB's info (ip, alias, uuid, public key)

ClientA->ClientB: Chat Message
ClientB->ClientB: Add ClientA to the list of active servers
ClientB->ClientA: Send server list hash (sha, etc)
ClientA->ClientA: Updates ClientB's alias

opt server list hashes differ
    ClientA->ClientB: Send full server list
    ClientB->ClientB: Diffs server list
    ClientB->ClientA: Sends server list diff to ClientA
end
```


### Format

The format for each of the sync messages' payloads are as follows:

#### nodelist

This should be a list of all known nodes

```
[
  { "alias": "etk", "location": "10.10...", "uid": "abcd...", "publickey"  },
  { "alias": "nvp", "location": "10.10...", "uid": "abcd...", "publickey"  },
  { "alias": "someotherguy", "location": "10.10...", "uid": "abcd...", "publickey"  }
  ...
]
```

#### nodelistdiff

After receiving a node list, this should be the list of nodes that are not included in the list received

```
[
  { "alias": "anotherbro", "location": "10.10...", "uid": "abcd...", "publickey"  }
  ...
]
```

#### nodelisthash

This should be all your nodes hashed with `SHA-512`

```
suaoehtiud0aoe89u6an4gchiypnsoe98uaoefnucgude...
```

## Common Mistakes

- Infinite loop of node list sending
  -  Likely that the node list hashes are never the same
    -  This could be due to formatting differences in the singular json representation of a node
    -  The nodes could be in a different order
    -  The nodes might not be diffed and added correctly upon receiving

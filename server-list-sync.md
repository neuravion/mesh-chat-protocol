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

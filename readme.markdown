# post-cyberpunk webapps

substack
James Halliday

Oakland, California

---
# cyberpunk

society is saturated with technology

---
# cyberpunk

society is saturated with technology

* expansive worldwide communications
* a supercomputer in your pocket
* access your data anywhere

---
# cyberpunk

society is saturated with technology

* expansive worldwide total surveillance
* your supercomputer is useless without a data plan
* marketers are combing through your data

http://tvtropes.org/pmwiki/pmwiki.php/Main/CyberpunkTropes

---
# cyberpunk

society is saturated with technology

(aka today)

---
# post-cyberpunk

a more balanced relationship with technology

(aka the future)

---
and what we can do about it!

* replication
* offline architecture
* authentication
* peer connections

---
# replication

Everyone gets a copy of the data they can edit.

---
## content-addressable data

key = hash(value)

---
## blob storage

https://github.com/maxogden/abstract-blob-store

* .createWriteStream()
* .createReadStream()
* .exists()
* .remove()

---
## demo: content-addressable-blob-store

node demo!

---
## demo: idb-content-addressable-blob-store

browser demo!

---
## merkle DAG

each document points at its parent(s)

like git!

```
  A      A: 457292 => null, aaaaaaa
 / \     B: 97f90e => 45729, bbBbbB
B  C     C: 8e5638 => 45729, ccc
   /\    D: 431271 => 8e5638, ddDddD
  D  E   E: f6d81a => 8e5638, EE

HEADS: B, D, E
```

---
## heads

heads => all the documents not currently pointed at by any other documents

---
## indexes

we need some indexes to keep track of which data points where

---
## leveldb

* `db.get()`
* `db.put()`
* `db.del()`
* `db.batch()`
* `db.createReadStream()`

---
### demo: leveldb in node

DEMO

---
### demo: leveldb in the browser

DEMO

---
## replication

to replicate:

* exchange hash lists with the other node
* request the hashes you don't have
* concatenate the other node's data to your log

---
## symmetric protocols

p2p: no "server" and "client"

an easy way to implement: stdin and stdout

---
## dupsh

dupsh cmd1 cmd2

pipes cmd2's stdout to cmd1's stdin
pipes cmd1's stdout to cmd2's stdin

```
.-> cmd1 | cmd -.
|_______________|
```

---
## forkdb

ties everything together:

* content-addressable-blob-store
* merkle dags in leveldb
* replication

---
## demo: forkdb

demo!

---
## demo: forkdb in the browser

browser demo!

---
# authentication

Use asymmetric keypairs.

Save the private key on the client in indexedDB.

---
## naming

Your ID is the hash of your public key.

Your name is what your friends call you.

---
# peer architectures

peers connect to other peers
instead of a central server

---
## peer architectures

Nobody can own these services.

No computer is privleged.

---
## p2p faustian bargain

You get:

* fixed or no server cost
* low latency
* automatic free scaling

You give up:

* total observation (aka surveilance)
* exclusivity as a gatekeeper

---
## bittorrent

uses a Distributed Hash Table (dht) to peers with hashes

---
## bittorrent-dht

bittorrent's DHT algorithms implemented in pure javascript

---
## bittorrent-dht (BEP 44)

Adds `get()` and `put()` to the dht.

The key is the hash of a public keypair.
The value is cryptographically signed.

Nodes will forget messages after 2 hours.

---
## implementing twitter on BEP44

Save the hash of the most recent tweet with `put()`

Save each tweet into bittorrent like usual.

Each tweet points at the hash of the previous tweet.

---
## torrent-blob-store

* .createWriteStream()
* .createReadStream()

to publish and consume files from bittorrent!

---
## demo: torrent-blob-store

node demo!

---
## webrtc

p2p connections in the browser

* video
* audio
* data <-- the one that actually matters

---
## webtorrent

all of these bittorrent libs ALSO work in the browser over webrtc

using http://webtorrent.io

---
# immutable apps

In bittorrent, you hash a file and fetch files by their hash.

In the browser, the server sends you whatever it feels like.

---
## p2p application delivery

Just fetch HTML over webtorrent!

---
## p2p application release

```
$ html-inline app.html > bundle.html
$ torrent seed bundle.html
```

Distribute application infohashes to your BEP44-powered feed.

Good for security: the server can't send you arbitrary javascript to run
whenever it wants.

---
## webrtc peer signals

file:///home/substack/projects/peernet/example/wrtc/index.html#1

---
# peernet

random gossip algorithms for peer discovery and subnetting

store webrtc introductions on peernet?

---
# EOF

Hack the planet!


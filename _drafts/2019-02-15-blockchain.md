---
layout: post
title: "blockchain"
date: 2019-02-25 19:40:00 +0300
tags: drugs
---

2019 was supposed to be _the year_. Being 21 and thus necessarily unsure of what to do with my life, I, in a rare stroke of genius, decided to embark upon the unprecedented journey of learning the most popular technology.
I fired up my favorite browser: not-chrome, and er.. searched "Technologies to watch out for in 2019". And there it was. Among ML, AR/VR, IoT and other examples of poor naming conventions, was the odd tech out, blockchain.

The first few reads about any technology are (and should be) meant to kind of buy you into the idea. The 'how this new thing is cool' or 'why this new thing over the other old thing that your boss probably wants you to learn'. So I spent the next 2 hours reading _about_ blockchain. I then spent the next 3 days after that doing the exact same thing, without ever writing a single piece of code. And I am writing this post still, without having written a single piece of code. And here's why:

Blockchain is, without a doubt, the technology with the least understood-to-talked-about ratio. And while many have the basics all ironed out, the proverbial devil, it seems, has escaped the meat of so many a blockchain article with high search engine ratings that in turn perpetuate the general -ignorance- misunderstanding of this exciting subject. A misunderstanding that currently has me at its throes. All I have left now is more questions, less answers and consequently, no code.




Satoshi Nakamoto

https://www.youtube.com/watch?v=SSo_EIwHSd4:

is a distributed ledger, accessible to everybody
you can change a block - it's hash will change
each block has its hash and the hash of the previous block
genesis block - has no block of a previous block

recalculating hashes

p2p
proof of work
consensus
smart contracts
=============================
https://www.youtube.com/watch?v=3xGLc-zz9cA:

if a change is made to a block, the change is tracked by a new block

(non destructive ledger)

before a block is added:
- a cryptographic puzzle must be solved
- computer solving the puzzle must share the solution with all other computers in the network (proof of work)
- the network (all other comps) verify this proof of work
================================
https://www.youtube.com/watch?v=Pl8OlkkwRpc:
Don Tapscott

"it's not the most sonorous word in the world
"when i'm sending you a pdf via email, i'm sending you a copy of it, and that's fine, this is democratized information"

middlemen (e.g. banks)
-they exclude a lot of people from [the global economy] transactions (like ppl who don't have enough money to open bank accounts)
-they take a big piece of the action (huge cuts to send money and carry out transactions)
-they can be hacked (cause they're centralized)
-slow things down (time to move money through the banking system)
-capturing our data (we can't monetize or reuse it. undermining our privacy)
-they've appropriated the largesse of the digital age asymetrically (we have wealth creation and we have growing social inequality)

but the real pony here... is the underlying technology, blockchain

ethereum (smart contracts)
impact:
-create a new replacement for the stock market
-create a new model of democracy where politicians are accountable to citizens

Applications
"the first era of the internet: the internet of information brought us wealth but not shared prosperity because social inequality is growing" (anger, extremism, xenophobia, protectionism)
-Rather than redistribute wealth, pre-distribute it, democratize wealth creation
- land titles on a block chain (immutable records, protecting people's rights)
- rethinking remittance

"privacy is the foundation of a free society"

Imogen Heap - music on a blockchain
- rightful compensation for creators of content
=============================
https://www.youtube.com/watch?v=8fbhI1qVj0c

How blockchain can transform india
-agriculture: smart records, farm equipment owned by multiple people, managing land records, farming records, output
-electricity: in villages, centralized power stations don't work, you have to produce power where you need it. (donating power from excesses to deficients) (you still need grids to transmit the energy to your peers)
-frauds in 'chamas'
==============================
https://www.youtube.com/watch?v=hYip_Vuv8J0
Yes, and...

you have an emergency but your car won't open because you're two days behind payment. Simply put: an app won't let you save your life
"the barrier being a rigidity in the structures that don't accomodate real life scenerios well"
"we tend to hold novel technologies to an unrealistically high standard in terms of what they're supposed to deliver"
================================
https://www.youtube.com/watch?v=G3psxs3gyf8

-voting
-govt documents
-public benefits
-healthcare data
-music
-real estate
-crowd funding
-hiring (posting jobs, voting and awarding contracts)
-(data + transactions)

names:
aeternity
innogy
augur (prediction)
storj (cloud)
bitgive (donation)
ABRA - bitcoin-based remittance
consensys
govcoin
tierion
mycelia, ujo music

===================================================
https://www.investopedia.com/terms/b/blockchain.asp

a single block can house a few thousand transactions under one roof.

a blockchain can be hacked, but it would require access to every computer on the chain

Each wallet consists of two unique and distinct cryptographic keys: a public key and a private key. The public key is a shortened version of the private key. But it is hard (impossible) to decrypt, hence secure

==========
Wikipedia
1991 by Stuart Haber and W. Scott Stornetta

(Bayer, Haber and Stornetta in 1992) improved the design by includeing Merkle trees (or Hash trees) to allow several document certificates to be collected into one block

Ralph Merkle who patented Merkle trees in 1979

(Satoshi Nakamoto before 2008) improved the design using a Hashcash-like method to add blocks to the chain without requiring them to be signed by a trusted party.

Hashcash is a proof of work system proposed in 1997 by Adam Back

Proof-of-work concept was invented by Cynthia Dwork and Moni Naor in 1992

blockchain reached 'ealry adopters' phase in 2016

"Network effect" - is the effect that an additional user of a good or service has on the value of that product to others. When a network effect is present, the value of a product or service increases according to the number of others using it

private blockchains...
Nikolai Hampton in computer world
-private bc is centralized in a way such that if you control the central bc db, you already have control over the entire bc
-ther is also no incentive to discover blocks faster: "This means that many in-house blockchain solutions will be nothing more than cumbersome databases"

=====
NOTE

reads:
https://blockgeeks.com/guides/what-is-blockchain-technology/
https://www.instapaper.com/read/1163646225

-nodes are...? the computers adding blocks to the network?
-what is 'joining' the blockchain? simply acquiring a copy of the chain?
-where does one receive the challenge from? how does one access the proof of work/stake?
-does a blockchain need a 'heartbeat'? or can less-busy (private) blockchains be configured to a) require no proof work. yes and b) just add blocks whenever a transaction is posted?
-wallets... do you need one to access the chain. This wallet, how complex is it in terms of implementation?
-when i send a transaction via my wallet? who do i send it to? where does the wallet take it? how does it gets processed and added to a block?
-and, for chains with heartbeats, how does the timeline play through? is the proof of work/task directly corelated to the transaction data?
-so at what point (during the heartbeat) do the miners start solving the puzzle?
-"That hash is put, along with some other data, into the header of the proposed block. This header then becomes the basis for an exacting mathematical puzzle which involves using the hash function yet again. This puzzle can only be solved by trial and error"
-does a node know when it has solved the puzzle? or does it repeatedly query..the source? if the solution it has got is the right one?
-"When a miner finally comes up with a solution other nodes quickly check it (that’s the one-way street again: solving is hard but checking is easy)"
-how efficient is blockchain as a database?

Wallets:
cryptoart
cryptosteel
https://walletgenerator.net/
bitaddress.org

IoT and blockchain
freenet, p2p hosting
webtorrent, js torrent client (streaming service)
AML (anti money laundering) and KYC (know your customer) need to be implemented NOW in kenya as technology is just being adopted so as to ensure people and their data are built into the systems

Enigma uses cryptographic techniques to allow individual data sets to be split between nodes, and at the same time run bulk computations over the data group as a whole. Fragmenting the data also makes Enigma scalable (unlike those blockchain solutions where data gets replicated on every node).

startups
========
Vault platform - report and resolve misconduct on a distributed ledger (perks: anonymity, immutable timestamps)
DADI - decentralized arch for democratic internet, like freenet
Varius World Tech - gambling, random num gen, kyc, aml, ai to spot problematic customers, reward schemes for recreational custs
content licensing: kodak one, mycelium, jaak
medicalchain - medical records SingleSrcOfTruth
bitticket - ticket delivery service
Shivom - genomic big data, DNA database
TWO IoT - full wastebins
nugget e commerce, POS

-blockchain for curbing piracy:
https://navms.com/blockchain-may-be-the-missing-link-for-video-protection/
Vevue on qtum
Custostech - blockchain and forensic watermarking

white paper
predicative script
fiat currency



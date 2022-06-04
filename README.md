# NFT-Event-Tickets-Reservation-Blockhain
![GitHub release](https://img.shields.io/github/release/ppy/osu.svg)
![CodeFactor](https://www.codefactor.io/repository/github/ppy/osu/badge)
![dev chat](https://discordapp.com/api/guilds/188630481301012481/widget.png?style=shield)
![Crowdin](https://d322cqt584bo4o.cloudfront.net/osu-web/localized.svg)
![Renovate enabled](https://img.shields.io/badge/renovate-enabled-brightgreen.svg)
![license](https://img.shields.io/github/license/mashape/apistatus.svg)
![Chat](https://badges.gitter.im/awesome-twitter-bots/Lobby.svg)

## Rationale

The [ERC-721](https://eips.ethereum.org/EIPS/eip-721) and [ERC - 1155](https://eips.ethereum.org/EIPS/eip-1155) are Ethereum protocals and are also supported by other projects running on EVM-compatible virtual machines. As these two standards are widely used by NFTs issued on EVM, this project only focuses on NFTs of ERC-721 and ERC-1155.

This project discovers NFTs by listening to the transfer events of ERC-721 and ERC-1155 contracts. Why only listen to the transfer events? The first reason is that the transfer events are sufficient. The transfer events include all transferring, minting and burning. The second is because this project is part of the NFT browser, other events that are not transfer are not needed. (it may be necessary to consider adding the URI event of ERC-1155, which will issue a URI event when the URI is modified. ERC-721 does not have the similar event type).

### Events used

##### ERC-721

```
event Transfer(address indexed _from, address indexed _to, uint256 indexed _tokenId);
```

##### ERC - 1155

```
event TransferSingle(address indexed _operator, address indexed _from, address indexed _to, uint256 _id, uint256 _value);
event TransferBatch(address indexed _operator, address indexed _from, address indexed _to, uint256[] _ids, uint256[] _values);
```

When `_from` is a zero address, this event is a minting.  
When `_to` is a zero address, this event is a burning.  
When `_from` and `_to` are both non-zero addresses, this event is a normal transfer event.  


* Home (all events) - display all events for which users could buy tickets. With button "Detail" user could open form with detail information about that event.

![1](https://user-images.githubusercontent.com/25621259/124457276-e8bfab00-dd8b-11eb-998c-e29a74006b68.png)


* My tickets - display all tickets that user owns

![18](https://user-images.githubusercontent.com/25621259/124473094-30036700-dd9f-11eb-9eb4-8e118b8fdf1a.png)


* My events - events that logged user created
  
  - Display
  - Button "New event" (create new event)
  
![2](https://user-images.githubusercontent.com/25621259/124457332-f9702100-dd8b-11eb-9ac3-69e7139a139c.png)

![3](https://user-images.githubusercontent.com/25621259/124459043-068e0f80-dd8e-11eb-8c5c-76629628ae8c.png)


* Event detail - from event creator view 

  - Display
  - Button "New ticket category"
    - Field "Resell fee for event owner" shows how much percent for every resell for tickets in that ticket category will event creator get

![4](https://user-images.githubusercontent.com/25621259/124464327-5bcd1f80-dd94-11eb-8d3b-07ad888bd0c2.png)

![5](https://user-images.githubusercontent.com/25621259/124465253-7e136d00-dd95-11eb-86e2-2e419ee6112c.png)


* Event detail - from other users view (buy ticket from event host)

  With click on button "Buy" for the selected category, users could buy tickets for that event and in that category

![6](https://user-images.githubusercontent.com/25621259/124465774-16a9ed00-dd96-11eb-8ab1-c6d5ff213636.png)

![7](https://user-images.githubusercontent.com/25621259/124465784-190c4700-dd96-11eb-9c5c-ddf939584f2f.png)


* Event detail - from others users view - tickets block (set for sell)

  With clcik on button "For sell" user set price for how much will sold that ticket
  
![8](https://user-images.githubusercontent.com/25621259/124467003-8d93b580-dd97-11eb-8a81-40d6a0fd8035.png)

![9](https://user-images.githubusercontent.com/25621259/124467020-93899680-dd97-11eb-9a84-30ab5caef0f0.png)

  With click on button "Cancel sell" user pulls that ticket from market
 

* Event detail - from others users view - tickets block (set for bid and set bid)

  With click on button "For bid" user put that ticket on market, so he expect from other users to give it to him different offers
  
  With click on button "Cancel for bid" user pull that ticket from market

![10](https://user-images.githubusercontent.com/25621259/124467633-67bae080-dd98-11eb-8c93-706a50f3e3c0.png)

  Other users could bid for that ticket from view "For bids". Users could bid for currency (WETH for now), or for other tickets that he owns.
  
![13](https://user-images.githubusercontent.com/25621259/124468739-caf94280-dd99-11eb-8d77-b8a108e884a9.png)

![14](https://user-images.githubusercontent.com/25621259/124468741-cb91d900-dd99-11eb-93ba-948226a6fd91.png)

  When other users offers bids for ticket, user who owns that ticket could accept appropriate bid or decline
  
![15](https://user-images.githubusercontent.com/25621259/124469140-46f38a80-dd9a-11eb-8637-cc3fbcd72395.png)


* Event detail - from others views - tickets block ("For sell" view)

  In for sell view users could buy tickets for fixed amount
  
![16](https://user-images.githubusercontent.com/25621259/124471904-c040ac80-dd9d-11eb-9fa2-95eea664e804.png)
  

* Ticket market - similar view as "Ticket market" on "Event detail" form, except, this is for all events and all tickets in application

![17](https://user-images.githubusercontent.com/25621259/124472891-f2064300-dd9e-11eb-9abe-6946e40567c3.png)

* Account - basic informations about user that are stored on firebase, and connect with MetaMask address
 
![20](https://user-images.githubusercontent.com/25621259/124477475-5d064880-dda4-11eb-8f28-afb9813dd049.png)



## HackMoney 2021

This project is created for ETHGlobal hackathon "HackMoney 2021". For this project, they are used technologies and tools from four different sponsors for this hackathon:
- Rarible (Rarible Protocol)
- The Graph (Subgraph project and query the graph)
- Consensys (Metamask)
- Protocol Labs (IPFS and Pinata)


### Rarible

From this sponsor, I used API from https://api-reference.rarible.com/ , and also smart contract "NFTicketize.sol" is designed that support this API. Functions that I used:

* Lazy mint (with all additions such as IPFS uri, royalties, etc) with generate ID, so ticket (NFT) could see from Rarible portal (with all informations). Also, for image, I generate image with informations about event name, ticket category and ticket id, but in future, this could be some form of electronic ticket 

![19](https://user-images.githubusercontent.com/25621259/124475162-b15bf900-dda1-11eb-94fd-ee23ac80ee3a.png)

* Create a sell order

* Accepting order

* Create a bid order

* Prepare TX for order

* Different types of GET call from API (getOrderByHash, getSellOrdersByItem, getSellOrdersByCollection, getBidsByItem, getItemsByCreator, getItemsByCollection...)


### The Graph

For this sponsor, I create separate project NFTicketizeTheGraph to define subgraph. This project has three entities (Events, TicketCategories and Tickets), which I query in main project. 

In main project, all forms in some way (or in multiple ways) used graph queries.


### Consensys

MetaMask is core of this application, so by changing account, the data and app design are automatically adjusted to the new account. 

Of atypical functions, they are integration in some basic way with Firebase Functions, so token authorization for Firebase depends from metamask address.

From typical functions, it has been used different interactions with smart contract and signatures.
- Basic smart function call
- Function call with sent value (sending transactions)
- Signing data with "eth_signTypedData_v4" 


### Determine if it is an ERC-721 or ERC-1155 contract

It is not possible to determine the type of a contract by events alone, because events can be the same for different types of contracts. if two event definitions has the same name and parameter types, they can produce the same kind of events . So there are other ways to determine whether the event belongs to an ERC-721 or ERC-1155 contract.

This is achieved through [ERC-165](https://eips.ethereum.org/EIPS/eip-165).

Both ERC-721 and ERC-1155 protocals specify that NFTs need to implement the interface of ERC-165. So, we can determine whether a contract is ERC-721 or ERC - 1155 by the interface provided by ERC-165.

```
function supportsInterface(bytes4 interfaceID) external view returns (bool);
```

When you call this method, its return value will tell you the result.

The interfaceID for ERC - 721 is `0x80ac58cd`.

The interfaceID for ERC -1155 is `0xd9b67a26`.

### Consider only visual NFTs

Neither ERC-721 nor ERC-1155 require that NFTs be visual, so some non-visual NFTs may exist.

Visualization is achieved through optional metadata extension. This project will ignore these NFTs that do not implement the metadata extension. Whether NFTs implement the metadata extension is also determined by [ERC-165](https://eips.ethereum.org/EIPS/eip-165).

The interfaceID of the metadata extension for ERC -721 is `0x5b5e139f`.

The interfaceID of the metadata extension for ERC -1155 is `0x0e89341c`.

Why ignore non-visual NFTs?  This project is part of [The NFT Explorer](https://github.com/uni-arts-chain/uniscan), it will only focus the visual NFTs, so this project is only concerned with visual NFTs.

## Project Structure

#### libs/nft-events

This is the core library for discovering NFTs, used by the executables to track blockchains.

The library is divided into two parts, ERC-721 and ER -1155 parts. The reason for not abstracting into one is that there are some differences between the two, and for the sake of easy modification, they are directly considered separately, and in the future, if they become stable, they can be considered to be merged.

The ERC-721 part contains three files, which are :  

- `erc721.rs`: This is the entry file that provides the `track_erc721_events` method that the executables use to discover ERC-721 events.

- `erc721_evm.rs`: This is the core file that implements how to fetch the required ERC-721 events from the blockchain.

- `erc721_db.rs`: This is the local database support. The database here is used to cache the ERC-721 metadata. The database uses sqlite3's persistent storage, so the data will still exist after restart.

If the library is to be used, all that is needed is to implement an executable to call the `track_erc721_events`  and two callbacks with your own logic.

The ERC-1155 part is similar, includes `erc1155.rs`, `erc1155_evm.rs` and `erc1155_db.rs` 

#### livenets/* and testnets/*

The crates under the two directories are specific executables for different blockchains, each implementing a tracker for their blockchain. These executables mainly call `track_erc721_events` and `track_erc1155_events` of `nft-events`  lib to get the NFT events for their respective chains, and each has its own parameters.

The executable runs and keeps getting NFT events, then sends the NFT events and NFT metadata to the message queue of the [The NFT Explorer](https://github.com/uni-arts-chain/uniscan) (currently they are only printed into the stdout).


## Challenges

1. huge amount of historical data, which needs to be synchronized for a long time to get all the data
2. Stability of blockchain nodes, as it takes a long time to connect nodes to get data, so stable nodes are needed for access. Nowadays, public nodes are generally limited in one way or another.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).


# Crystara

---

## 1. Team Introduction
- **Team Name**: Crystara
- **Team Members**:
  - Yong - Founder, Developer - Handling frontend, backend and blockchain development. Managing social media and business relations with key partners.
- **Team Mission**: Delivering the next generation NFT Marketplace on Supra. 

---

## 2. Useful Links
- **Team Profiles**:
  - [Yong's Github](https://github.com/tyhh00)
  - [Yong's Twitter](https://x.com/tyhho0)
- **Crystara Main Links**:
  - [Website](https://crystara.trade/)
  - [Hungry Hippos X - Lootbox on Testnet](https://crystara.trade/marketplace/hungryhipposx)
  - [Twitter](https://x.com/CrystaraMarkets)
- **Crystara Repositories**:
  - [Crystara Frontend](https://github.com/tyhh00/BlindBox_ProductionSite)
  - [Crystara Blockchain Code](https://github.com/tyhh00/BlindBoxMarketplaceV1)
  - [Crystara Indexer (Public)](https://github.com/tyhh00/Crystara_Indexer)
  - [Crystara Hyperdrive API](https://github.com/tyhh00/crystara-hyperdriver)
- **Crystara Indexer API Endpoints**:
  - [Indexed 0x3::Tokens](https://api.crystara.trade/api/tokens)
  - [Indexed 0x3::Token Collections](https://api.crystara.trade/api/token-collections)
  - [Indexed Crystara::Lootboxes](https://api.crystara.trade/api/lootboxes)
  - ...
- **Resources Used**:
  - [Nolan's Starkey Wallet Example](https://github.com/nolan-supra/starkey-demo/tree/main)
  - [Aptos_Token (0x3)](https://github.com/Entropy-Foundation/aptos-core/blob/dev/aptos-move/framework/aptos-token-objects/sources/aptos_token.move)
  - [Mint_NFT Demo](https://github.com/aptos-labs/aptos-core/blob/main/aptos-move/move-examples/mint_nft/2-Using-Resource-Account/sources/create_nft_with_resource_account.move)
  - [Move Book](https://move-book.com/reference/introduction.html)
  - [Aptos STDLIB](https://github.com/Entropy-Foundation/aptos-core/tree/dev/aptos-move/framework/aptos-stdlib)
  - [Supra CLI](https://docs.supra.com/move/cli-commands)
  - [Supra-l1-sdk](https://github.com/Entropy-Foundation/supra-l1-sdk/tree/master)
  - [Supra dVRF (Testnet)](https://github.com/Entropy-Foundation/vrf-interface)
  - [Hetzner VPS](https://www.hetzner.com/)
  - [PM2](https://www.npmjs.com/package/pm2)
  - [Cloudflare Pages, Workers, Hyperdrive, R2 Object Storage](https://workers.cloudflare.com/built-with/collections/Pages/)
  - [PostgreSQL via Supabase](https://supabase.com/)
  - [Prisma ORM](https://www.prisma.io/)
  - [Supra REST-API](https://docs.supra.com/move/rest-api)
  - [Jose JWT Authentication](https://www.npmjs.com/package/jose)
  - [Sharp](https://www.npmjs.com/package/sharp)
  - [Million Linter (Recommended by @FraggorLabs)](https://www.npmjs.com/package/@million/lint)

---

## 3. Project Description
- **Project Name**: Crystara
- **Overview**: NFT Launchpad & Marketplace with Blind Box Mechanics to spark life into Supra's NFT Ecosystem.
- **Key Features**:
  - NFT collection blind boxes with rarities
  - Optional NFT regular mints with no frills 
  - NFT collection creation system (Launchpad)
  - NFT marketplace (Buy & Sell)
- **Target Audience**: NFT Creators, NFT Collectors, Game Companies, Gatcha Gamers, Skin Collectors, Traders, Blind Box Community.

---

## 4. Design/Flow Diagrams
- **System Architecture Diagram**:  
  ![System Architecture](https://raw.githubusercontent.com/tyhh00/Crystara/main/images/Server%20Architecture.png)
- **User Flow Diagram**:  
  ![User Flow](https://raw.githubusercontent.com/tyhh00/Crystara/main/images/User%20Flow.png)

---

## 5. Goals of the Project
- **Problems Solved**: Previously NFTs were really exclusive. They're meant to be 1/1s because it is hard to create a tier system, or build NFTs for games due to fees. Supra X NFTs is the perfect way to go because each creation is cheap, and costs almost nothing. Games can create their skin collections here with semi fungible or non fungible assets here with 1/1 or limited supply or infinite supply crates to level up their on chain games with special loot crates and more. It also focuses on web 2 experiences for users to create fun projects here. The goal of the project is to make the next biggest NFT marketplace trading platform. The project also had a lot of propreitary tech built like the indexers specifically for lootboxes which is a unique technical aspect that allows for customizations and elevation of the NFT scheme.
- **Project Goals**:
  - Onboard the next million NFT adopters
  - Gamification of NFT Minting
  - Onboard NFT Projects to Supra via Crystara
- **Impact**: Provides a revoluntionary backbone to NFT Collections, empowering collection creators to make collections suited for a plethora of different needs.

---

## 6. Challenges Faced & Solutions
- **Challenge 1**:  
  - Indexing Blockchain Data while there are no official indexed data:  
  - **Solution**: Supra is a new chain, there are no available supra standards to get indexed data like i.e.: Tokens in a Collection, or who owns which tokens. As such, we decided to build a custom fetch based Indexing system using an event poller. This poller fetches from a specified block height defined in .env, and will poll 10 blocks at a time via the Supra's REST-API and store data into a Postgresql DB on supabase. We'd then hosted the indexer software on a VPS in Frankfurt, and set our db location in Frankfurt as well to optimize latency. This indexing software was made public for other hackathon developers to adapt and it is a great resource for an early chain phase.
- **Challenge 2**:  
  - Global Edge Caching: 
  - **Solution**: An NFT Platform requires extremely fast load times. The technology stack had to be planned for sustainable world-wide access. My frankfurt db's data had to be readable, and writtable on the edge. As well as images, they need to be loaded on the edge. Prisma ORM does not allow for edge compute unless purchase their overpriced accelerator plans. Cloudflare's hyperdrive came in clutch and we had to fully migrate our DB interactions (R/W) to Hyperdrive and it serves us well. Images are also stored on cloudflare's R2 object storage.
- **Challenge 3**:  
  - DVRF Integration: 
  - **Solution**: Throughout the development, I realized an extremely big issue with the whitelist system for dVRF on Move chains which basically prevented it from being integrated into dAPPs, where users can call for a function that invokes rng_request. After much delibrations with our dev-rel, this was ultimately patched at the supra level.
- **Challenge 4**:  
  - Off Chain data sync:
  - **Solution**: Building custom URLs for each collection requires offchain data to be stored in our system. Syncing onchain data to offchain 1-1 is a complex task. For example, each collection needs a dedicated url endpoint for its users to access. We didnt want to use address/collectionName because it would look ugly and unprofessional. So we decided to adopt an OFFChain stats version of the lootbox which sync's with the indexer, to provide data that only the marketplace really needed. This allows for project's lootbox url to be "/hungryhippos" for e.g.
- **Challenge 5**:  
  - NFT Image Resource handling:  
  - **Solution**: Having a very intuitive UI for users to upload is a challenging process. Ideally we want the users to merely submit images, and they would be formatted for URI purposes that includes additional metadata props. How we went about it is to allow users upload images, we'd then upload them to our R2 storage under a unique folder name then use that link, to create the metadata for the token, which its image: attribute is set to the uploaded image
- **Challenge 6**:  
  - Authenticated Routes: 
  - **Solution**: Interacting with sensitive account related API routes requires some form of authentication. I'm very used to server-side auth i.e. Supabase Auth etc to ensure the actor is valid and not of malicious intent. Then I stumbled upon JWT and I had to implement a specific strip-down version of JWT called Jose for edge runtime support. Signing a message and generating a token in localstorage for cached authentication on our platform, and when the user signs out of starkey it is removed.

---

## 7. Technical Breakdown
- **Technologies Used**:
  - Programming Languages: Move Lang, Typescript, SQL
  - Frameworks/Libraries: Next.Js, React, Postgres NPM, Prisma ORM, Shadcn UI, Tailwind CSS, Framer Motion, Wrangler, Jose, Million Linter, Sharp
  - Tools/Platforms: Cloudflare R2 Object Storage, Cloudflare Pages & Workers, Cloudflare Hyperdrive, 
- **APIs/Integrations**:
  - Crystara API(https://api.crystara.trade)
  - Crystara CDN(https://cdn.crystara.trade)
- **Database**: PostgreSQL on Supabase
- **Hosting/Deployment**:
  - Frontend Hosting Platform: Cloudflare Pages
  - Hyperdrive API Hosting Platform: Cloudflare Workers
  - Indexer Hosting Platform: Hetzner VPS
  - Deployment Process: We first heavily focused on the blockchain codes and a very internal, barebones form on the website to interact with the blockchain codes. After the blockchain codes were stable, we focused on data indexing. After that we worked on API routes and NFT Image storage via R2 Object Storage. Then we worked on the UI/UX for Crystara to make sure it looks good. Then worked on the offchain statistics for accounts and lootboxes for the marketplace. Finally, once all the data required is there, we implemented the Lootbox Page, and the animation spinner for rewards.

---

## 8. Future Roadmap
- **Planned Features**:
  - Buying & Selling on the Marketplace for Individual NFT/SFTs/FTs Items.
    Marketplace For You page, showing trending collections tailored to your accounts preferences
    All other unfinished non-priority features on the website for a complete experience.
  - Inventory & Claims Page (Should be done by hackathon)
- **Long-Term Vision**: We hope to onboard as many projects as we can, and create a lively NFT ecosystem on the Supra blockchain.



---


## MY NOTES

# Basic NFT Notes

1. **OpenZeppelin Contracts for ERC721 Installation:**

   - Install OpenZeppelin contracts for ERC721 using the command:
     ```bash
     forge install OpenZeppelin/openzeppelin-contracts --no-commit
     ```

2. **Foundry Configuration:**

   - Update `Foundry.toml` with remappings to include OpenZeppelin contracts:
     ```toml
     remappings = ['@openzeppelin/contracts=lib/openzeppelin-contracts/contracts']
     ```

3. **ERC721 Basics:**

   - Import ERC721 and declare your contract as ERC721.
   - NFT contract represents a collection with each NFT having a unique `tokenId`.
   - Contract address represents the collection, followed by each unique `tokenId`.

4. **Token URI:**

   - `tokenURI` is a function in ERC721 that returns the Universal Resource Identifier (URI) for a given token.
   - Think of `tokenURI` as an API call providing metadata associated with the NFT.
   - tokenURI - ‘Universal Resource Identifier’. There is a tokenURI function in the ERC/EIP 721 (https://eips.ethereum.org/EIPS/eip-721)

- Whereas a URL is a ‘Universal Resource Locator’. A URL provides the location of the resource. A URI identifies the resource by name at the specified location or URL.

5. **IPFS Integration:**

   - IPFS is a decentralized data structure; install it for desktop.
   - NFTs can point to IPFS via URLs like https://ipfs.io for broader browser support.
   - Images can be saved in .img folder as name.png.
   - Consider pinning data to services like 'piñata.'

6. **Testing Note:**
   - When testing, use `assert` with `keccak256` for string comparison, as strings are treated as arrays.

# Interactions Script and Deployment

1. **Contracts in Script:**

   - There are three contracts; one for minting basic NFT, others for SVG NFTs.
   - Use DevOpsTools for the latest deployment information.

2. **Deployment Commands:**
   - Deployment command for Sepolia:
     ```bash
     make deploy ARGS="--network sepolia"
     ```
   - Minting command for Sepolia:
     ```bash
     make mint ARGS="--network sepolia"
     ```

# Dynamic NFT Notes

1. **Dynamic NFT Overview:**

   - Project involves switching between happy and sad faces based on mood.

2. **SVG Usage:**

   - SVG (Scalable Vector Graphic) is used instead of IPFS.
   - SVG code is saved directly on-chain, maintaining consistent quality.

3. **SVG Conversion:**

   - Convert SVG to a URI that browsers can understand using base64 encoding.

4. **Token URI Implementation:**

   - Check `tokenURI()` function in `moodNFT.sol` for details.
   - Override ERC721's `baseURI` function.

5. **ReadFile Cheat Code:**

   - Foundry's `fs_permissions` provides read access; use cautiously.
   - Set `FFI = true` for DevOpsTool access but consider using `fs_permissions` for security.

6. **Testing and Deployment:**

   - Use `forge test --fork-url $SEPOLIA_RPC_URL` to test with a forked testnet.
   - Deploy with recommended commands in the makefile.
   - Reset the Anvil chain using `make anvil` for testing.

7. **Decentralized Storage Options:**
   - Consider decentralized solutions like Filecoin and Arweave for storing data.

## Below are my original notes

# BASIC NFT NOTES

- Open zeppelin contracts for ERC721: ‘forge install OpenZeppelin/openzeppelin-contracts —no-commit’
- Foundry.toml - ‘remappings = ['@openzeppelin/contracts=lib/openzeppelin-contracts/contracts’]’
- Import ERC721 and contract is ERC721
- Launch an NFT contract is a collection of NFTs and an NFT will get a unique ‘tokenId’
- Contract address represents the collection, and then each tokenId
- In our example, we have a counter representing each token, which is set to 0 in constructor
- tokenURI - ‘Universal Resource Identifier’. There is a tokenURI function in the ERC/EIP 721 (https://eips.ethereum.org/EIPS/eip-721)
- Whereas a URL is a ‘Universal Resource Locator’. A URL provides the location of the resource. A URI identifies the resource by name at the specified location or URL.
- Can think of tokenURI like an API call representing an end point that will call the meta data associated with the NFT
- We override the tokenURI function, as it has a ‘virtual’ keyword in the ERC721 contract
- Can check an NFT on opensea - Take token ID > Go to address on etherscan > Contract > Read contract > Connect to WEB3 > Paste ID in tokenURI > Copy link. Shows the end point which should return the meta data associated with that NFT.
- Images saved in .img folder, as name.png
- IPFS - It’s a distributed, decentralised, date structure. Not a blockchain, but similar to a blockchain. No mining etc., but can pin data.
- IPFS - Our code/data > hash the data to get a unique hash that only points to your data > IPFS node doe the hashing for you, and every IPFS node on the planet hash the same hashing function > Can then pin the data to the node.
- Node is connected a network of other IPFS nodes which talk to each other, can pin data to other nodes which makes more secure in case your individual node goes down
- There’s no smart contracts etc. on IPFS, it’s just storage
- Install IPFS for desktop
- NFTS point to https://IPFS.io… do so because not a lot of browsers support ipfs://… However, pointing to https://IPFS.io… is different as if website goes down then no longer a link to NFT
- Can also pin data to ‘piñata’ for example
- When testing cannot compare string with string, as this is type of array. Need something like this -‘ assert(keccak256(abi.encodePacked(basicNft.name())) == keccak256(abi.encodePacked((NFT_NAME))) );’

Interactions script and deployment

- There’s 3 contracts in this script, one is for minting the basic NFT (other 2 are n relation to the SVG NFT)
- The DevOpsTools is used to get the most recent deployment
- Info is in makefile. The command for running on Sepolia is ‘make deploy ARGS="--network sepolia" ‘
- For minting… FFI is set to true on foundry.toml file in order to work with DevOpsTools
- make mint ARGS="--network sepolia”

# DYNAMIC NFT NOTES

- For this project, there is the ability to flip between a happy and sad face depending on your mood. Hence, dynamic.
- Instead of pinning data to IPFS node, this project uses SVG (scalable vector graphic)
- Code image as an SVG type and this is saved directly on chain
- No matter how big or small you make an SVG image, it is always going to be the same quality as it is scalable
- I have downloaded an SVG preview app, and can ‘cmd + p’ + ‘>’ to view preview of SVG file
- Need to convert SVG file to a URI that our browser can understand
- ‘cd images > cd dynamicNft’ and run ‘base64 -i example.svg’ in command line, where ‘-I’ stands for input
- Will get something like ‘PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iNTAwIiBoZWlnaHQ9IjUwMCI+Cjx0ZXh0IHg9IjAiIHk9IjE1IiBmaWxsPSJibGFjayI+SGkhIFlvdXIgYnJvd3NlciBkZWNvZGVkIHRoaXM8L3RleHQ+Cjwvc3ZnPg==‘
- This is the base64 encoded example SVG
- If you paste a line the following line in front, ‘data:image/xmg+hml;base64,’, your browser can decode it
- See tokenURI() function in moodNFT.sol.
- You can see a string, which is wrapped in ‘abi.encodePacked()’ which concatenates the string
- You could also do ‘string.concat()’
- Convert to bytes to use the OpenZeppelin base64 encoder
- Then base64.encode the whole thing, and this is the equivalent of getting the code above starting with ‘PH…’
- Use function \_baseURI() internal pure override returns (string memory) {
  return "data:application/json;base64,";
  }. For our JSON data. This is the equivalent of ‘data:image/xmg+hml;base64,’ as shown in the example above
- Override as ERC721 contract also has a baseURI function
- Create a string > Concatenated it with abi.encodePacked > turned it into bytes object > encode bytes object > combine with baseURI > turned the whole thing into a string and returned it
- There’s a readFile cheat code in Foundry. See foundry.toml - fs_permissions = [ { access = "read", path = "./images/" }, { access = "read", path = "./broadcast" }. This gives access to read at the specified location.
- ‘FFI = true’ is basically saying do whatever you want in the shell, i.e. for the DevOpsTool package. However, it’s safer if could use something like ‘fs_permissions’ as above, as this would only give access to a specific location.
- I think this ‘fs_permissions’ is in relation to reading certain code, e.g ‘string memory sadSvg = vm.readFile("./images/dynamicNft/sad.svg”);’
- Can fork a test net to run tests ‘forge test --fork-url $SEPOLIA_RPC_URL’
- Recommended to deploy on anvil using ‘make deployMood’ as per makefile. Tries with Sepolia as well, but costs too much gas.
- Resetting anvil chain. In your command line do ‘make anvil’. Go to meta mask > add network > networks > rest anvil by redoing some data > should see one of accounts in dropdown with 10000. If don’t have an account you can take an address from the list in anvil and import it.
- Do ‘make deployMood’ and copy contract address e.g 0x5FbDB2315678afecb367f032d93F642f64180aa3.
- Then ‘make mintMoodnft’ and copy the contract address and view NFT in MetaMask
- cast send 0x5FbDB2315678afecb367f032d93F642f64180aa3 “mintNft()” --private-key $(PRIVATE_KEY) --rpc-url http://localhost:8545
- Decentralised solutions for storing data include filecoin and arweave

## Below are the notes included in the course

# Foundry NFT

This is a section of the Cyfrin Foundry Solidity Course.

_[⭐️ (7:40:56) | Lesson 11: Foundry NFT](https://www.youtube.com/watch?v=sas02qSFZ74&t=27656s)_

We go through creating 2 different kinds of NFTs.

1. An IPFS Hosted NFT
2. An SVG NFT (Hosted 100% on-chain)

<br/>
<p align="center">
<img src="./images/dogNft/pug.png" width="225" alt="NFT Pug">
<img src="./images/dynamicNft/happy.svg" width="225" alt="NFT Happy">
<img src="./images/dogNft/shiba-inu.png" width="225" alt="NFT Shiba">
<img src="./images/dynamicNft/sad.svg" width="225" alt="NFT Frown">
<img src="./images/dogNft/st-bernard.png" width="225" alt="NFT St.Bernard">
</p>
<br/>

- [Foundry NFT](#foundry-nft)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Quickstart](#quickstart)
    - [Optional Gitpod](#optional-gitpod)
- [Usage](#usage)
  - [Start a local node](#start-a-local-node)
  - [Deploy](#deploy)
  - [Deploy - Other Network](#deploy---other-network)
  - [Testing](#testing)
    - [Test Coverage](#test-coverage)
- [Deployment to a testnet or mainnet](#deployment-to-a-testnet-or-mainnet)
  - [Scripts](#scripts)
  - [Base64](#base64)
  - [Estimate gas](#estimate-gas)
- [Formatting](#formatting)
- [Thank you!](#thank-you)

# Getting Started

## Requirements

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [foundry](https://getfoundry.sh/)
  - You'll know you did it right if you can run `forge --version` and you see a response like `forge 0.2.0 (816e00b 2023-03-16T00:05:26.396218Z)`

## Quickstart

```
git clone https://github.com/Cyfrin/foundry-nft-f23
cd foundry-nft-f23
forge install
forge build
```

### Optional Gitpod

If you can't or don't want to run and install locally, you can work with this repo in Gitpod. If you do this, you can skip the `clone this repo` part.

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#github.com/PatrickAlphaC/foundry-foundry-nft-f23)

# Usage

## Start a local node

```
make anvil
```

## Deploy

This will default to your local node. You need to have it running in another terminal in order for it to deploy.

```
make deploy
```

## Deploy - Other Network

[See below](#deployment-to-a-testnet-or-mainnet)

## Testing

We talk about 4 test tiers in the video.

1. Unit
2. Integration
3. Forked
4. Staging

This repo we cover #1 and #3.

```
forge test
```

or

```
forge test --fork-url $SEPOLIA_RPC_URL
```

### Test Coverage

```
forge coverage
```

# Deployment to a testnet or mainnet

1. Setup environment variables

You'll want to set your `SEPOLIA_RPC_URL` and `PRIVATE_KEY` as environment variables. You can add them to a `.env` file, similar to what you see in `.env.example`.

- `PRIVATE_KEY`: The private key of your account (like from [metamask](https://metamask.io/)). **NOTE:** FOR DEVELOPMENT, PLEASE USE A KEY THAT DOESN'T HAVE ANY REAL FUNDS ASSOCIATED WITH IT.
  - You can [learn how to export it here](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key).
- `SEPOLIA_RPC_URL`: This is url of the goerli testnet node you're working with. You can get setup with one for free from [Alchemy](https://alchemy.com/?a=673c802981)

Optionally, add your `ETHERSCAN_API_KEY` if you want to verify your contract on [Etherscan](https://etherscan.io/).

1. Get testnet ETH

Head over to [faucets.chain.link](https://faucets.chain.link/) and get some tesnet ETH. You should see the ETH show up in your metamask.

2. Deploy (IPFS NFT)

```
make deploy ARGS="--network sepolia"
```

3. Deploy (SVG NFT)

```
make deploySvg ARGS="--network sepolia"
```

## Scripts

After deploy to a testnet or local net, you can run the scripts.

Using cast deployed locally example:

```
cast send <RAFFLE_CONTRACT_ADDRESS> "enterRaffle()" --value 0.1ether --private-key <PRIVATE_KEY> --rpc-url $SEPOLIA_RPC_URL
```

or, to create a ChainlinkVRF Subscription:

```
make createSubscription ARGS="--network sepolia"
```

## Base64

To get the base64 of an image, you can use the following command:

```
echo "data:image/svg+xml;base64,$(base64 -i ./images/dynamicNft/happy.svg)"
```

Then, you can get the base64 encoding of the json object by placing the imageURI into `happy_image_uri.json` then running:

```
echo "data:application/json;base64,$(base64 -i ./images/dynamicNft/happy_image_uri.json)"
```

## Estimate gas

You can estimate how much gas things cost by running:

```
forge snapshot
```

And you'll see and output file called `.gas-snapshot`

# Formatting

To run code formatting:

```
forge fmt
```

# Thank you!

If you appreciated this, feel free to follow me or donate!

ETH/Arbitrum/Optimism/Polygon/etc Address: 0x9680201d9c93d65a3603d2088d125e955c73BD65

[![Patrick Collins Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/PatrickAlphaC)
[![Patrick Collins YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/channel/UCn-3f8tw_E1jZvhuHatROwA)
[![Patrick Collins Linkedin](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/patrickalphac/)
[![Patrick Collins Medium](https://img.shields.io/badge/Medium-000000?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/@patrick.collins_58673/)

data:application/json;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iNTAwIiBoZWlnaHQ9IjUwMCI+Cjx0ZXh0IHg9IjAiIHk9IjE1IiBmaWxsPSJibGFjayI+SGkhIFlvdXIgYnJvd3NlciBkZWNvZGVkIHRoaXM8L3RleHQ+Cjwvc3ZnPg==

data:application/json;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjAwIDIwMCIgd2lkdGg9IjQwMCIgIGhlaWdodD0iNDAwIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPgogIDxjaXJjbGUgY3g9IjEwMCIgY3k9IjEwMCIgZmlsbD0ieWVsbG93IiByPSI3OCIgc3Ryb2tlPSJibGFjayIgc3Ryb2tlLXdpZHRoPSIzIi8+CiAgPGcgY2xhc3M9ImV5ZXMiPgogICAgPGNpcmNsZSBjeD0iNjEiIGN5PSI4MiIgcj0iMTIiLz4KICAgIDxjaXJjbGUgY3g9IjEyNyIgY3k9IjgyIiByPSIxMiIvPgogIDwvZz4KICA8cGF0aCBkPSJtMTM2LjgxIDExNi41M2MuNjkgMjYuMTctNjQuMTEgNDItODEuNTItLjczIiBzdHlsZT0iZmlsbDpub25lOyBzdHJva2U6IGJsYWNrOyBzdHJva2Utd2lkdGg6IDM7Ii8+Cjwvc3ZnPg==
# foundry-NFT
# foundry-NFT

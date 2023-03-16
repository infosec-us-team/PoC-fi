A javascript library that turns Tenderly Sandbox into the fastest way to test and share professional PoCs.

--------------------------------------------
# Install

#### Option 1 - Copy the template (recommended)
- Go to https://sandbox.tenderly.co/infosec_us_team/poc-library and click `Create Copy`.

#### Option 2 - Manually inject it

- Add to the top of your `script.js` in your Tenderly Sandbox:
```javascript
// Install libraries and modules
const _lib = await fetch("https://raw.githubusercontent.com/infosec-us-team/PoC-fi/main/poc-fi.js"); eval(await _lib.text());
```

--------------------------------------------
# How to use

## Transfer tokens and NFTs faster than ever:
> The library automatically impersonates the owner of the Token/NFT.
```javascript
transfer( _address, _from, _to, _amount); // _amount for ERC20, _tokenId for ERC721
```
```javascript
transferFrom( _address, _from, _to, _amount); // _amount for ERC20, _tokenId for ERC721
```
```javascript
safeTransferFrom( _address, _from, _to, _amount); // _amount for ERC20, _tokenId for ERC721
```

## Sending transactions is super easy:
```javascript
await send({ to: _contract_object, call: "nameOfFunctionToCall", params: [], from: _from });
```
> Example:
```javascript
// Get USDC contract
const USDC = erc20("0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48");

// Send transaction to USDC contract
await send({
  to: USDC,
  call: "transfer",
  params: ["0x4707ed426Cb57B30534cb5B73788cA7c3202a51B",184975000000],
  from: "0xdfd5293d8e347dfe59e90efd55b2956a1343963d"
});
```
> Opcional parameters: `value`, `gas` and `gasPrice`.            
```javascript
await send({ to: _contract, call: "function", params: [], from: _from,
             gas: ethers.utils.hexValue(30000000000), // opcional
             value: ethers.utils.hexValue(0), // opcional
             gasPrice: ethers.utils.hexValue(0) // opcional
            });
```

> Example with ERC20:
``` javascript
// Send 184975000000 USDC from `0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48` to `0xdfd5293d8e347dfe59e90efd55b2956a1343963d`
transfer("0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48", // USDC token
         "0xdfd5293d8e347dfe59e90efd55b2956a1343963d", // _from address
         "0x4707ed426Cb57B30534cb5B73788cA7c3202a51B", // _to address
          184975000000);                               // _amount
```
> Example with ERC721:
``` javascript
// Send 1 MutantApeYachtClub (MAYC) from `0xD8897A28248a8E5A893Fe94033081f802Ab41495` to `0x7F9E815E8878677478f76E6Bc9B513a8F5A256b7`
transferFrom("0x60E4d786628Fea6478F785A6d7e704777c86a7c6", // NFT address
             "0xD8897A28248a8E5A893Fe94033081f802Ab41495", // _from
             "0x7F9E815E8878677478f76E6Bc9B513a8F5A256b7", // _to
              9157);                                       // _tokenId
```

## Initialize (standard) tokens without their ABI:

> Returns the contract object from `new ethers.Contract(_address, _abi_object, provider)`, the ABI is automatically added.
```javascript
const USDC = erc20("0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48");
```
```javascript
// Returns a contract object.
const MAYC = erc721("0x60E4d786628Fea6478F785A6d7e704777c86a7c6");
```
```javascript
// Returns a contract object.
const RaribleUserToken = erc1155("0x5C6e2892Ed14bD178F0928AbCe94C1373B8265eB");
```

## Initinialize any contract using the ABI object:
> Returns the contract object from `new ethers.Contract(_address, _abi_object, provider)`.
```javascript
const custom_contract = contract("0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48", _abi_object);
```


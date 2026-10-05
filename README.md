# CosmJS Integration

A small Node.js script that runs an escrow contract end to end on a CosmWasm testnet using CosmJS. It's a quick way to check that the contract works on a real chain and to see how a JavaScript app talks to CosmWasm.

The script uses the contract from [glassflow-escrow](https://github.com/AI-pro017/glassflow-escrow) and walks through:

1. Uploading `cw_escrow.wasm` from the sender account.
2. Instantiating the contract.
3. Creating an escrow funded with 10000 `upebble`, with an arbiter and a recipient.
4. Querying the escrow's details while it's still open.
5. Approving it from the arbiter account, which releases the funds to the recipient and closes the escrow.

## Running it

You'll need Node.js 16 or newer.

```bash
git clone https://github.com/AI-pro017/cosmjs-integration.git
cd cosmjs-integration
npm install
```

Build the escrow contract in the glassflow-escrow repo with `cargo wasm` (or the CosmWasm optimizer) and copy the result here as `cw_escrow.wasm`. Then run:

```bash
node index.js
```

Each step logs its result, including the new contract address.

## Before you run it

- The RPC endpoint and gas price point at Cliffnet (`upebble`), the old CosmWasm public testnet, which has since been shut down. Change `rpcEndpoint`, the gas price denom and the `wasm` address prefix in `index.js` to match the testnet you're using, and fund the three accounts there.
- The three accounts use the public test mnemonics from the CosmJS docs. They're fine for testnets, but never send real funds to them.
## Built with

- `@cosmjs/cosmwasm-stargate` for uploading, instantiating and executing contracts
- `@cosmjs/proto-signing` for HD wallets from mnemonics
- `@cosmjs/stargate` for fees

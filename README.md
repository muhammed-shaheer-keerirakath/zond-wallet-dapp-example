![Zond Wallet dApp Example Preview Cover](misc/zond_wallet_dapp_example_preview_cover.png)

# Zond Wallet dApp Example

A dApp web application for demonstrating the connectivity(based on EIP-6963) to the zond wallet web extension.

The application renders 3 sections:

- **Detected Wallets:** Displays all the wallets(supporting EIP-6963) installed in the browser. The wallet's icon and name is displayed. To connect to a wallet, click on the desired wallet.
- **Selected Wallet:** On succesfully connecting to a wallet, the wallet name, connected account address, uuid and rdns is displayed in this section.
- **Wallet Error:** On rejecting the connection request, or if any errors are thrown, it is displayed in this section.

## :keyboard: Run locally

- Run `git clone https://github.com/theQRL/zond-wallet-dapp-example.git` for cloning this repo to your machine.
- Run `npm install` for installing all dependencies of this project.
- Run `npm run dev` to run the application locally. By default, the application will be running at `http://localhost:5173/`.

## :link: JSON-RPC API details

Communication between a dApp and Zond Wallet happens via JSON-RPC API requests.

### eth_requestAccounts

The eth_requestAccounts method is an Ethereum provider API call that prompts the user to connect their Ethereum account(s) to the dApp.

| **Request**                                                                                           | **Response**                                                                                                                             | **Example**                                                        |
| ----------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| <pre><code>{<br> "jsonrpc": "2.0",<br> "method": "eth_requestAccounts",<br> "id": 1<br>}</code></pre> | <pre><code>{<br> "jsonrpc": "2.0",<br> "id": 1,<br> "result": ["0x1234567890abcdef1234567890abcdef12345678"]<br>}</code></pre>           | `"result": ["0x1234567890abcdef1234567890abcdef12345678"]`         |
|                                                                                                       | <pre><code>{<br> "jsonrpc": "2.0",<br> "id": 1,<br> "error": { "code": 4001, "message": "User rejected the request." }<br>}</code></pre> | `"error": {"code": 4001, "message": "User rejected the request."}` |

The following code is used to connect to Zond Wallet in the `connectWallet` method of [WalletProvider.tsx](src/components/WalletProvider.tsx) file.

```typescript
const accounts = await provider.request({ method: "eth_requestAccounts" });
```

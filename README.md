# MetaIDConnect

version: 0.0.3

## What is MetaIDConnect?

MetaIDConnect is an open-source wallet protocol specification based on the MetaID protocol. It defines the essential functionalities of plugin wallets for MetaID applications, including signing, transaction submission, broadcast, and more. It also serves as a standard for connecting blockchain wallets to decentralized MetaID applications. Our mission is to enhance the interoperability of the Web3 space by providing top-notch tools and infrastructure for an exceptional user experience. With MetaIDConnect, users can seamlessly switch between various decentralized applications without the need for reauthentication or re-entering private keys. It also offers developers a straightforward and efficient means to develop decentralized applications based on MetaID.

## Why use MetaIDConnect?
 
1. Enhanced Security for Identity Verification: Users can effortlessly switch between various decentralized applications without the need to re-enter their private keys, ensuring a more secure identity authentication process.

2. Support for Multiple Cryptocurrencies and Blockchain Networks: MetaIDConnect accommodates a wide range of cryptocurrencies and blockchain networks, offering users a broader spectrum of choices and usage experiences.

3. Streamlined Development for Decentralized Applications: MetaIDConnect provides developers with a platform for rapidly creating decentralized applications based on the MetaID protocol, thereby fostering the growth and innovation of decentralized applications.

## How to use MetaIDConnect?

To integrate with MetaIDConnect, all that's required is for a wallet to implement the MetaIDConnect protocol specifications. Wallets that adhere to the MetaIDConnect protocol specifications can serve as plugin wallets for MetaIDConnect, offering users identity authentication, signing, transaction submission, broadcasting, and other essential features when using MetaID applications.

The defined MetaIDConnect-Wallet interface is as follows:：
```ts
export interface IWallet {
  address: string

  signInput(txComposer: TxComposer, inputIndex: number, ...option): TxComposer
  send(
    toAddress: string,
    amount: number,
  ): Promise<{
    txid: string
  }>
  broadcast(txComposer: TxComposer): Promise<{ txid: string }>
  
  encrypt(data: string, alg: string, encoding: string = "hex", ...option): string
  decrypt(ciphertext: string, alg: string, encoding: string = "hex", ...option): string

  getAddress(path?: string): string
  getPublicKey(path?: string): string
}
```

1. `address`  --  The wallet's 0/0 path address.

The `address` is the wallet's 0/0 path address, for example: `1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2`. By default, the wallet's 0/0 path address is the wallet's first address, which is `m/44'/10001'/0'/0/0`.

2. `signInput(txComposer: TxComposer, inputIndex: number, ...option)`  --  TxComposer: Sign the transaction.

The `signInput` method is used for signing transactions. It takes `txComposer` as the transaction to be signed and `inputIndex` as the index of the transaction input to be signed. Based on `inputIndex`, it retrieves the transaction input to be signed from `txComposer`. Then, it uses the wallet's private key to sign the transaction input and adds the signed transaction input to `txComposer`. The method returns the `txComposer` after signing. The supported signature type is currently P2PKH. The `option` is an optional parameter used to pass additional information required for signing, such as the signature type of the transaction input being signed.

3. `send(toAddress: string, amount: number): Promise<{ txid: string }>`  --  Send the transaction.

The `send` method is used to send a transaction. It takes `toAddress` as the recipient address of the transaction and `amount` as the transaction amount (in the smallest unit). The `send` method constructs a transaction, signs it using the wallet's private key, and then broadcasts the signed transaction to the blockchain network. It returns the TxId of the transaction.

4. `broadcast(txComposer: TxComposer): Promise<{ txid: string }>`  --  Broadcast the transaction.

The `broadcast` method is used to broadcast a transaction. It takes `txComposer` as the transaction to be broadcast. It broadcasts the already signed transaction to the blockchain network and returns the TxId of the transaction.

5. `encrypt(data: string, alg: string, encoding: string = "hex", ...option): string`  --  Encrypt data.

The `encrypt` method is used for encrypting data. It takes data as the `data` to be encrypted, `alg` as the encryption algorithm, and `encoding` as the encoding format for the encrypted data. `option` is an optional parameter used to provide additional information required for encryption.
The available encryption algorithms (`alg`) include: `ecdh`, `ecies`.

6. `decrypt(ciphertext: string, alg: string, encoding: string = "hex", ...option): string`  --  Decrypt data.

The `decrypt` method is used for decrypting data. It takes `ciphertext` as the data to be decrypted, `alg` as the decryption algorithm, and `encoding` as the encoding format for the decrypted data. option is an optional parameter used to provide additional information required for decryption.
The available decryption algorithms (`alg`) include: `ecdh`, `ecies`.

7. `getAddress(path?: string): string`  --  Get the address.

The `getAddress` method is used to retrieve the address of a Wallet. It accepts an optional parameter, `path`, which is used to specify the path of the address. If `path` is empty, it defaults to the address of the Wallet at the `0/0` path. If `path` is provided, it retrieves the corresponding address based on the specified path. For example, `getAddress('/0/2')` fetches the address at the `0/2` path.

8. `getPublicKey(path?: string): string`  --  Get the public key.

The `getPublicKey` method is used to retrieve the public key of a Wallet. It accepts an optional parameter, `path`, which is used to specify the path of the public key. If `path` is empty, it defaults to the public key of the Wallet at the `0/0` path. If `path` is provided, it retrieves the corresponding public key based on the specified path. For example, `getPublicKey('/0/2')` fetches the public key at the `0/2` path.

---

## Join the community

Share your experience, contribute or ask questions with the MetaIdConnect community :
- [GitHub](https://github.com/MetaID-Labs)
- [Twitter](https://twitter.com/MetaIDio)
- [Telegram](t.me/metaidglobal)

---

## Version

### 0.0.3
  - Add `getAddress` and `getPublicKey` methods to the `IWallet` interface.

### 0.0.2
  - Add `encrypt` and `decrypt` methods to the `IWallet` interface.

### 0.0.1
  - Initial release.
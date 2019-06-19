<img src="https://user-images.githubusercontent.com/211411/34776833-6f1ef4da-f618-11e7-8b13-f0697901d6a8.png" height="100" />

## Ledger Casinocoin app API

## Usage


```js
import Transport from "@ledgerhq/hw-transport-node-hid";
// import Transport from "@ledgerhq/hw-transport-u2f"; // for browser
import Csc from "@ledgerhq/hw-app-csc";

const getCscAppVersion = async () => {
    const transport = await Transport.create();
    const csc = new Csc(transport);
    const result = await csc.getAppConfiguration();
    return result.version;
}
getCscAppVersion().then(v => console.log(v));

const getCscPublicKey = async () => {
  const transport = await Transport.create();
  const csc = new Csc(transport);
  const result = await csc.getPublicKey("44'/148'/0'");
  return result.publicKey;
};
getCscPublicKey().then(pk => console.log(pk));

const signCscTransaction = async () => {
  const transaction = ...;
  const transport = await Transport.create();
  const csc = new Csc(transport);
  const result = await csc.signTransaction("44'/148'/0'", transaction.signatureBase());
  
  // add signature to transaction
  const keyPair = CasinocoinSdk.Keypair.fromPublicKey(publicKey);
  const hint = keyPair.signatureHint();
  const decorated = new CasinocoinSdk.xdr.DecoratedSignature({hint: hint, signature: signature});
  transaction.signatures.push(decorated);
  
  return transaction;
}
signCscTransaction().then(s => console.log(s.toString('hex')));
```


[Github](https://github.com/LedgerHQ/ledgerjs/),
[API Doc](http://ledgerhq.github.io/ledgerjs/),
[Ledger Devs Slack](https://ledger-dev.slack.com/)

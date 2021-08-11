![SecreyKey](https://i.imgur.com/cMLCFX6.png)

1. We will use `create-ecdh` to generate our public and private keys
   ```shell
   $ yarn add create-ecdh
   ```
2. `create-ecdh` have two versions 
   1. for nodejs  ->   we require `create-ecdh`
      ```javascript
      const ecdh = require("create-ecdh");
      ```
   2. for browser (react)  ->  we require `create-ecdh/browser`
      ```javascript
      const ecdh = require("create-ecdh/browser");
      ```
5. we create our variable `client` and we use ecdh with curve `secp256k1` (you can use other curves)

   ```javascript
   let client = ecdh("secp256k1");
   ```

6. we then just use method `generateKeys()` to generate the public key and private key for the `client`
   ```javascript
   client.generateKeys();
   ```
7. to get publicKey we use method `getPublicKey`

   ```javascript
   let publicKey = client.getPublicKey(null, "compressed");
   ```

8. to get privateKey we use method `getPrivateKey`

   ```javascript
   let privateKey = client.getPrivateKey(null, "compressed");
   ```
9. privateKey and public key will be in type `Buffer` , in order to change it to string (for storing in database for example) use `JSON.stringify`
   ```javascript
   let stringPublicKey = JSON.stringify(publicKey)
   let stringPrivateKey = JSON.stringify(privateKey)
   ```
9. to change it again to `Buffer` we will use `JSON.parse` and `Buffer.from`
   ```javascript
   let publicKeyfromString = Buffer.from(JSON.parse(stringPublicKey).data);
   let privateKeyfromString = Buffer.from(JSON.parse(stringPrivateKey).data);
   ```
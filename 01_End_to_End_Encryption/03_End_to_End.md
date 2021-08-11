![SecreyKey](https://i.imgur.com/ZBxBpw7.png)

1. Now we need to generate secret Key from other client Public Key 
	1. in our concept we recive other client public key as string from a database of publickeys
	2. our keys are stored in our localstorgae as string
2. We require `create-ecdh` and create `client` with curve `secp256k1` (the one used to generate keys)
   ```javascript
   const ecdh = require("create-ecdh");
   let client = ecdh("secp256k1");
   ```
3. we get our public and private keys as `String` from our localstorge so we change them to `Buffer`
	```javascript
	let storedPublicKey = Buffer.from(JSON.parse(MY_PUBLIC_KEY).data);
	let storedPrivateKey = Buffer.from(JSON.parse(MY_PRIVATE_KEY).data);
	```
4. we set our keys in `client` using methods `setPublicKey` and `setPrivateKey`
	```javascript
	client.setPublicKey(storedPublicKey);
	client.setPrivateKey(storedPrivateKey);
	```
5. we get the other client publicKey as `String` so we change it as a `Buffer`
	```javascript
	let otherPublicKey = Buffer.from(JSON.parse(OTHER_PUBLIC_KEY).data);
	```
6. Now using deffie-Hellman we can mix `our` private key with `other` client to generate `secreyKey`
	```javascript
	let secretKey = client.computeSecret(otherPublicKey).toString("hex");
	```
7. Other client will use `his` private Key with `our` public key to generate the same `secreyKey`

8. Now we can use AES-256 encryption and `secreyKey` to encrypt the message

9. Other client can use `secreyKey` to decrypt the message 


	
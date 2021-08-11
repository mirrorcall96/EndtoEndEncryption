
1. We will use `Crypto-js` to encrypt our text.
   ```shell
   $ yarn add crypto-js
   ```
2. We require crypto-js in our code

   ```javascript
   const CryptoJS = require("crypto-js");
   ```

5. Now we will use AES 256bit encryption , AES 256 is a very secure , in order to bruteforce it you need to guess 2^256 times (which make virtually unbreakable with today technologies)

![AES](https://i.imgur.com/AFpNQyd.jpg)

6. we use `CryptoJS.AES` for AES (iv gernerated by default)

![SecretKey](https://i.imgur.com/eMwCY0O.png)


7. for encryption we use `CryptoJS.AES.encrypt(message,secretKey)` and we add `toString()' so we can store it in our db or send it as a message

   ```javascript
   let encrypted = CryptoJS.AES.encrypt("Hello World", "SuperSecretKey").toString();
   ```

8. for decryption we use `CryptoJS.AES.decrypt(encryptedMessage,secretKey)` and we add `toString(CryptoJS.enc.Utf8)' so we can get the plain text before encryption 

   ```javascript
   let plainText = CryptoJS.AES.decrypt(encrypted,key).toString(CryptoJS.enc.Utf8);
   ```
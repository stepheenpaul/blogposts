# Generating a Secure VAPID Key for a Node.js Project

**VAPID** stands for **Voluntary Application Server Identification for Web Push**. It is a set of specifications that allows you to identify your server and send push notifications to web applications through the Web Push Protocol.

VAPID is a widely used standard for identifying servers and sending push notifications in web applications. VAPID keys are a public and private key pair that is used to authenticate the server and encrypt the push notification payload.

In this article, we will look at a few ways you can generate a Secure VAPID Key for a node.js project.

## **Ways to Generate VAPID keys.**

### **Using the web-push library**

[**web-push**](https://www.npmjs.com/package/web-push) is a popular npm package for implementing Web Push in node.js applications. It provides a simple API for generating and sending push notifications, as well as a set of utilities for managing VAPID keys and subscriptions.

To generate a VAPID key pair using the web-push library, you can use the `generateVAPIDKeys()` function as shown below:

```javascript
const webpush = require('web-push');

const vapidKeys = webpush.generateVAPIDKeys();
console.log(vapidKeys);
```

This will generate a VAPID key pair in the form of an object with `publicKey` and `privateKey` properties. You can then use these keys to send push notifications to your web application's subscribers.

Here's an example of how you can use the web-push library to send a push notification to a subscriber:

```javascript
const subscription = {
  endpoint: 'https://fcm.googleapis.com/fcm/send/...',
  keys: {
    auth: '...',
    p256dh: '...'
  }
};

const payload = 'Hello, World!';

webpush.sendNotification(subscription, payload, {
  vapidDetails: {
    subject: 'mailto:sender@example.com',
    publicKey: vapidKeys.publicKey,
    privateKey: vapidKeys.privateKey
  }
}).catch(error => {
  console.error(error.stack);
});
```

### Using VapidKeys.com

Kindly visit [Vapid](https://vapidkeys.com/), enter your email address, and then click the "Generate" button. You should get the JSON object that contains **the subject** which is your given email address.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--AV2CI5-z--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/24m907tihzrp8k6fdfiv.png align="left")

### Using the Comand Line

If you don't want to use the online services, you can generate it through the command line. So open your terminal and enter this command.

`./node_modules/.bin/web-push generate-vapid-keys`

You should see a response in this format

`=======================================`

`Public Key: BO4imRW5SYfMtEUyfwMrrxvzJjuoThJ1FNqiUX3Z0C93Ajdrhdy0rX5iwvGBWHffmH3nP-NhVsF5XXbnHxsUnrg`

`Private Key: yI31gBBUlJYKj_7wZmPZsLGFklxNMVSk_9UVpWBXEHc =======================================`

### Using the crypto module

The [**crypto**](https://nodejs.org/api/crypto.html) module in node.js provides cryptographic functionality that includes a set of wrappers for OpenSSL's hash, HMAC, cipher, decipher, sign, and verify functions.

You can use the crypto module to generate a VAPID key pair by calling the `createECDH()` function and passing in the `'prime256v1'` curve. Here's an example of how you can do this:

```javascript
const crypto = require('crypto');

const ecdh = crypto.createECDH('prime256v1');
const publicKey = ecdh.generateKeys();
const privateKey = ecdh.getPrivateKey();
console.log({ publicKey, privateKey });
```

This will generate a VAPID key pair in the form of a `Buffer` object with the `publicKey` and `privateKey` properties. You can then use these keys to send push notifications to your web application's subscribers.

### **Using the openssl command-line tool**

You can also generate a VAPID key pair using the \[[openssl](https://www.openssl.org)\] command-line tool, which is a widely used open-source implementation of the SSL and TLS protocols. To generate a VAPID key pair using openssl, you can use the following command:

`openssl ecparam -genkey -name prime256v1 | openssl ec -out vapid_keypair.pem`

This will generate a VAPID key pair in the PEM format and save it to a file called `vapid_keypair.pem`. You can then extract the public and private keys by calling the following commands:

`openssl ec -in vapid_keypair.pem -pubout -out public_key.pem`

`openssl ec -in vapid_keypair.pem -out private_key.pem`

You can then use these keys to send push notifications to your web application's subscribers.

## **Examples**

Let's look at a few real-world examples of how VAPID keys are used in node.js applications.

### A chat application

Imagine you are building a chat application using node.js and Web Push. You can use the VAPID key pair to send push notifications to your users whenever they receive a new message. Here's an example of how you can do this using the web-push library:

```javascript
const webpush = require('web-push');

const vapidKeys = webpush.generateVAPIDKeys();

// Set the VAPID details for the application
webpush.setVapidDetails(
  'mailto:sender@example.com',
  vapidKeys.publicKey,
  vapidKeys.privateKey
);

// Send a push notification to a subscriber
const subscription = {
  endpoint: 'https://fcm.googleapis.com/fcm/send/...',
  keys: {
    auth: '...',
    p256dh: '...'
  }
};

const payload = 'You have a new message!';

webpush.sendNotification(subscription, payload).catch(error => {
  console.error(error.stack);
});
```

### A weather forecasting application

Imagine you are building a weather forecasting application using node.js and Web Push. You can use the VAPID key pair to send push notifications to your users whenever there is a weather alert in their area. Here's an example of how you can do this using the web-push library:

```javascript
const webpush = require('web-push');

const vapidKeys = webpush.generateVAPIDKeys();

// Set the VAPID details for the application
webpush.setVapidDetails(
  'mailto:sender@example.com',
  vapidKeys.publicKey,
  vapidKeys.privateKey
);

// Send a push notification to a subscriber
const subscription = {
  endpoint: 'https://fcm.googleapis.com/fcm/send/...',
  keys: {
    auth: '...',
    p256dh: '...'
  }
};

const payload = 'There is a severe weather alert in your area!';

webpush.sendNotification(subscription, payload).catch(error => {
  console.error(error.stack);
});
```

## Conclusion

In this article, we looked at a few ways you can generate a Secure VAPID Key for a node.js project. We saw how to use the web-push library, the crypto module, and the openssl command-line tool to generate a VAPID key pair. We also looked at a few case studies to see how VAPID keys are used in real-world applications.

I hope this article has helped understand how to generate a Secure VAPID Key for your node.js project. If you have any questions or need further clarification, don't hesitate to ask. Good luck with your project!
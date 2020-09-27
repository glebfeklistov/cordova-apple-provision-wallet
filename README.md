# Apple Pay

This plugin implements Apple Pay Push Provisioning API features for card enrollment integration. Lets customers add a bank card to Apple Pay from the issuer app by providing the required card details.

## Supported Platforms

- iOS (Apple devices)

## Using
It's only documentation for preview of capabilities. If you want you this plugin, contact with author for getting full version plugin.

## Installation

Type this string in cordova application root:

```sh
cordova plugin add cordova-apple-provision
```

## Check Apple Pay status
This method must be called before using any other feature in the Apple Pay SDK.

```js
getStatus(successCallback, errorCallback);
```

Success callback structure:

```json
{
    "ready": true
}
```

## Check already enrolled cards
The getAllCards method is used to request a list of the issuer's cards currently registered/enrolled by this
user in Apple Pay. The getAllCards method is typically called when the issuer app wants to check card status.

```js
getAllCards(successCallback, errorCallback);
```

Success callback structure:

```json
{
    "deviceName": "iPhone",
    "accountNumberSuffix": "0772",
    "isRemotePass": false,
    "organizationName": "BANK_ISSUER_NAME"
}
```

## Get certificates for encryption card data
This method provides the data needed to create add payment request. 
Pass the certificate chain to the issuer server. 
The server returns an encrypted JSON file containing the card data. 
After you receive the encrypted data, send it with sendPayload method.

```js
getCertificates("CARD_DATA", successCallback, errorCallback);
```

Success callback structure:

```json
{
  "certificateSubCA": "Base64 string certificateSubCA",
  "certificateLeaf": "Base64 string certificateLeaf",
  "nonce": "Base64 string nonce",
  "nonceSignature": "Base64 string nonceSignature"
}
```

Card data fields:

Card 
```json
{
    "cardholderName": "Test User",
    "primaryAccountSuffix": "1234",
    "localizedDescription": "Description of payment card",
    "paymentNetwork": "PAYMENT_NETWORK",
    "encryptionScheme": "ENCRYPTION_SCHEME"
}
```

> The encryption scheme, payment network, and primary account suffix are required for configuration.

## Pass encrypted card data to wallet
This method provides request to wallet with encrypted data for complete card enrolment.

```js
sendPayload("ENCRYPTED_DATA", successCallback, errorCallback);
```

Success callback structure:

```json
{
  "result": "success"
}
```

Encrypted card data fields:

```json
{
    "activationData": "encoded Base64 activationData",
    "encryptedPassData": "encoded Base64 encryptedPassData",
    "wrappedKey": "encoded Base64 wrappedKey",
    "ephemeralPublicKey": "encoded Base64 ephemeralPublicKey"
}
```

## List of payment networks

```json
[
  "PKPaymentNetworkVisa",
  "PKPaymentNetworkMasterCard"
]
```

## List of encryption schemes

```json
[
  "PKEncryptionSchemeRSA_V2",
  "PKEncryptionSchemeECC_V2"
]
```

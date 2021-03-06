
# Authorizing a request

## Collecting parameters

You should be able to see that the header contains 7 key/value pairs, where the keys all begin with the string “oauth_”. For any given Atomic Reach API request, collecting these 7 values and creating a similar header will allow you to specify authorization for the request. How each value was generated is described below:

## Consumer key
### oauth_consumer_key 	xvz1evFS4wEEPTGEFPHBog

## Nonce

The oauth_nonce parameter is a unique token your application should generate for each unique request. Atomic Reach will use this value to determine whether a request has been submitted multiple times. The value for this request was generated by base64 encoding 32 bytes of random data, and stripping out all non-word characters, but any approach which produces a relatively random alphanumeric
string should be OK here.

### oauth_nonce 	kYjzVBB8Y0ZFabxSWbWovY3uYSQ2pTgmZeNu2VS4cg

## Signature

The oauth_signature parameter contains a value which is generated by running all of the other request parameters and two secret values through a signing algorithm. The purpose of the signature is so that Atomic Reach can verify that the request has not been modified in transit, verify the application sending the request, and verify that the application has authorization to interact with the
user’s account.

The process for calculating the oauth_signature for this request is described in Creating a signature.
### oauth_signature 	tnnArxj06cWHq44gCs1OSKk/jLY=

## Signature method

The oauth_signature_method used by Atomic Reach is HMAC-SHA1. This value should be used for any authorized request sent to Atomic Reach’s API.
### oauth_signature_method 	HMAC-SHA1

## Timestamp

The oauth_timestamp parameter indicates when the request was created. This value should be the number of seconds since the Unix epoch at the point the request is generated, and should be easily generated in most programming languages. Atomic Reach will reject requests which were created too far in the past, so it is important to keep the clock of the computer generating requests in sync with NTP.
### oauth_timestamp 	1318622958

## Token

The oauth_token parameter typically represents a user’s permission to share access to their account with your application. There are a few authentication requests where this value is not passed or is a different form of token, but those are covered in detail in Obtaining access tokens. For most general-purpose requests, you will use what is referred to as an access token.

### oauth_token 	370773112-GmHxMAgYyLbNEtIKZeRNFsMKPR9EyMZeS9weJAEb

## Version
The oauth_version parameter should always be 1.0 for any request sent to the Atomic Reach API.
### oauth_version 	1.0

## Building the header string

To build the header string, imagine writing to a string named DST.

    Append the string “OAuth ” (including the space at the end) to DST.
    For each key/value pair of the 7 parameters listed above:
        Percent encode the key and append it to DST.
        Append the equals character ‘=’ to DST.
        Append a double quote ‘”’ to DST.
        Percent encode the value and append it to DST.
        Append a double quote ‘”’ to DST.
        If there are key/value pairs remaining, append a comma ‘,’ and a space ‘ ‘ to DST.

Pay particular attention to the percent encoding of the values when building this string. For example, the oauth_signature value of tnnArxj06cWHq44gCs1OSKk/jLY= must be encoded as tnnArxj06cWHq44gCs1OSKk%2FjLY%3D.

Performing these steps on the parameters collected above results in the following string:

OAuth oauth_consumer_key="xvz1evFS4wEEPTGEFPHBog", oauth_nonce="kYjzVBB8Y0ZFabxSWbWovY3uYSQ2pTgmZeNu2VS4cg", oauth_signature="tnnArxj06cWHq44gCs1OSKk%2FjLY%3D", oauth_signature_method="HMAC-SHA1", oauth_timestamp="1318622958", oauth_token="370773112-GmHxMAgYyLbNEtIKZeRNFsMKPR9EyMZeS9weJAEb", oauth_version="1.0"

This value should be set as the Authorization header for the request.

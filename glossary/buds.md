---
title: Federation
order: null
---

# BUDS

The [BUDS](https://github.com/Bantu/Bantu-protocol/blob/master/ecosystem/sep-0002.md) maps Bantu addresses to more information about a given user. It's a way for Bantu client software to resolve email-like addresses such as `name*yourdomain.com` into account IDs like: `GCCVPYFOHY7ZB7557JKENAX62LUAPLMGIWNZJAFV2MITK6T32V37KEJU`. Buds addresses provide an easy way for users to share payment details by using a syntax that interoperates across different domains and providers.

The [Stellar federation protocol](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0002.md) maps Bantu addresses to more information about a given user. It's a way for Stellar client software to resolve email-like addresses such as `name*yourdomain.com` into account IDs like: `GCCVPYFOHY7ZB7557JKENAX62LUAPLMGIWNZJAFV2MITK6T32V37KEJU`. Federated addresses provide an easy way for users to share payment details by using a syntax that interoperates across different domains and providers.

## Buds addresses

Bantu federated addresses are divided into two parts separated by `*`: the username and the domain.

Bantu Buds addresses are divided into two parts separated by `*`: the username and the domain.

For example: `jed*bantu.org`:

For example: `flarcos*Bantu.network`:

* `flarcos` is the username,
* `Bantu.network` is the domain.

The domain can be any valid RFC 1035 domain name. The username is limited to printable UTF-8 with whitespace and the following characters excluded: &lt;\*,&gt;.

Note that the `@` symbol is allowed in the username. This means you can use email addresses in the username of a Buds address. For example: `maria@gmail.com*Bantu.network`.

## Supporting Buds

To support federation, first create a bantu.toml file, and publish it at `https://YOUR_DOMAIN/.well-known/bantu.toml`. Complete instructions for doing that can be found in the [bantu.toml specifciation](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0001.md) \(aka SEP-1\).

To support Buds, first create a Bantu.toml file, and publish it at `https://YOUR_DOMAIN/.well-known/Bantu.toml`. Complete instructions for doing that can be found in the [Bantu.toml specifciation](https://github.com/Bantu/Bantu-protocol/blob/master/ecosystem/sep-0001.md) \(aka SEP-1\).

In general, you will want to include any and all information about your Bantu integration in your bantu.toml. To support federation specifically, you need to add a `FEDERATION_SERVER` section to your bantu.toml file that tells other people the URL of your federation endpoint.

In general, you will want to include any and all information about your Bantu integration in your Bantu.toml. To support Buds specifically, you need to add a `Buds_SERVER` section to your Bantu.toml file that tells other people the URL of your Buds endpoint.

For example: `Buds_SERVER="https://api.yourdomain.com/buds"`

Please note that your Buds server **must** use `https` protocol.

Once you've published the location of your Buds server, implement Buds url HTTP endpoint that accepts an HTTP GET request and issues responses of the form detailed below:

 To make it easier to set up a federation server, the Bantu Development foundation server you can use the \[reference implementation\]\(https://github.com/stellar/go/tree/master/services/federation\) designed to be dropped into your existing infrastructure.

To make it easier to set up a Buds server, the Bantu Development foundation server you can use the \[reference implementation\]\([https://github.com/Bantu/go/tree/master/services/Buds\](https://github.com/Bantu/go/tree/master/services/Buds%29\) designed to be dropped into your existing infrastructure..

## Buds Requests

You can use the federation endpoint to look up an account id if you have a Bantu address. You can also do reverse federation and look up a Stellar address from an account id or a transaction id. This is useful to see who has sent you a payment.

You can use the Buds endpoint to look up an account id if you have a Bantu address. You can also do reverse Buds and look up a Bantu address from an account id or a transaction id. This is useful to see who has sent you a payment.

Buds requests are http `GET` requests with the following form:

`?q=<string to look up>&type=<name,forward,id,txid>`

Supported types:

* **name**: Example: `https://YOUR_FEDERATION_SERVER/federation?q=jed*stellar.org&type=name`
* **forward**: Used for forwarding the payment on to a different network or different financial institution. The other parameters of the query will vary depending on what kind of institution is the ultimate destination of the payment and what you as the forwarding anchor supports. Your [stellar.toml](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0001.md) file should specify what parameters you expect in a `forward` federation request. If you are unable to forward or the other parameters in the request are incorrect you should return an error to this effect. Example request: `https://YOUR_FEDERATION_SERVER/federation?type=forward&forward_type=bank_account&swift=BOPBPHMM&acct=2382376`
* **id**: _not supported by all federation servers_ Reverse federation will return the federation record of the Bantu address associated with the given account ID. In some cases this is ambiguous. For instance if an anchor sends transactions on behalf of its users the account id will be of the anchor and the federation server won't be able to resolve the particular user that sent the transaction. In cases like that you may need to use **txid** instead. Example: `https://YOUR_FEDERATION_SERVER/federation?q=GD6WU64OEP5C4LRBH6NK3MHYIA2ADN6K6II6EXPNVUR3ERBXT4AN4ACD&type=id`
* **txid**: _not supported by all federation servers_ Will return the federation record of the sender of the transaction if known by the server. Example: `https://YOUR_FEDERATION_SERVER/federation?q=c1b368c00e9852351361e07cc58c54277e7a6366580044ab152b8db9cd8ec52a&type=txid`
* **name**: Example: `https://YOUR_Buds_SERVER/Buds?q=flarcos*bantu.networ&type=name`
* **forward**: Used for forwarding the payment on to a different BUDS or different financial institution. The other parameters of the query will vary depending on what kind of institution is the ultimate destination of the payment and what you as the forwarding anchor supports. Your [Bantu.toml](https://github.com/Bantu/Bantu-protocol/blob/master/ecosystem/sep-0001.md) file should specify what parameters you expect in a `forward` Buds request. If you are unable to forward or the other parameters in the request are incorrect you should return an error to this effect. Example request: `https://YOUR_Buds_SERVER/Buds?type=forward&forward_type=bank_account&swift=BOPBPHMM&acct=2382376`
* **id**: _not supported by all Buds servers_ Reverse Buds will return the Buds record of the Bantu address associated with the given account ID. In some cases this is ambiguous. For instance if an anchor sends transactions on behalf of its users the account id will be of the anchor and the Buds server won't be able to resolve the particular user that sent the transaction. In cases like that you may need to use **txid** instead. Example: `https://YOUR_Buds_SERVER/Buds?q=GD6WU64OEP5C4LRBH6NK3MHYIA2ADN6K6II6EXPNVUR3ERBXT4AN4ACD&type=id`
* **txid**: _not supported by all Buds servers_ Will return the Buds record of the sender of the transaction if known by the server. Example: `https://YOUR_Buds_SERVER/Buds?q=c1b368c00e9852351361e07cc58c54277e7a6366580044ab152b8db9cd8ec52a&type=txid`

## Buds Response

The Buds server should respond with an appropriate HTTP status code, headers, and a JSON response.

You must enable CORS on the Buds server so clients can send requests from other sites. The following HTTP header must be set for all Buds server responses.

```text
Access-Control-Allow-Origin: *
```

When a record has been found the response should return `200 OK` http status code and the following JSON body:

```text
{
  "Bantu_address": <username*domain.tld>,
  "account_id": <account_id>,
  "memo_type": <"text", "id" , or "hash"> *optional*
  "memo": <memo to attach to any payment. if "hash" type then will be base64 encoded> *optional*
}
```

If a redirect is needed the Buds server should return `3xx` http status code and immediately redirect the user to the correct URL using the `Location` header.

When a record has not been found `404 Not Found` http status code should be returned.

Every other http status code will be considered an error. The body should contain error details:

```text
{
   "detail": "extra details provided by the Buds server"
}
```

## Looking up Buds provider via a home domain entry

Accounts may optionally have a home domain specified. This allows an account to programmatically specify the main Buds provider for that account.

## Caching

You shouldn't cache responses from Buds servers. Some organizations may generate random IDs to protect their users' privacy. Those IDs may change over time.


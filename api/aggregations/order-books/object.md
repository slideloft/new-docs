---
title: The Order Book Object
order: 10
---

# object

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When Horizon returns information about an order book, it uses the following format:

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - bids - object - The prices and amounts for the buyside of the asset pair. - price\_r - object - A precise representation of the bid price of the asset pair. - n - number - The numerator. - d - number - The denominator. - price - string - The bid price of the base asset denominated in the counter asset. A number representing the decimal form of \`price\_r\`. - amount - string - The amount of counter asset that the account making this offer is willing to buy at this price. - asks - object - The prices and amounts for the sellside of the asset pair. - price\_r - object - A precise representation of the ask price of the asset pair. - n - number - The numerator. - d - number - The denominator. - price - string - The ask price of the base asset denominated in the counter asset. A number representing the decimal form of \`price\_r\`. - amount - string - The amount of counter asset that the account making this offer is willing to sell at this price. - base - object - Details about the base asset. - asset\_type - string - The type for the base asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - asset\_code - string - The code for the base asset. - asset\_issuer - string - The Stellar address of the base asset’s issuer. - counter - object - Details about the counter asset. - asset\_type - string - The type for the counter asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - asset\_code - string - The code for the counter asset. - asset\_issuer - string - The Stellar address of the counter asset’s issuer.

 \`\`\`json { "bids": \[ { "price\_r": { "n": 6014600, "d": 102275119 }, "price": "0.0588080", "amount": "0.1722469" }, { "price\_r": { "n": 1250000, "d": 21831117 }, "price": "0.0572577", "amount": "0.2991796" } \], "asks": \[ { "price\_r": { "n": 118163, "d": 2000000 }, "price": "0.0590815", "amount": "8057.2710223" }, { "price\_r": { "n": 60627, "d": 1000000 }, "price": "0.0606270", "amount": "10000.0000000" } \], "base": { "asset\_type": "native" }, "counter": { "asset\_type": "credit\_alphanum4", "asset\_code": "USD", "asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX" } } \`\`\`


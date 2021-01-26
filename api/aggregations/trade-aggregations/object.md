---
title: The Trade Aggregation Object
order: 10
---

# object

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When Horizon returns information about a trade aggregation, it uses the following format:

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - timestamp - string - Start time for this trade aggregation. Represented as milliseconds since epoch. - trade\_count - integer - Total number of trades aggregated. - base\_volume - string - Total volume of base asset. - counter\_volume - string - Total volume of counter asset. - avg - string - Weighted average price of counter asset in terms of base asset. - high - string - The highest price for this time period. - high\_r - object - The highest price for this time period as a rational number. - n - number - The numerator. - d - number - The denominator. - low - string - The lowest price for this time period. - low\_r - object - The lowest price for this time period as a rational number. - n - number - The numerator. - p - number - The denominator. - open - string - The price as seen on first trade aggregated. - open\_r - object - The price as seen on first trade aggregated as a rational number. - n - number - The numerator. - p - number - The denominator. - close - string - The price as seen on last trade aggregated. - close\_r - object - The price as seen on last trade aggregated as a rational number. - n - number - The numerator. - p - number - The denominator.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/trade\_aggregations?base\_asset\_type=native\u0026counter\_asset\_code=NGNT\u0026counter\_asset\_issuer=GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD\u0026counter\_asset\_type=credit\_alphanum4\u0026limit=200\u0026order=asc\u0026resolution=3600000\u0026start\_time=1582156800000\u0026end\_time=1582178400000" }, "next": { "href": "https://horizon.stellar.org/trade\_aggregations?base\_asset\_type=native\u0026counter\_asset\_code=NGNT\u0026counter\_asset\_issuer=GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD\u0026counter\_asset\_type=credit\_alphanum4\u0026end\_time=1582178400000\u0026limit=200\u0026order=asc\u0026resolution=3600000\u0026start\_time=1582178400000" }, "prev": { "href": "" } }, "\_embedded": { "records": \[ { "timestamp": 1582156800000, "trade\_count": 9, "base\_volume": "3487.4699458", "counter\_volume": "88675.3982178", "avg": "25.4268566", "high": "25.7603393", "high\_r": { "N": 257603393, "D": 10000000 }, "low": "25.3804530", "low\_r": { "N": 25380453, "D": 1000000 }, "open": "25.3990186", "open\_r": { "N": 2500000, "D": 98429 }, "close": "25.7090558", "close\_r": { "N": 1250000, "D": 48621 } }, { "timestamp": 1582160400000, "trade\_count": 1, "base\_volume": "0.1058787", "counter\_volume": "2.7155348", "avg": "25.6476024", "high": "25.6476019", "high\_r": { "N": 100000, "D": 3899 }, "low": "25.6476019", "low\_r": { "N": 100000, "D": 3899 }, "open": "25.6476019", "open\_r": { "N": 100000, "D": 3899 }, "close": "25.6476019", "close\_r": { "N": 100000, "D": 3899 } }, { "timestamp": 1582164000000, "trade\_count": 15, "base\_volume": "3992.1321821", "counter\_volume": "99702.0620798", "avg": "24.9746395", "high": "25.6764460", "high\_r": { "N": 5000000, "D": 194731 }, "low": "24.9291379", "low\_r": { "N": 249291379, "D": 10000000 }, "open": "25.6764460", "open\_r": { "N": 5000000, "D": 194731 }, "close": "25.0055050", "close\_r": { "N": 5001101, "D": 200000 } }, { "timestamp": 1582167600000, "trade\_count": 4, "base\_volume": "278.4950271", "counter\_volume": "7047.6740325", "avg": "25.3062832", "high": "25.3844475", "high\_r": { "N": 5000000, "D": 196971 }, "low": "25.2923181", "low\_r": { "N": 252923181, "D": 10000000 }, "open": "25.2923181", "open\_r": { "N": 252923181, "D": 10000000 }, "close": "25.3844475", "close\_r": { "N": 5000000, "D": 196971 } }, { "timestamp": 1582174800000, "trade\_count": 1, "base\_volume": "9.9379734", "counter\_volume": "252.7685174", "avg": "25.4346140", "high": "25.4346140", "high\_r": { "N": 254346140, "D": 10000000 }, "low": "25.4346140", "low\_r": { "N": 254346140, "D": 10000000 }, "open": "25.4346140", "open\_r": { "N": 254346140, "D": 10000000 }, "close": "25.4346140", "close\_r": { "N": 254346140, "D": 10000000 } } \] } } \`\`\`

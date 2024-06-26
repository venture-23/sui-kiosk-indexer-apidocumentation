# KIOSK INDEXER API


## Responses

API endpoints return the JSON representation of the resources created or edited. However, if an invalid request is submitted, or some other error occurs, returns a JSON response in the following format:

```javascript
{
  "message" : string,
  "success" : bool,
  "data"    : string
}
```

The `message` attribute contains a message commonly used to indicate errors or, in the case of deleting a resource, success that the resource was properly deleted.

The `success` attribute describes if the transaction was successful or not.

The `data` attribute contains any other metadata associated with the response. This will be an escaped string containing JSON data.

## Status Codes

Gophish returns the following status codes in its API:

| Status Code | Description |
| :--- | :--- |
| 200 | `OK` |
| 201 | `CREATED` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR` |


- APIs
    - [Basic](#basic)
        * ReadOnly APIs
            + [kiosks](#get_kiosks)
            + [kiosk detail](#get_kiosk_detail)
            + [object detail](#get_object_detail)
            + [items](#get_items)
            + [summary metric](#get_kiosk_summary)
            + [kiosk item history](#get_kiosk_item_history)
            + [kiosk transactions](#get_kiosk_transactions)
            + [single kiosk transactions](#get_single_kiosk_transactions)
            + [kiosk extensions](#get_kiosk_extensions)
            + [kiosk profit withdraws](#get_kiosk_profit_withdraws)
            + [kiosk graph](#get_kiosk_graph)
            + [item transfer policies](#get_item_transfer_policies)
            + [transaction details](#get_transaction_details)
            + [search](#search)

### get_kiosks

#### Overview
This API provides access to information about kiosks.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosks
```
GET /kiosks
```
#### Description
Retrieve a list of kiosks with optional filtering, sorting, and pagination.


#### Parameters

- `limit` (optional): The maximum number of kiosks to return per page. Default is 20.
- `sort_by` (optional): The field to sort the kiosks by. Possible values are `items`, `created_at`, `updated_at`, `profit`. Default is `-created_at`,
- `direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).
- `next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.
- `prev_cursor` (optional): Cursor for pagination. If provided, it retrieves the previous page of results.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosks?limit=1&sort_by=items&direction=desc&next_cursor=&prev_cursor='
```

#### Example Response
```
{
    "data": [
         {
            "id": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb",
            "version": 25033030,
            "created_at": 1715603927683,
            "updated_at": 1715603968197,
            "type": {
                "full": "0x2::kiosk::Kiosk",
                "package": "0x2",
                "module": "kiosk",
                "struct": "Kiosk",
                "generics": []
            },
            "owner": null,
            "ownership_type": "Shared",
            "initial_shared_version": 25033018,
            "storage_rebate": 1611200,
            "last_tx_block": "FrGehqGBq2Xi3jjMD1hYgpi7QktyCPukhK66BXnBUy4T",
            "fields": {
                "allow_extensions": {
                    "value": false
                },
                "id": {
                    "value": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb"
                },
                "item_count": {
                    "value": 9
                },
                "owner": {
                    "value": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7"
                },
                "profits": {
                    "value": "0"
                }
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 177,
        "next_cursor": "ZQAAABJjcmVhdGVkX2F0AER69nGPAQAAAl9pZABDAAAAMHg4MjllZmY0ZDZmOGRmNmYxMzc3YjRmYjAxNjQ3Y2Y1YzAyMzQ1ZDU1YTM0MjEzNmRhNDljMWNjY2FiNDQ4OWU5AAA=",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```


###  get_kiosk_detail

#### Overview
This API endpoint provides detailed information about a specific kiosk.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosk Detail
```
GET /kiosk/detail/{kiosk_id}
```
#### Description
Retrieve detailed information about a specific kiosk identified by its ID.

#### Parameters
- {kiosk_id}: The unique identifier of the kiosk.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/detail/0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb'
```

#### Example Response
```
{
    "id": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb",
    "version": 25033030,
    "created_at": 1715603927683,
    "updated_at": 1715603968197,
    "type": {
        "full": "0x2::kiosk::Kiosk",
        "package": "0x2",
        "module": "kiosk",
        "struct": "Kiosk",
        "generics": []
    },
    "owner": null,
    "ownership_type": "Shared",
    "initial_shared_version": 25033018,
    "storage_rebate": 1611200,
    "last_tx_block": "FrGehqGBq2Xi3jjMD1hYgpi7QktyCPukhK66BXnBUy4T",
    "fields": {
        "allow_extensions": {
            "value": false
        },
        "id": {
            "value": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb"
        },
        "item_count": {
            "value": 9
        },
        "owner": {
            "value": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7"
        },
        "profits": {
            "value": "0"
        }
    },
    "ownership_cap": {
        "id": "0xd9d02a4ee098eb2ccf1d4af7ebb919324e26ff0f645b5bcac118867ac659f818",
        "version": 25033030,
        "created_at": 1715603927683,
        "updated_at": 1715603968197,
        "type": {
            "full": "0x2::kiosk::KioskOwnerCap",
            "package": "0x2",
            "module": "kiosk",
            "struct": "KioskOwnerCap",
            "generics": []
        },
        "owner": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
        "ownership_type": "Address",
        "initial_shared_version": null,
        "storage_rebate": 1573200,
        "last_tx_block": "FrGehqGBq2Xi3jjMD1hYgpi7QktyCPukhK66BXnBUy4T",
        "fields": {
            "for": {
                "value": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb"
            },
            "id": {
                "value": "0xd9d02a4ee098eb2ccf1d4af7ebb919324e26ff0f645b5bcac118867ac659f818"
            }
        }
    }
}

```


<!-- ### get_kiosk_details

Returns information about single kiosk

```http
GET  /api/v1/kiosk/detail/<kiosk_id>
```

cURL
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/detail/0x720396e6f8cb22c5362eb2163886302a6e7d73f3eee1b72f1a35a6a7d601bf28'
```

*Parameters:*

| Name | Type | Description                                                    | 
|:------------|:-----|:--------------------------------------------------------|
| kiosk_id    | str  | Kiosk object id                                         |


#### A single kiosk

```
{
    "id": "0x720396e6f8cb22c5362eb2163886302a6e7d73f3eee1b72f1a35a6a7d601bf28",
    "version": 118,
    "created_at": 1712660466128,
    "updated_at": 1712660542563,
    "type": {
        "full": "0x2::kiosk::Kiosk",
        "package": "0x2",
        "module": "kiosk",
        "struct": "Kiosk",
        "generics": []
    },
    "owner": null,
    "ownership_type": "Shared",
    "initial_shared_version": 95,
    "storage_rebate": 1611200,
    "last_tx_block": "J9QFwdZ1NDicdLUf8k6FjzxituGYhNkeyjSuQwUj1q9R",
    "fields": {
        "allow_extensions": {
            "value": false
        },
        "id": {
            "value": "0x720396e6f8cb22c5362eb2163886302a6e7d73f3eee1b72f1a35a6a7d601bf28"
        },
        "item_count": {
            "value": 20
        },
        "owner": {
            "value": "0x16b80901b9e6d3c8b5f54dc8a414bb1a75067db897e7a3624793176b97445ec6"
        },
        "profits": {
            "value": "0"
        }
    },
    "ownership_cap": {
        "id": "0xa9a26bbd94cb29cd5714e8794e5cfe3e8200792527e591e0df61177062308a6c",
        "version": 118,
        "created_at": 1712660466128,
        "updated_at": 1712660542563,
        "type": {
            "full": "0x2::kiosk::KioskOwnerCap",
            "package": "0x2",
            "module": "kiosk",
            "struct": "KioskOwnerCap",
            "generics": []
        },
        "owner": "0x16b80901b9e6d3c8b5f54dc8a414bb1a75067db897e7a3624793176b97445ec6",
        "ownership_type": "Address",
        "initial_shared_version": null,
        "storage_rebate": 1573200,
        "last_tx_block": "J9QFwdZ1NDicdLUf8k6FjzxituGYhNkeyjSuQwUj1q9R",
        "fields": {
            "for": {
                "value": "0x720396e6f8cb22c5362eb2163886302a6e7d73f3eee1b72f1a35a6a7d601bf28"
            },
            "id": {
                "value": "0xa9a26bbd94cb29cd5714e8794e5cfe3e8200792527e591e0df61177062308a6c"
            }
        }
    }
}
``` -->


### get_items

#### Overview
This API endpoint provides information about items associated with a specific kiosk.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosks Items
```
GET /kiosk/items/{kiosk_id}
```
#### Description
Retrieve information about items associated with a specific kiosk identified by its ID, with optional limit, sorting, and pagination.


#### Parameters

- `kiosk_id`(required): The unique identifier of the kiosk id.
- `direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).
- `next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.
- `prev_cursor` (optional): Cursor for pagination. If provided, it retrieves the previous page of results.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/items/0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb?next_cursor=&prev_cursor=&limit=1'
```

#### Example Response
```
{
    "data": [
        {
            "id": "0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8",
            "version": 25033029,
            "created_at": 1715603925703,
            "updated_at": 1715603965225,
            "owner": "0xb356a3eceb5df30fd4b80b5b15be244dbfa2aecefeebc748227d91c70580fb5a",
            "previous_transaction": "AcyfzgX1tb3Ypgbmr5qAo6ZzcuguXnFxJqTPtTMheq8C",
            "storage_rebate": 2287600,
            "type_": {
                "full": "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword",
                "package": "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214",
                "module": "nft",
                "struct": "Sword",
                "generics": []
            },
            "ownership_type": "Object",
            "lock": {
                "id": "0x2ad7fdb5217407e91fd84230bbf1963425b3c79246f94440ecc7b50450b79964",
                "version": 25033029,
                "digest": "58Z9zx3BDwFbU9zf8CtvDax4qeJJHpfofbacBD1Gw6Qt",
                "owner": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb",
                "ownership_type": "Object",
                "previous_transaction": "AcyfzgX1tb3Ypgbmr5qAo6ZzcuguXnFxJqTPtTMheq8C",
                "value": "test",
                "details": {
                    "id": {
                        "value": "0x2ad7fdb5217407e91fd84230bbf1963425b3c79246f94440ecc7b50450b79964"
                    },
                    "name": {
                        "type_": "0x2::kiosk::Lock",
                        "fields": {
                            "id": {
                                "value": "0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8"
                            }
                        }
                    },
                    "value": {
                        "value": true
                    }
                }
            },
            "listing": null,
            "details": {
                "description": {
                    "value": "Selling Rare NFT"
                },
                "id": {
                    "value": "0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8"
                },
                "name": {
                    "value": "Kiosk NFT"
                },
                "strength": {
                    "value": "50"
                },
                "url": {
                    "value": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ8gtNrUa5bVR8qWLQIJiuG99NR2xUaUqV89qXg6WiLcQ&s"
                }
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 9,
        "next_cursor": "UQAAAAJfaWQAQwAAADB4YjM1NmEzZWNlYjVkZjMwZmQ0YjgwYjViMTViZTI0NGRiZmEyYWVjZWZlZWJjNzQ4MjI3ZDkxYzcwNTgwZmI1YQAA",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```




###  get_object_detail

#### Overview
This API provides access to information about objects.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Object
```
GET /object/{object_id}
```
#### Description
Retrieve details about a specific object.

#### Parameters
- {object_id} (required): The unique identifier of the object.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/object/0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8'
```

#### Example Response
```
{
    "_id": "0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8",
    "version": 25033029,
    "created_at": 1715603925703,
    "updated_at": 1715603965225,
    "digest": "J3oQEufiipWnayhN2rjoFvP3MN5MAqo18MV3adq9h7BK",
    "type": {
        "full": "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword",
        "package": "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214",
        "module": "nft",
        "struct": "Sword",
        "generics": []
    },
    "owner": "0xb356a3eceb5df30fd4b80b5b15be244dbfa2aecefeebc748227d91c70580fb5a",
    "ownership_type": "Object",
    "previous_transaction": "AcyfzgX1tb3Ypgbmr5qAo6ZzcuguXnFxJqTPtTMheq8C",
    "storage_rebate": 2287600,
    "fields": {
        "description": {
            "value": "Selling Rare NFT"
        },
        "id": {
            "value": "0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8"
        },
        "name": {
            "value": "Kiosk NFT"
        },
        "strength": {
            "value": "50"
        },
        "url": {
            "value": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ8gtNrUa5bVR8qWLQIJiuG99NR2xUaUqV89qXg6WiLcQ&s"
        }
    },
    "bcs": [
        177,
        28,
        138,
        187,
        44,
        27,
        0,
        250,
        202,
        235,
        93,
        88,
        75,
        1,
        211,
        219,
        92,
        63,
        156,
        155,
        86,
        173,
        183,
        120,
        158,
        65,
        32,
        164,
        233,
        112,
        139,
        184,
        9,
        75,
        105,
        111,
        115,
        107,
        32,
        78,
        70,
        84,
        16,
        83,
        101,
        108,
        108,
        105,
        110,
        103,
        32,
        82,
        97,
        114,
        101,
        32,
        78,
        70,
        84,
        100,
        104,
        116,
        116,
        112,
        115,
        58,
        47,
        47,
        101,
        110,
        99,
        114,
        121,
        112,
        116,
        101,
        100,
        45,
        116,
        98,
        110,
        48,
        46,
        103,
        115,
        116,
        97,
        116,
        105,
        99,
        46,
        99,
        111,
        109,
        47,
        105,
        109,
        97,
        103,
        101,
        115,
        63,
        113,
        61,
        116,
        98,
        110,
        58,
        65,
        78,
        100,
        57,
        71,
        99,
        81,
        56,
        103,
        116,
        78,
        114,
        85,
        97,
        53,
        98,
        86,
        82,
        56,
        113,
        87,
        76,
        81,
        73,
        74,
        105,
        117,
        71,
        57,
        57,
        78,
        82,
        50,
        120,
        85,
        97,
        85,
        113,
        86,
        56,
        57,
        113,
        88,
        103,
        54,
        87,
        105,
        76,
        99,
        81,
        38,
        115,
        50,
        0,
        0,
        0,
        0,
        0,
        0,
        0
    ]
}


```

### get_kiosk_transactions

#### Overview
This API provides access to information about transactions related to all the kiosks.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get  Kiosk Transactions
```
GET /kiosks/transactions
```
#### Description
Retrieve details about transactions related to kiosks.

#### Parameters

- `limit` (optional): Limit the number of transactions returned. Default is 20.
- `offset` (optional): Offset for pagination. Default is 0.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/transactions?limit=1&offset=0'
```

#### Example Response
```
{
    "data": [
        {
            "tx_digest": "FrGehqGBq2Xi3jjMD1hYgpi7QktyCPukhK66BXnBUy4T",
            "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
            "kind": "ProgrammableTransaction",
            "checkpoint_sequence_number": 34695227,
            "timestamp": 1715603968197,
            "executed_epoch": 368,
            "status": true,
            "gas": {
                "price": 1000,
                "budget": 7944720,
                "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                "storage_cost": 11362000,
                "storage_rebate": 6395400,
                "computation_cost": 1000000,
                "non_refundable_storage_fee": 64600
            },
            "move_calls": [
                {
                    "args": [
                        "Input(0)",
                        "Input(1)",
                        "Input(2)",
                        "Input(3)"
                    ],
                    "module": "kiosk",
                    "package": "0x0000000000000000000000000000000000000000000000000000000000000002",
                    "type_args": [
                        "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword"
                    ],
                    "function_name": "lock"
                }
            ],
            "input": [
                {
                    "mutable": true,
                    "object_id": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb",
                    "object_type": "sharedObject",
                    "initial_shared_version": 25033018
                },
                {
                    "digest": "Gu257aVzrZPur4e8zv8FjKPUooDvMSTcPA4C8VPoVTGY",
                    "version": 25033029,
                    "object_id": "0xd9d02a4ee098eb2ccf1d4af7ebb919324e26ff0f645b5bcac118867ac659f818",
                    "object_type": "immOrOwnedObject"
                },
                {
                    "mutable": false,
                    "object_id": "0x8a3409de2ba7fa460d7dda83c3c9aaa29e339c1987272b25f2af979b42dad76d",
                    "object_type": "sharedObject",
                    "initial_shared_version": 25033020
                },
                {
                    "digest": "EgxfCtAqtuyFdbDmEsfehqeg2ivc36ZfBpwBvSspoLfT",
                    "version": 25033017,
                    "object_id": "0xc9eb15b71ce2e15eccdd54e8953306c2e883f0a65fc951f84a0b6f39d8e5c64c",
                    "object_type": "immOrOwnedObject"
                }
            ],
            "object_changes": {
                "transferred_objects": null,
                "deleted_object": [
                    {
                        "digest": "AsyLrvhzQ6px6rSSqJ4Z5KBhDw7At5LwZ95Uf5CfE36Q",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0x0397f98f589525f8ca7c8aa74b350109ba135b0b1e523e0febedf41ff7c50963",
                        "timestamp": 1715603968197,
                        "object_type": "0x2::coin::Coin<0x2::sui::SUI>"
                    },
                    {
                        "digest": "3UdntZuaNPDTHAsrnc6qDMHoWFRiEuLfjZvaX3F3Z5vy",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb",
                        "timestamp": 1715603968197,
                        "object_type": "0x2::kiosk::Kiosk"
                    },
                    {
                        "digest": "J5dVYmG1US1QVKd4EkVZoepouLo8XPBNLqGptB7h6ZzB",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0xc9eb15b71ce2e15eccdd54e8953306c2e883f0a65fc951f84a0b6f39d8e5c64c",
                        "timestamp": 1715603968197,
                        "object_type": "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword"
                    },
                    {
                        "digest": "F6DZCeinnwnP9HVHu1jFEsQz1XQhYxZGnmGF8mQdyQ6N",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0xd9d02a4ee098eb2ccf1d4af7ebb919324e26ff0f645b5bcac118867ac659f818",
                        "timestamp": 1715603968197,
                        "object_type": "0x2::kiosk::KioskOwnerCap"
                    }
                ],
                "created_object": [
                    {
                        "digest": "QmoZ3pgSoX7QbCx1jvBWxCVUw6df5pRGEv2Dj1wgnPr",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0x079c32ba4fd3af76f9e2a418c2f2f6b563d299b44ca186026f6dff98db585b42",
                        "timestamp": 1715603968197,
                        "object_type": "0x2::dynamic_field::Field<0x2::kiosk::Lock, bool>"
                    },
                    {
                        "digest": "DKsmkkKDKrywkkC1VyGDcrKbpCGi81Gsigc2r89ag4NP",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0x2e99cb0210761467f356db344d54487abe901fe90c614abc1d5ca76d521c025f",
                        "timestamp": 1715603968197,
                        "object_type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>"
                    }
                ],
                "mutated_objects": null
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "offset": 0,
        "total": 1047
    }
}

```





### get_single_kiosk_transactions

#### Overview
This API provides transaction data associated with a specific kiosk.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Single Kiosk Transactions
```
Retrieve transaction data associated with a specific kiosk.
```
#### Description
Retrieve transaction data associated with a specific kiosk.

#### Parameters

- `kiosk_id` (string): The ID of the kiosk.
- `limit` (optional): Limit the number of transactions returned. Default is 20.
- `limit` (optional): Limit the number of transactions returned. Default is 20.
- `offset` (optional): Offset for pagination. Default is 0.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb/transactions?limit=1&&offset=0'
```

#### Example Response
```
{
    "data": [
        {
            "tx_digest": "EYPFnu2CLA3mWdewMi7TgoSxJR5Ved8uZHLeT37EotXz",
            "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
            "kind": "ProgrammableTransaction",
            "checkpoint_sequence_number": 34695221,
            "timestamp": 1715603962230,
            "executed_epoch": 368,
            "status": true,
            "gas": {
                "price": 1000,
                "budget": 7944720,
                "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                "storage_cost": 11362000,
                "storage_rebate": 6395400,
                "computation_cost": 1000000,
                "non_refundable_storage_fee": 64600
            },
            "move_calls": [
                {
                    "args": [
                        "Input(0)",
                        "Input(1)",
                        "Input(2)",
                        "Input(3)"
                    ],
                    "module": "kiosk",
                    "package": "0x0000000000000000000000000000000000000000000000000000000000000002",
                    "type_args": [
                        "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword"
                    ],
                    "function_name": "lock"
                }
            ],
            "input": [
                {
                    "mutable": true,
                    "object_id": "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb",
                    "object_type": "sharedObject",
                    "initial_shared_version": 25033018
                },
                {
                    "digest": "28aksLyeohZ4y17HQWitQKw9yyHDH2jvVwBSRfjEhknc",
                    "version": 25033027,
                    "object_id": "0xd9d02a4ee098eb2ccf1d4af7ebb919324e26ff0f645b5bcac118867ac659f818",
                    "object_type": "immOrOwnedObject"
                },
                ...
            ],
            "object_changes": {
                "deleted_object": [
                    {
                        "digest": "DdpZkPfKB1VK3W4T1Z7ycjX6pGBEZfqeQV28hDuWFxTy",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0x0397f98f589525f8ca7c8aa74b350109ba135b0b1e523e0febedf41ff7c50963",
                        "timestamp": 1715603962230,
                        "object_type": "0x2::coin::Coin<0x2::sui::SUI>"
                    },
                    ...
                ],
                "created_object": [
                    {
                        "digest": "4iqGopvp7Q1uceGeqTbtyHyNrx6vLwx98Kz3xue9qSzc",
                        "sender": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                        "object_id": "0x35458b3e1c162364fd9793810afd2e374f49d9831fd5888d4fe7002ae583279e",
                        "timestamp": 1715603962230,
                        "object_type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>"
                    },
                    ...
                ],
                "transferred_objects": null,
                "mutated_objects": null
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "offset": 0,
        "total": 10
    }
}

```

###  get_kiosk_summary

#### Overview
This API provides access to information about objects.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosk Summary
```
GET /kiosk/summary
```
#### Description

Retrieve a summary of statistics related to kiosks.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/summary'
```

#### Example Response
```
{
    "kiosks": 177,
    "extensions": 39,
    "items": 1787,
    "profits": 13570077663,
    "locked_items": 896,
    "listed_items": 774
}

```

###  get_kiosk_item_history

#### Overview
This API provides a history of actions performed on items associated with a specific kiosk.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosk Item History
```
GET /kiosk/<kiosk_id>/items/history
```
#### Description

Retrieve a history of actions performed on items associated with a specific kiosk.


#### Parameters

- `kiosk_id` (required): The ID of the kiosk.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb/items/history'
```

#### Example Response
```
{
    "0xd9d02a4ee098eb2ccf1d4af7ebb919324e26ff0f645b5bcac118867ac659f818": [
        {
            "action": "lock",
            "timestamp": 1715603965225,
            "tx_digest": "AcyfzgX1tb3Ypgbmr5qAo6ZzcuguXnFxJqTPtTMheq8C"
        },
        ...
    ],
    "0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb": [
        {
            "action": "lock",
            "timestamp": 1715603965225,
            "tx_digest": "AcyfzgX1tb3Ypgbmr5qAo6ZzcuguXnFxJqTPtTMheq8C"
        },
        ...
    ],
    ...
}
```

###  get_kiosk_profit_withdraws

#### Overview
This API endpoint allows you to retrieve information about withdrawals made from a specific kiosk.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosk Profits Withdrawals

```
GET /kiosk/<kiosk_id>/withdrawals
```
#### Description

Retrieve information about withdrawals made from a specific kiosk.

#### Parameters

- `kiosk_id` (required):  The ID of the kiosk for which you want to retrieve withdrawal information.
- `limit` (optional): Limit the number of transactions returned. Default is 20.
- `offset` (optional): Offset for pagination. Default is 0.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/0x25f7579bf0baadc72a80357141a0e2e0ff06914a2c832ba1f474f55930d4a4eb/items/history'
```

#### Example Response
```
{
    "data": [
         {
            "tx_digest": "Dp5L3mB2pcF7Kt4LRsojzRUXPYU6NTUhJDdApBNdB6pB",
            "timestamp": 1715603650053,
            "amt": 90000000
        }
    ],
    "page_info": {
        "limit": 20,
        "offset": 0,
        "total": 1
    }
}

```



###  get_kiosk_extensions

#### Overview
This API provides information about extensions associated with a specific kiosk.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosk Extensions
```
GET /kiosks/<kiosk_id>/extensions
```
#### Description

Retrieve information about extensions associated with a specific kiosk.


#### Parameters

- `kiosk_id` (required): The ID of the kiosk.
- `limit` (optional): The maximum number of kiosks to return per page. Default is 20.
- `direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).
- `next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.
- `prev_cursor` (optional): Cursor for pagination. If provided, it retrieves the previous page of results.

#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosks/0x18ed34f58368d5927a3789e0ed55c2948175f5548d3b4b4aa29bbbda8b6db1eb/extensions'
```

#### Example Response
```
{
    "data": [
        {
            "id": "0x8c3b02111b6df707a354609e4eeec8bf95d441c206716967ec2c2dead84e6ead",
            "version": 25033003,
            "created_at": 1715603657069,
            "updated_at": null,
            "type": {
                "full": "0x2::dynamic_field::Field<0x2::kiosk_extension::ExtensionKey<0x49ac265c392a74f0dea85f3388d93931e79633edfbeb37817f3788b627d87c7a::ext::Ext>, 0x2::kiosk_extension::Extension>",
                "package": "0x2",
                "module": "dynamic_field",
                "struct": "Field",
                "generics": [
                    "0x2::kiosk_extension::ExtensionKey<0x49ac265c392a74f0dea85f3388d93931e79633edfbeb37817f3788b627d87c7a::ext::Ext>",
                    "0x2::kiosk_extension::Extension"
                ]
            },
            "owner": "0x18ed34f58368d5927a3789e0ed55c2948175f5548d3b4b4aa29bbbda8b6db1eb",
            "ownership_type": "Object",
            "initial_shared_version": null,
            "storage_rebate": 3024800,
            "last_tx_block": "EQq3DG4ZsqXzR2MLErDYt1GpXUAJyvCWbUmQTz49gDuM",
            "fields": {
                "id": {
                    "value": "0x8c3b02111b6df707a354609e4eeec8bf95d441c206716967ec2c2dead84e6ead"
                },
                "name": {
                    "type_": "0x2::kiosk_extension::ExtensionKey<0x49ac265c392a74f0dea85f3388d93931e79633edfbeb37817f3788b627d87c7a::ext::Ext>",
                    "fields": {
                        "dummy_field": {
                            "value": false
                        }
                    }
                },
                "value": {
                    "type_": "0x2::kiosk_extension::Extension",
                    "fields": {
                        "is_enabled": {
                            "value": true
                        },
                        "permissions": {
                            "value": "10"
                        },
                        "storage": {
                            "type_": "0x2::bag::Bag",
                            "fields": {
                                "id": {
                                    "value": "0x34c48013647a0fd86d9c97bfcee2c92766889ce2965f3de2a5ac52fc9e0bb303"
                                },
                                "size": {
                                    "value": "0"
                                }
                            }
                        }
                    }
                }
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 1,
        "next_cursor": "UQAAAAJfaWQAQwAAADB4OGMzYjAyMTExYjZkZjcwN2EzNTQ2MDllNGVlZWM4YmY5NWQ0NDFjMjA2NzE2OTY3ZWMyYzJkZWFkODRlNmVhZAAA",
        "prev_cursor": null,
        "direction": "Next"
    }
}

```

###  get_kiosk_graph

#### Overview
This API endpoint allows you to retrieve graph data related to kiosks.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosk Graph data
```
GET /kiosk/graph
```
#### Description

This endpoint provides a graph of data related to the kiosk. The data can be items, withdrawals, or creations, depending on the parameter passed in the request. 
And the range of time with the frequency.

#### Parameters
- `graph` (required): graph for the given query params (creation/withdrawl/item)
- `from` (required): start time of the range in Unix timestamp format.
- `to` (required): the end time of the range in Unix timestamp format.
- `freq` (required): the frequency at which data points should be aggregated, in this case, per day.


#### Example Request
```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosk/graph?graph=creation&from=1713112971&to=1715704971&freq=day'
```

#### Example Response
```
{
    "data": [
        {
    "2024-05-10 00:00:00UTC": 51,
    "2024-05-08 00:00:00UTC": 5,
    "2024-05-12 00:00:00UTC": 3,
    "2024-05-09 00:00:00UTC": 40,
    "2024-05-11 00:00:00UTC": 6,
    "2024-05-13 00:00:00UTC": 59
}
```

### get_item_transfer_policies

#### Overview
This API provides information about transfer policies.

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Item transfer policies
```
GET /item-policy/{item_id}?limit=1
```
#### Description
This endpoint retrieves information about an item policy associated with the item.

#### Parameters

- `item_id` : The unique identifier of the item id.
- `limit` (optional): The maximum number of kiosks to return per page. Default is 20.
- `direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).
- `next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.
- `prev_cursor` (optional): Cursor for pagination. If provided, it retrieves the previous page of results.

#### Example Request
```
curl --location https://kioskapp.venture23.xyz/api/v1/item-policy/0xb11c8abb2c1b00facaeb5d584b01d3db5c3f9c9b56adb7789e4120a4e9708bb8?limit=1
```

#### Example Response
```
{
    "data": [
        {
            "id": "0x8a3409de2ba7fa460d7dda83c3c9aaa29e339c1987272b25f2af979b42dad76d",
            "version": 25033021,
            "created_at": 1715603931621,
            "updated_at": 1715603937553,
            "type": {
                "full": "0x2::transfer_policy::TransferPolicy<0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword>",
                "package": "0x2",
                "module": "transfer_policy",
                "struct": "TransferPolicy",
                "generics": [
                    "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword"
                ]
            },
            "owner": null,
            "ownership_type": "Shared",
            "initial_shared_version": 25033020,
            "storage_rebate": 2508000,
            "last_tx_block": "J915TN35nFLu3dgRuuEry4US5P2Xouttbv5xai1D15rF",
            "fields": {
                "balance": {
                    "value": "0"
                },
                "id": {
                    "value": "0x8a3409de2ba7fa460d7dda83c3c9aaa29e339c1987272b25f2af979b42dad76d"
                },
                "rules": {
                    "type_": "0x2::vec_set::VecSet<0x1::type_name::TypeName>",
                    "fields": {
                        "contents": {
                            "value": [
                                {
                                    "type_": "0x1::type_name::TypeName",
                                    "fields": {
                                        "name": {
                                            "value": "e1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::item_locked_policy::Rule"
                                        }
                                    }
                                }
                            ]
                        }
                    }
                }
            },
            "ownership_cap": {
                "id": "0x02f27b91510f0579d5d7ea5846149fa2efc1a9980de0abe3d242b778257fe7db",
                "version": 25033021,
                "created_at": 1715603931621,
                "updated_at": 1715603937553,
                "type": {
                    "full": "0x2::transfer_policy::TransferPolicyCap<0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword>",
                    "package": "0x2",
                    "module": "transfer_policy",
                    "struct": "TransferPolicyCap",
                    "generics": [
                        "0xe1ab956722f0544979729d679411b87fd448dce82564007ca8935803b1d2f214::nft::Sword"
                    ]
                },
                "owner": "0x0850b12520f4f23a1510cf23ae06a34c073c2582c47d59bdddc6b85a59253eb7",
                "ownership_type": "Address",
                "initial_shared_version": null,
                "storage_rebate": 2014000,
                "last_tx_block": "J915TN35nFLu3dgRuuEry4US5P2Xouttbv5xai1D15rF",
                "fields": {
                    "id": {
                        "value": "0x02f27b91510f0579d5d7ea5846149fa2efc1a9980de0abe3d242b778257fe7db"
                    },
                    "policy_id": {
                        "value": "0x8a3409de2ba7fa460d7dda83c3c9aaa29e339c1987272b25f2af979b42dad76d"
                    }
                }
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 2,
        "next_cursor": "UQAAAAJfaWQAQwAAADB4OGEzNDA5ZGUyYmE3ZmE0NjBkN2RkYTgzYzNjOWFhYTI5ZTMzOWMxOTg3MjcyYjI1ZjJhZjk3OWI0MmRhZDc2ZAAA",
        "prev_cursor": null,
        "direction": "Next"
    }
}

```


### get_transaction_details

#### Overview
This API provides information about the transaction details

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get transaction details
```
GET /tx/{tx_digest}
```

#### Description
This endpoint retrieves information about the transactions from the given digest.

#### Parameters

- `tx_digest` : The unique identifier of transaction digest.

#### Example Request
```
curl --location https://kioskapp.venture23.xyz/api/v1/tx/V4CpxhJhvLVaApoEhX2aNcQHkDacGFLUFyNW9Wsrzr3
```

#### Example Response
```
{
    "tx_digest": "V4CpxhJhvLVaApoEhX2aNcQHkDacGFLUFyNW9Wsrzr3",
    "kind": "ProgrammableTransaction",
    "checkpoint_sequence_number": 35584287,
    "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
    "signature": [
        "007db4293c7da5bf41b937fc2eb4247690aaf3ffd2e3187486c77462caf4eecc535304649d9f28cbccad7a6d04a098f2ae9d6b12275147985da56f171ccb2da308635df1e98fa3dd70b8147ccec9c04c29735b4c497e3cf094c4b725708c899fa9"
    ],
    "timestamp": 1715817173562,
    "status": true,
    "executed_epoch": 371,
    "gas": {
        "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
        "price": 1000,
        "budget": 3060352,
        "computation_cost": 1000000,
        "storage_cost": 13490000,
        "storage_rebate": 13407768,
        "non_refundable_storage_fee": 135432
    },
    "move_calls": [
        {
            "package": "0x06f6bdd3f2e2e759d8a4b9c252f379f7a05e72dfe4c0b9311cdac27b8eb791b1",
            "module": "personal_kiosk",
            "function_name": "borrow_val",
            "type_args": [],
            "args": [
                "Input(1)"
            ]
        },
        {
            "package": "0x20695982a54d29b8d18a1fa4b37f26df910970822b4b693ffc71ee958c82c3e3",
            "module": "character_inventory",
            "function_name": "unequip_item",
            "type_args": [
                "0x3e956ac677170ac32ca32d801e0f6c730c11df3f3ec0fe191bed4232c3c91d92::item::Item"
            ],
            "args": [
                "Input(0)",
                "NestedResult(0,0)",
                "Input(2)",
                "Input(3)",
                "Input(4)"
            ]
        },
        {
            "package": "0x0000000000000000000000000000000000000000000000000000000000000002",
            "module": "kiosk",
            "function_name": "return_purchase_cap",
            "type_args": [
                "0x3e956ac677170ac32ca32d801e0f6c730c11df3f3ec0fe191bed4232c3c91d92::item::Item"
            ],
            "args": [
                "Input(0)",
                "NestedResult(1,0)"
            ]
        },
        {
            "package": "0x0000000000000000000000000000000000000000000000000000000000000002",
            "module": "kiosk",
            "function_name": "list_with_purchase_cap",
            "type_args": [
                "0x3e956ac677170ac32ca32d801e0f6c730c11df3f3ec0fe191bed4232c3c91d92::item::Item"
            ],
            "args": [
                "Input(0)",
                "NestedResult(0,0)",
                "Input(5)",
                "Input(6)"
            ]
        },
        {
            "package": "0x20695982a54d29b8d18a1fa4b37f26df910970822b4b693ffc71ee958c82c3e3",
            "module": "character_inventory",
            "function_name": "equip_item",
            "type_args": [
                "0x3e956ac677170ac32ca32d801e0f6c730c11df3f3ec0fe191bed4232c3c91d92::item::Item"
            ],
            "args": [
                "Input(0)",
                "NestedResult(0,0)",
                "Input(7)",
                "Input(8)",
                "NestedResult(3,0)",
                "Input(4)"
            ]
        },
        {
            "package": "0x06f6bdd3f2e2e759d8a4b9c252f379f7a05e72dfe4c0b9311cdac27b8eb791b1",
            "module": "personal_kiosk",
            "function_name": "return_val",
            "type_args": [],
            "args": [
                "Input(1)",
                "NestedResult(0,0)",
                "NestedResult(0,1)"
            ]
        }
    ],
    "inputs": [
        {
            "type": "object",
            "objectType": "sharedObject",
            "objectId": "0xa7b9d490972387e9fc40f08c5c30ccb573098428153154a052d41d75ca80c629",
            "initialSharedVersion": "30129358",
            "mutable": true
        },
        {
            "type": "object",
            "objectType": "immOrOwnedObject",
            "objectId": "0x83ad1892580cd62eff230a4dc9763e96951677d663d9d4f4469c8e68e2965810",
            "version": "30129560",
            "digest": "41iGWYRpJkNTMhqm48GR4w4Gbs139gT7Aoaj3Px6UuNy"
        },
        {
            "type": "pure",
            "valueType": "0x2::object::ID",
            "value": "0xbed7df040742eed1405ce8ddc7f38260eebc88ab1cbe68a5526f1a5db2167b19"
        },
        {
            "type": "pure",
            "valueType": "0x1::string::String",
            "value": "right_ring"
        },
        {
            "type": "object",
            "objectType": "sharedObject",
            "objectId": "0x07ff28bf6619a3f2947ad1bd40e8b7cad509fc7da9ef3cf42fdb131e51e74dc0",
            "initialSharedVersion": "30129516",
            "mutable": false
        },
        {
            "type": "pure",
            "valueType": "0x2::object::ID",
            "value": "0xd857af3830a421b9ceef104005e575a715b6b145d8398751085f256af55a3583"
        },
        {
            "type": "pure",
            "valueType": "u64",
            "value": "18446744073709551615"
        },
        {
            "type": "pure",
            "valueType": "0x2::object::ID",
            "value": "0xbed7df040742eed1405ce8ddc7f38260eebc88ab1cbe68a5526f1a5db2167b19"
        },
        {
            "type": "pure",
            "valueType": "0x1::string::String",
            "value": "hat"
        }
    ],
    "object_changes": {
        "created": [
            {
                "object_id": "0x793afb9468039f98cee7e9c0aee500879cdd2adca694ae48d2784690d5b3e833",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x1::string::String>, 0x2::object::ID>",
                "digest": "5465A6GnEaUUcqZrStPsQTQM5Shp39rDpsVBGDETY1Rv"
            },
            {
                "object_id": "0x86f8e5b531383c8a0d6fba9a6421bdad98af4a6e20bcc1905192fbf7b334537d",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x2::dynamic_field::Field<0x2::kiosk::Listing, u64>",
                "digest": "EYnUW82955Gngpj1fxSPgdQnqZp7JM5BvRyRyiFkNuXJ"
            },
            {
                "object_id": "0xe06c64eaf9a28819986ba14bb1833343a811df1a762b95ffad45bffd7d63520e",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x2::kiosk::PurchaseCap<0x3e956ac677170ac32ca32d801e0f6c730c11df3f3ec0fe191bed4232c3c91d92::item::Item>",
                "digest": "BKSSSp2aM8Xp3WAbLkJxeiMA6Zt1x1PjtGieftJUT9Nf"
            }
        ],
        "mutated": [
            {
                "object_id": "0x280106cab9c98c600ff2e29e0860137b6709f9ecea2509ecaa1d6ae4591f36f5",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x2::coin::Coin<0x2::sui::SUI>",
                "digest": "CL823CP3UHZp6D2WFuMehGCAZfpATgYbG1pJnjp3sfLF"
            },
            {
                "object_id": "0x83ad1892580cd62eff230a4dc9763e96951677d663d9d4f4469c8e68e2965810",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x6f6bdd3f2e2e759d8a4b9c252f379f7a05e72dfe4c0b9311cdac27b8eb791b1::personal_kiosk::PersonalKioskCap",
                "digest": "6DQstpZSQeJTUDtxzMbJp1P3KQ1rKbd9ftX3SdLq2UqX"
            },
            {
                "object_id": "0xa7b9d490972387e9fc40f08c5c30ccb573098428153154a052d41d75ca80c629",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x2::kiosk::Kiosk",
                "digest": "FKNo2JYBgUKUu2ao766Zh6Yg8eLNsHvygVUijvkeCAQv"
            },
            {
                "object_id": "0xbed7df040742eed1405ce8ddc7f38260eebc88ab1cbe68a5526f1a5db2167b19",
                "sender": "0xb1329007ab91c20209db03bf4126bb7b002b7de4fca20b576ac3ad48b5e88224",
                "object_type": "0x3e956ac677170ac32ca32d801e0f6c730c11df3f3ec0fe191bed4232c3c91d92::character::Character",
                "digest": "3WanewwEj3J9RZcdyHe1C6Wjke4v11TgaGiwwKwBMNpR"
            }
        ]
    }
}
```








### search

#### Overview
This API provides search for transaction digest and object id

#### Base URL
```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get search result
```
GET /tx/{tx_digest}
```

#### Description
This endpoint retrieves information of the search request as per transaction digest or object id

#### Parameters

- `tx_digest/object_id` : The unique identifier of transaction digest or object id.

#### Example Request
```
curl --location https://kioskapp.venture23.xyz/api/v1/search/V4CpxhJhvLVaApoEhX2aNcQHkDacGFLUFyNW9Wsrzr3
```

#### Example Response
```
{
    "type":"Transaction",
    "data":"V4CpxhJhvLVaApoEhX2aNcQHkDacGFLUFyNW9Wsrzr3"
}
```



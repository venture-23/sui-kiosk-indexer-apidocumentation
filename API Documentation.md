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

| Status Code | Description             |
| :---------- | :---------------------- |
| 200         | `OK`                    |
| 201         | `CREATED`               |
| 400         | `BAD REQUEST`           |
| 404         | `NOT FOUND`             |
| 500         | `INTERNAL SERVER ERROR` |

- APIs
  - [Basic](#basic)
    - ReadOnly APIs
      - [Kiosks](#kiosks-list)
      - [Kiosk Detail](#get_kiosk_detail)
      - [Object Detail](#get_object_detail)
      - [Items](#get_items)
      - [Kiosk Items of Sui Address (Listed/Nonlisted)](#kiosk-items-of-sui-address)
      - [Summary Metric](#get_kiosk_summary)
      - [Kiosk Item History](#get_kiosk_item_history)
      - [Kiosk Transactions](#get_kiosk_transactions)
      - [Single Kiosk Transactions](#get_single_kiosk_transactions)
      - [Kiosk Extensions](#get_kiosk_extensions)
      - [Kiosk Profit Withdraws](#get_kiosk_profit_withdraws)
      - [Kiosk Graph](#get_kiosk_graph)
      - [Item Transfer Policies](#get_item_transfer_policies)
      - [Transaction Details](#get_transaction_details)
      - [Search](#search)

### Kiosks List

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

- `account` (optional): Get kiosks by account address.
- `filter.{profit/item_count}.min/max` (Optional): Filter kiosks in range between min and max field_name value. For instance, filter.profit.min=10&filter.profit.max=100, gets all kiosks containing profits between 10 and 100.
- `page.limit` (optional): The maximum number of kiosks to return per page. Default is 20.
- `page.next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.
- `sort.field` (optional): The field to sort the kiosks by. Possible values are fields in api response. Default is `-timestamp`,
- `sort.direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).

#### Example Request

```
curl --location 'https://kioskapp.venture23.xyz/api/v1/kiosks?page.limit=1&sort.field=item_count&sort.direction=desc&page.next_cursor=&filter.profit.min=10'
```

#### Example Response

```
{
    "data": [
        {
            "kiosk_id": "0xb9a4bb1d7d7666c78412e23123d2a86682fee7900fb4457b8eb6fe29e4e0fcfc",
            "version": "1299498",
            "owner": "0xc0a7b1e6c40870567c6f916bc578161823dfaec0cc6841622b124f15638fc792",
            "item_count": 3,
            "profit": 0.0,
            "created_at": 1722428177489,
            "mutated_at": 1722428212039
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 0,
        "next_cursor": "eyJsYXRlc3..",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```

### get_kiosk_detail

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
GET /items
```

#### Description

Retrieve information about items associated with a specific kiosk identified by its ID, with optional filtration, limit, sorting, and pagination.

#### Parameters

- `filter.kiosk_id` (optional): Get items of kiosk.
- `filter.collection` (optional): Filter kiosk items by item collection type.
- `filter.price.min/max` (optional): Filter listed items between listed price range.
- `sort.field` (optional): The field to sort the items by. Possible values are fields of item object,
- `sort.direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).
- `show` (optional): The field to filter item list by. Possible values are `all`, `listed`, `nonlisted`. Default: `all`
- `details` (optional): The field to get item list with or without item details. Possible values are `true`, `false`. Default: `true`.
- `page.limit` (optional): The maximum number of items to return per page. Default is 20.
- `page.next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.

#### Example Request

```
curl --location 'https://kioskapp.venture23.xyz/api/v1/items?page.limit=1&details=true&show=all&filter.kiosk_id=0x8c656964819fd6cd3b344483a7ad43744a506340bf1b1b6a99d34eded537ba2a&filter.price.min=18446744033.709553&filter.collection=0xe638169c0c173d069996cace570b44cf6cb48365c77a058cb4a9bf8ad757a51d::eggdeniyi::AfEggdeniyi&sort.field=_id&sort.direction=desc'
```

#### Example Response

```
{
    "data": [
        {
            "_id": "0xf76d49d05b513ffedbc6497d22d68845e03f9be6918ef265430de0b66c9598f9",
            "item_id": "0x991e0d499380c77cd71912803aebdc7a59a09dbe79f9bd5c3f8a4cb6060a2c97",
            "type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
            "kiosk_id": "0x8c656964819fd6cd3b344483a7ad43744a506340bf1b1b6a99d34eded537ba2a",
            "created_at": 1716459042633,
            "item_detail": {
                "object_id": "0x991e0d499380c77cd71912803aebdc7a59a09dbe79f9bd5c3f8a4cb6060a2c97",
                "type": "0xe638169c0c173d069996cace570b44cf6cb48365c77a058cb4a9bf8ad757a51d::eggdeniyi::AfEggdeniyi",
                "version": "39275391",
                "previous_transaction": "B9NMPMhrtfmfxhfHbZzWhqVQucNGrFcQrgL5dgFs1BkH",
                "fields": {
                    "id": {
                        "id": "0x991e0d499380c77cd71912803aebdc7a59a09dbe79f9bd5c3f8a4cb6060a2c97"
                    }
                }
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 0,
        "next_cursor": "eyJsYXR...",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```

### Kiosk Items of Sui Address

#### Overview

This API provides access to information about items inside all the kiosk of particular sui address.

#### Base URL

```
https://kioskapp.venture23.xyz/api/v1/
```

#### Endpoints

##### Get Kiosks

```
GET /account/{owner_id}/kiosk/items
```

#### Description

Retrieve a list of items in all the kiosk with optional filtering, sorting, and pagination.

#### Parameters

- `page.limit` (optional): The maximum number of kiosks to return per page. Default is 20.
- `sort.field` (optional): The field to sort the kiosks by. Possible values are all dynamic fields of item object like `name`, `description`, etc.. Default: `-mutated_at`,
- `sort.direction` (optional): The direction of sorting. Possible values are `asc` (ascending) and `desc` (descending).
- `page.next_cursor` (optional): Cursor for pagination. If provided, it retrieves the next page of results.
- `page.prev_cursor` (optional): Cursor for pagination. If provided, it retrieves the previous page of results.
- `show` (optional): The field to filter item list by. Possible values are `all`, `listed`, `nonlisted`. Default: `all`
- `details` (optional): The field to get item list with or without item details. Possible values are `true`, `false`. Default: `true`.

#### Example Request

```
curl --location 'https://kioskapp.venture23.xyz/api/v1/account/0xc0a7b1e6c40870567c6f916bc578161823dfaec0cc6841622b124f15638fc792/kiosk/items?page.limit=20&page.next_cursor=eyJpZCI6IjB4YmJhODFlNjgxZWI3NmViNjc0ZWNjZWNkYjBlNjIzMjUxOTRkYTQxMjMxYTFmNjViMTc5NTE5M2MwNDRiZDgxZSJ9&details=true&show=nonlisted&sort.field=name&sort.direction=asc
```

#### Example Response

```
{
    "data": [
        {
            "object_id": "0x16a648992a572d4a5850a3b87f9f4f030f7a7b3dcc7cf754673cf9ec4dc067b3",
            "item_id": "0x054e2051fa0d2f39f4fdc13c641348ac14fb682f23d41b2c0d0a3848dc1f58dd",
            "type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
            "kiosk_id": "0x2e49e8dd47577b27e4d386ae04e4c853150d43e5cf1af2382204c8700c442ccc",
            "created_at": 1720679299476,
            "item_detail": {
                "object_id": "0x054e2051fa0d2f39f4fdc13c641348ac14fb682f23d41b2c0d0a3848dc1f58dd",
                "type": "0xacc8056d9c5e4ff5d70a9bb87b078a540f77b4e7099702d4e002d4826c393841::nft::Sword",
                "version": "1173604",
                "previous_transaction": "BEMTHtzrKX5K47dBop7fg9oWjCXK81GrBzi23h5vC6g4",
                "fields": {
                    "description": "Selling Rare NFT",
                    "id": {
                        "id": "0x054e2051fa0d2f39f4fdc13c641348ac14fb682f23d41b2c0d0a3848dc1f58dd"
                    },
                    "name": "Kiosk NFT",
                    "strength": "50",
                    "url": "https://img.freepik.com/free-vector/hand-drawn-nft-style-ape-illustration_23-2149622021.jpg"
                }
            }
        },
        {
            "object_id": "0x17da9a64154adec159cdd22b132529b606bb3f1de84c678af7db42e5843e6439",
            "item_id": "0x65d91dd40c36a4753f2e62cc83331da7a5bd1cd4bfc98b3c6aaad762478e0272",
            "type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
            "kiosk_id": "0xac06e8500db047bf13429fceed20c92a4d5ee0559be932d2ba1112aa4327632f",
            "created_at": 1720679330593,
            "item_detail": {
                "object_id": "0x65d91dd40c36a4753f2e62cc83331da7a5bd1cd4bfc98b3c6aaad762478e0272",
                "type": "0xacc8056d9c5e4ff5d70a9bb87b078a540f77b4e7099702d4e002d4826c393841::nft::Sword",
                "version": "1173616",
                "previous_transaction": "GGqRvLtSPEdeQ7tm3TnHZvr9bNgGydYTPqNNgh7Rjv9w",
                "fields": {
                    "description": "Selling Rare NFT",
                    "id": {
                        "id": "0x65d91dd40c36a4753f2e62cc83331da7a5bd1cd4bfc98b3c6aaad762478e0272"
                    },
                    "name": "Kiosk NFT",
                    "strength": "50",
                    "url": "https://img.freepik.com/free-vector/hand-drawn-nft-style-ape-illustration_23-2149622021.jpg"
                }
            }
        },
        {
            "object_id": "0x1ea8ad577937856820d166973d79a35231636ee5a2809ce8630b9d3ae1f8164a",
            "item_id": "0xc9e8bd692105016a4a63d8b532ca211602058657019b2799cc305cad14ae8616",
            "type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
            "kiosk_id": "0x2e49e8dd47577b27e4d386ae04e4c853150d43e5cf1af2382204c8700c442ccc",
            "created_at": 1720679322404,
            "item_detail": {
                "object_id": "0xc9e8bd692105016a4a63d8b532ca211602058657019b2799cc305cad14ae8616",
                "type": "0xacc8056d9c5e4ff5d70a9bb87b078a540f77b4e7099702d4e002d4826c393841::nft::Sword",
                "version": "1173613",
                "previous_transaction": "EYJdMgastyuWRC3aPmU5rm4pR7ApXV4HfFwUWPD5LraH",
                "fields": {
                    "description": "Selling Rare NFT",
                    "id": {
                        "id": "0xc9e8bd692105016a4a63d8b532ca211602058657019b2799cc305cad14ae8616"
                    },
                    "name": "Kiosk NFT",
                    "strength": "50",
                    "url": "https://img.freepik.com/free-vector/hand-drawn-nft-style-ape-illustration_23-2149622021.jpg"
                }
            }
        },
        {
            "object_id": "0x49ed48aeba07a4a0f778ff904915fbc98f2fbb971dfd66270836efca28b0fda8",
            "item_id": "0xaf5d1140e4e0c926a7d3ed25b7b8d74c4d94a5713e0adf41d7581cf1607a4358",
            "type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
            "kiosk_id": "0x2e49e8dd47577b27e4d386ae04e4c853150d43e5cf1af2382204c8700c442ccc",
            "created_at": 1720679317575,
            "item_detail": {
                "object_id": "0xaf5d1140e4e0c926a7d3ed25b7b8d74c4d94a5713e0adf41d7581cf1607a4358",
                "type": "0xacc8056d9c5e4ff5d70a9bb87b078a540f77b4e7099702d4e002d4826c393841::nft::Sword",
                "version": "1173611",
                "previous_transaction": "FSXbTDaiBj4bpzTfgyccNGQFHSi533RHVSw32zsFjAWr",
                "fields": {
                    "description": "Selling Rare NFT",
                    "id": {
                        "id": "0xaf5d1140e4e0c926a7d3ed25b7b8d74c4d94a5713e0adf41d7581cf1607a4358"
                    },
                    "name": "Kiosk NFT",
                    "strength": "50",
                    "url": "https://img.freepik.com/free-vector/hand-drawn-nft-style-ape-illustration_23-2149622021.jpg"
                }
            }
        },
        {
            "object_id": "0x86667ec3e40f94f5f8226b0e07ac028ca3215bb1a8013b70081ae1655e2f4c31",
            "item_id": "0x6f707e5a7a3f9289855006c79d13394634a1b82c9869055b406b210bcfc7e7fb",
            "type": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
            "kiosk_id": "0x2e49e8dd47577b27e4d386ae04e4c853150d43e5cf1af2382204c8700c442ccc",
            "created_at": 1720679311795,
            "item_detail": {
                "object_id": "0x6f707e5a7a3f9289855006c79d13394634a1b82c9869055b406b210bcfc7e7fb",
                "type": "0xacc8056d9c5e4ff5d70a9bb87b078a540f77b4e7099702d4e002d4826c393841::nft::Sword",
                "version": "1173609",
                "previous_transaction": "FXnWbmCePBDmQBgmjNQmp1KUuCADY3WrDA1qqXa5a76d",
                "fields": {
                    "description": "Selling Rare NFT",
                    "id": {
                        "id": "0x6f707e5a7a3f9289855006c79d13394634a1b82c9869055b406b210bcfc7e7fb"
                    },
                    "name": "Kiosk NFT",
                    "strength": "50",
                    "url": "https://img.freepik.com/free-vector/hand-drawn-nft-style-ape-illustration_23-2149622021.jpg"
                }
            }
        }
    ],
    "page_info": {
        "limit": 20,
        "total": 0,
        "next_cursor": "eyJpZCI6IjB4YmJhODFlNjgxZWI3NmViNjc0ZWNjZWNkYjBlNjIzMjUxOTRkYTQxMjMxYTFmNjViMTc5NTE5M2MwNDRiZDgxZSJ9",
        "prev_cursor": null,
        "direction": "Next"
    }
}

```

### get_object_detail

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
        ..
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

##### Get Kiosk Transactions

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

### get_kiosk_summary

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

### get_kiosk_item_history

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

### get_kiosk_profit_withdraws

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

- `kiosk_id` (required): The ID of the kiosk for which you want to retrieve withdrawal information.
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

### get_kiosk_extensions

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

### get_kiosk_graph

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

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
      - [kiosks](#get_kiosks)
      - [kiosk detail](#get_kiosk_details)
      - [item detail](#get_item_detail)
      - [items](#get_items)
      - [summary metric](#get_summary_metrics)
      - [kiosk item history](#get_kiosk_item_history)
      - [kiosk transactions](#get_kiosk_transactions)
      - [kiosk creation in range](#get_kiosk_creation_in_range)
      - [kiosk profit withdraws](#get_kiosk_profit_withdraws)
      - [item transfer policies](#get_item_transfer_policies)
      - [kiosk extensions](#get_kiosk_extensions)

### get_kiosks

Returns all kiosks.

```http
GET /api/v1/kiosks
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/kiosks?limit=1&sort_by=items&direction=desc&next_cursor=&prev_cursor='
```

_Parameters:_

| Name        | Type | Description                                            |
| :---------- | :--- | :----------------------------------------------------- |
| limit       | str  | Total number of kiosk to list (max is 100, default 20) |
| sort_by     | str  | Sort response as per input (items/profit)              |
| direction   | str  | (items/profit)                                         |
| next_cursor | str  |                                                        |
| prev_cursor | str  |                                                        |

#### A paginated collection of kiosks

```
{
    "data": [
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
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 183,
        "next_cursor": "ewAAABJvYmplY3QuY29udGVudC5maWVsZHMuaXRlbV9jb3VudAAUAAAAAAAAAAJfaWQAQwAAADB4NzIwMzk2ZTZmOGNiMjJjNTM2MmViMjE2Mzg4NjMwMmE2ZTdkNzNmM2VlZTFiNzJmMWEzNWE2YTdkNjAxYmYyOAAA",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```

### get_kiosk_details

Returns information about single kiosk

```http
GET  /api/v1/kiosk/detail/<kiosk_id>
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/kiosk/detail/0x720396e6f8cb22c5362eb2163886302a6e7d73f3eee1b72f1a35a6a7d601bf28'
```

_Parameters:_

| Name     | Type | Description     |
| :------- | :--- | :-------------- |
| kiosk_id | str  | Kiosk object id |

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
```

### get_item_detail

Returns information about items

```http
GET /api/v1/item-details/<item_id>
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/item-details/0x26a1f6764fe4fc4b26ede6c3f27ca1c48c9484bf88d3bbc51ec36fedcdde651e'
```

_Parameters:_

| Name    | Type | Description    |
| :------ | :--- | :------------- |
| item_id | str  | Item object id |

#### A single item

```
{
    "id": "0x26a1f6764fe4fc4b26ede6c3f27ca1c48c9484bf88d3bbc51ec36fedcdde651e",
    "version": 1616995,
    "created_at": 1683159322188,
    "updated_at": null,
    "owner": "0xfaf1b99c273737e914da13324ee1191f42346643083892d3f6f09a2d246967e5",
    "previous_transaction": "Ej6yKKrQ12rV2UKjFLsDutk26EkhqKAYdTsZpwWWLqnP",
    "storage_rebate": 2971600,
    "type_": {
        "full": "0x2::dynamic_field::Field<0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>, 0x2::object::ID>",
        "package": "0x2",
        "module": "dynamic_field",
        "struct": "Field",
        "generics": [
            "0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>",
            "0x2::object::ID"
        ]
    },
    "ownership_type": "Object",
    "lock": null,
    "listing": null,
    "details": {
        "id": {
            "value": "0x26a1f6764fe4fc4b26ede6c3f27ca1c48c9484bf88d3bbc51ec36fedcdde651e"
        },
        "name": {
            "type_": "0x2::dynamic_object_field::Wrapper<0x2::kiosk::Item>",
            "fields": {
                "name": {
                    "type_": "0x2::kiosk::Item",
                    "fields": {
                        "id": {
                            "value": "0x58512cfd4a93afc37d082487e29ce2c47aed863d5a692930b799a95013f8e086"
                        }
                    }
                }
            }
        },
        "value": {
            "value": "0x58512cfd4a93afc37d082487e29ce2c47aed863d5a692930b799a95013f8e086"
        }
    }
}
```

### get_summary_metrics

Returns summary metric of kiosk

```http
GET /api/v1/kiosk/summary
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/kiosk/summary'


#### A sample response

```

{
"kiosks": 5987,
"extensions": 5940,
"items": 20747,
"profits": 439055810000,
"locked_items": 541,
"listed_items": 11
}

````

### get_kiosk_item_history

Returns the item history of kiosk [item details like action, timestamp, tx_digest]

```http
GET /api/v1/kiosk/<kiosk_id>/items/history
````

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/kiosk/0x17faabb98d3622d3a9a4a0c6bb980d03beaaf5a1985fd22c974728f38611beee/items/history'
```

_Parameters:_

| Name     | Type | Description     |
| :------- | :--- | :-------------- |
| kiosk_id | str  | Kiosk object id |

#### A sample response

```
{
    "0x17faabb98d3622d3a9a4a0c6bb980d03beaaf5a1985fd22c974728f38611beee": [
        {
            "action": "place",
            "timestamp": 1712625085011,
            "tx_digest": "4RX3de5VMZ2EN64NK3UQotpvmgiavtkc3x2jbtti6hrT"
        }
    ]
}
```

### get_kiosk_transactions

Returns the transactions related to kiosk

```http
GET /api/v1/kiosk/<kiosk_id>/transactions
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/kiosk/<kiosk_id>/transactions?limit=1&sort_by=items&direction=desc&next_cursor=&prev_cursor='
```

_Parameters:_

| Name     | Type | Description                                            |
| :------- | :--- | :----------------------------------------------------- |
| kiosk_id | str  | Kiosk object id                                        |
| limit    | int  | Total number of kiosk to list (max is 100, default 20) |
| module   | str  | kiosk                                                  |
| offset   | int  | offset value                                           |

#### A list of transaction details of kiosk

```
{
    "data": [
        {
            "tx_digest": "14AsQZEQCad6utqNKHjJVwb5zpzuNVpZpv37Nw1tSNUt",
            "tx_sender": "0x16b80901b9e6d3c8b5f54dc8a414bb1a75067db897e7a3624793176b97445ec6",
            "kind": "ProgrammableTransaction",
            "checkpoint_number": 188437,
            "timestamp": 1712660536502,
            "module": "kiosk",
            "function_name": "lock",
            "executed_epoch": 183,
            "status": true,
            "input": [
                {
                    "type": "object",
                    "mutable": true,
                    "objectId": "0x720396e6f8cb22c5362eb2163886302a6e7d73f3eee1b72f1a35a6a7d601bf28",
                    "objectType": "sharedObject",
                    "initialSharedVersion": "95"
                },
                {
                    "type": "object",
                    "digest": "7bt8DR7LoWsMv3ds8NFZLinvKWF8HHNYTF8tKT7zN7mi",
                    "version": "115",
                    "objectId": "0xa9a26bbd94cb29cd5714e8794e5cfe3e8200792527e591e0df61177062308a6c",
                    "objectType": "immOrOwnedObject"
                },
                {
                    "type": "object",
                    "mutable": false,
                    "objectId": "0x833caed5558ba15dae806f41a27a7f39cd4a9ebb88d0744935b7e6710df123eb",
                    "objectType": "sharedObject",
                    "initialSharedVersion": "94"
                },
                {
                    "type": "object",
                    "digest": "9cuT4KfHZHeE3TA4LhzEo1vDocprSGHiTV5SfZMRUzru",
                    "version": "108",
                    "objectId": "0xc82103b233965890c1770f5d304bab60dc5795be67bc39c4cb45ae09bdc3bfc2",
                    "objectType": "immOrOwnedObject"
                }
            ],
            "args": [
                "Input(0)",
                "Input(1)",
                "Input(2)",
                "Input(3)"
            ],
            "type_args": [
                "0xcf72c34e33799861c2ab7d1395b1eb011479bdf429cc9cafb80ec51adc07dc19::nft::Sword"
            ],
            "price": 1000,
            "budget": 7935600,
            "computation_cost": 1000000,
            "storage_rebate": 5492520,
            "non_refundable_storage_fee": 55480
        }
    ],
    "page_info": {
        "limit": 1,
        "offset": 2,
        "total": 20
    }
}
```

### get_kiosk_creation_in_range

Returns information about the kiosk

```http
GET /api/v1/kiosk/detail/<kiosk_id>
```

cURL

```
curl --location 'http://10.10.10.1:8085api/v1/kiosk/detail/<kiosk_id>'
```

_Parameters:_

| Name | Type | Description                                      |
| :--- | :--- | :----------------------------------------------- |
| type | str  | The information about the parameter and its type |

#### A single kiosk

```
{
    "data": {
        "id": 1,
        "name": "Shane Berry",
        "email": "shane@berry.com"
        "created_at": "2015-03-02T12:59:02+0100",
        "updated_at": "2015-03-04T15:50:40+0100"
    }
}
```

### get_kiosk_profit_withdraws

Returns withdraw details of kiosk

```http
GET /api/v1/kiosk/<kiosk_id>/withdrawls
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/kiosk/<kiosk_id>/withdrawls'
```

_Parameters:_

| Name     | Type | Description     |
| :------- | :--- | :-------------- |
| kiosk_id | str  | Kiosk object id |

#### Kiosk withdraw response

```
{
    "total": 0,
    "history": []
}
```

### get_item_transfer_policies

Returns item policies related to the particular items

```http
GET /api/v1/item-policy/<item_id>
```

cURL

```
curl --location 'http://10.10.10.1:8085/api/v1/item-policy/0x56e8934630d3e227ac0328fa8b22e100336023dd341d0709bb526df69b033cdc'
```

_Parameters:_

| Name        | Type | Description                                            |
| :---------- | :--- | :----------------------------------------------------- |
| item_id     | str  | Item object id                                         |
| limit       | str  | Total number of kiosk to list (max is 100, default 20) |
| sort_by     | str  | Sort response as per input (items/profit)              |
| direction   | str  | (items/profit)                                         |
| next_cursor | str  |                                                        |
| prev_cursor | str  |                                                        |

#### A list of transfer policies for an item

```
{
    "data": [
        {
            "id": "0x56e8934630d3e227ac0328fa8b22e100336023dd341d0709bb526df69b033cdc",
            "version": 151,
            "created_at": 1712661673580,
            "updated_at": 1712661693245,
            "type": {
                "full": "0x2::transfer_policy::TransferPolicy<0x537f947bd9b7ce12a4061ea2fa1b40debff1b3fc27b61265fb718107e6f983e3::nft::Sword>",
                "package": "0x2",
                "module": "transfer_policy",
                "struct": "TransferPolicy",
                "generics": [
                    "0x537f947bd9b7ce12a4061ea2fa1b40debff1b3fc27b61265fb718107e6f983e3::nft::Sword"
                ]
            },
            "owner": null,
            "ownership_type": "Shared",
            "initial_shared_version": 148,
            "storage_rebate": 2477600,
            "last_tx_block": "CLQm1LkpdV3d2MWr1mXVYjZmDoeijosH3ERJ3N56PFCf",
            "fields": {
                "balance": {
                    "value": "0"
                },
                "id": {
                    "value": "0x56e8934630d3e227ac0328fa8b22e100336023dd341d0709bb526df69b033cdc"
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
                                            "value": "537f947bd9b7ce12a4061ea2fa1b40debff1b3fc27b61265fb718107e6f983e3::royalty_policy::Rule"
                                        }
                                    }
                                }
                            ]
                        }
                    }
                }
            },
            "ownership_cap": {
                "id": "0x7259e74d3c798dad1e08339c44bf9fc2f72f59b9332e3caae2c99fef0501c7c9",
                "version": 151,
                "created_at": 1712661673580,
                "updated_at": 1712661693245,
                "type": {
                    "full": "0x2::transfer_policy::TransferPolicyCap<0x537f947bd9b7ce12a4061ea2fa1b40debff1b3fc27b61265fb718107e6f983e3::nft::Sword>",
                    "package": "0x2",
                    "module": "transfer_policy",
                    "struct": "TransferPolicyCap",
                    "generics": [
                        "0x537f947bd9b7ce12a4061ea2fa1b40debff1b3fc27b61265fb718107e6f983e3::nft::Sword"
                    ]
                },
                "owner": "0x16b80901b9e6d3c8b5f54dc8a414bb1a75067db897e7a3624793176b97445ec6",
                "ownership_type": "Address",
                "initial_shared_version": null,
                "storage_rebate": 2014000,
                "last_tx_block": "CLQm1LkpdV3d2MWr1mXVYjZmDoeijosH3ERJ3N56PFCf",
                "fields": {
                    "id": {
                        "value": "0x7259e74d3c798dad1e08339c44bf9fc2f72f59b9332e3caae2c99fef0501c7c9"
                    },
                    "policy_id": {
                        "value": "0x56e8934630d3e227ac0328fa8b22e100336023dd341d0709bb526df69b033cdc"
                    }
                }
            }
        }
    ],
    "page_info": {
        "limit": 1,
        "total": 1,
        "next_cursor": "UQAAAAJfaWQAQwAAADB4NTZlODkzNDYzMGQzZTIyN2FjMDMyOGZhOGIyMmUxMDAzMzYwMjNkZDM0MWQwNzA5YmI1MjZkZjY5YjAzM2NkYwAA",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```

### get_kiosk_extensions

Returns all the kiosk extensions of the given kiosk

```http
GET /api/v1/kiosks/<kiosk_id>/extensions
```

cURL

```
curl --location 'http://10.10.10.1:8085//api/v1/kiosks/<kiosk_id>/extensions'
```

_Parameters:_

| Name     | Type | Description     |
| :------- | :--- | :-------------- |
| kiosk_id | str  | Kiosk object id |

#### A list of kiosk extensions

```
{
    "data": [
        {
            "id": "0x59cf9a87fce817ae7c4c26b620bd778a81ade12c4fe3ec299362b5f2080c27aa",
            "version": 12,
            "created_at": null,
            "updated_at": null,
            "type": {
                "full": "0x2::dynamic_field::Field<0x2::kiosk_extension::ExtensionKey<0xf0d9c16afcc81c7ae0bdbf3b040feb1928272883649fb4ae5650c2d8eeee0e13::marketplace::Ext>, 0x2::kiosk_extension::Extension>",
                "package": "0x2",
                "module": "dynamic_field",
                "struct": "Field",
                "generics": [
                    "0x2::kiosk_extension::ExtensionKey<0xf0d9c16afcc81c7ae0bdbf3b040feb1928272883649fb4ae5650c2d8eeee0e13::marketplace::Ext>",
                    "0x2::kiosk_extension::Extension"
                ]
            },
            "owner": "0x133304517ae77914cdcda1df11666c1187c33004a36d4d809595fddeeac54dc7",
            "ownership_type": "Object",
            "initial_shared_version": null,
            "storage_rebate": 3085600,
            "last_tx_block": "EZWNXc2Vh3bzbraVvpcSKZhcCrsXeqWhKqMjUEGKUkqk",
            "fields": {
                "id": {
                    "value": "0x59cf9a87fce817ae7c4c26b620bd778a81ade12c4fe3ec299362b5f2080c27aa"
                },
                "name": {
                    "type_": "0x2::kiosk_extension::ExtensionKey<0xf0d9c16afcc81c7ae0bdbf3b040feb1928272883649fb4ae5650c2d8eeee0e13::marketplace::Ext>",
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
                                    "value": "0x3bcdf11db5d0c21d5ec508a0e3cbba7b51e3ec15263296a2146aab5066f10186"
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
        "next_cursor": "UQAAAAJfaWQAQwAAADB4NTljZjlhODdmY2U4MTdhZTdjNGMyNmI2MjBiZDc3OGE4MWFkZTEyYzRmZTNlYzI5OTM2MmI1ZjIwODBjMjdhYQAA",
        "prev_cursor": null,
        "direction": "Next"
    }
}
```

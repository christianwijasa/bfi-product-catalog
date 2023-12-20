# Category API

## Category Properties

### Categories

| No. | Name               | Data Type | Description                |
|-----|--------------------|-----------|----------------------------|
| 1.  | category_id        | UUID      | Category's ID              |
| 2.  | parent_category_id | UUID      | Category's Parent ID       |
| 3.  | name               | String    | Category's name            |
| 4.  | created_at         | Timestamp | Time category created      |
| 5.  | updated_at         | Timestamp | Time category last updated |
| 6.  | deleted_at         | Timestamp | Time category deleted      |

## Get category list

### This API is used to get category list. Returns 200 OK even though category is empty
### Store API response to Redis with request as key. Expiry 1 day

`[GET] /api/v1/category`

### Request

| No. | Name  | Required | Data Type | Description                         |
|-----|-------|----------|-----------|-------------------------------------|
| 1.  | page  | FALSE    | Integer   | Page of categories (Default 1)      |
| 2.  | limit | FALSE    | Integer   | Limit item to retrieve (Default 20) |

### Response

```json
{
  "data": {
    "categories": [
      {
        "category_id": "",
        "parent_category_id": "",
        "name": "",
        "created_at": "2023-12-31 00:00:00",
        "updated_at": "2023-12-31 00:00:00",
        "deleted_at": null
      }
    ],
    "page": 1,
    "limit": 20,
    "total": 100,
    "last": false
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description   |
|-----|--------|---------------|
| 1.  | CAT000 | Unknown error |

## Create category

### This API is used to create category

`[POST] /api/v1/category`

### Request

| No. | Name               | Required | Data Type | Description          |
|-----|--------------------|----------|-----------|----------------------|
| 1.  | parent_category_id | FALSE    | UUID      | Category's parent ID |
| 2.  | name               | TRUE     | String    | Category's name      |

```json
{
  "parent_category_id": null,
  "name": ""
}
```

### Response

```json
{
  "data": {
    "category_id": "",
    "parent_category_id": null,
    "name": "",
    "created_at": "2023-12-31 00:00:00",
    "updated_at": "2023-12-31 00:00:00",
    "deleted_at": null
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description                             |
|-----|--------|-----------------------------------------|
| 1.  | CAT000 | Unknown error                           |
| 2.  | CAT200 | Bad request : parent category not found |

## Update category

### This API is used to update category

`[PATCH] /api/v1/category/{category_id}`

### Request

| No. | Name               | Type | Required | Data Type | Description                    |
|-----|--------------------|------|----------|-----------|--------------------------------|
| 1.  | category_id        | PATH | TRUE     | UUID      | Category's ID                  |
| 2.  | parent_category_id | JSON | FALSE    | String    | To change category's parent ID |
| 3.  | name               | JSON | FALSE    | String    | To change category's name      |

```json
{
  "category_id": "",
  "parent_category_id": null,
  "name": ""
}
```

### Response

```json
{
  "data": {
    "category_id": "",
    "parent_category_id": null,
    "name": "",
    "created_at": "2023-12-31 00:00:00",
    "updated_at": "2023-12-31 00:00:00",
    "deleted_at": null
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description                                                                                 |
|-----|--------|---------------------------------------------------------------------------------------------|
| 1.  | CAT000 | Unknown error                                                                               |
| 2.  | CAT300 | Bad request : category not found                                                            |
| 3.  | CAT301 | Bad request : parent category not found                                                     |
| 4.  | CAT302 | Bad request : name is required (this only happened if parent category id and name are null) |

## Create bulk categories

### This API is used to create multiple categories

`[POST] /api/v1/category/bulk`

### Request

| No. | Name     | Required | Data Type       | Description         |
|-----|----------|----------|-----------------|---------------------|
| 1.  | name     | TRUE     | UUID            | Category's ID       |
| 2.  | children | FALSE    | Array of String | Children categories |

```json
[
  {
    "name": "",
    "children": [
      ""
    ]
  }
]
```

### Response

```json
{
  "data": [
    {
      "category_id": "",
      "parent_category_id": null,
      "name": "",
      "created_at": "2023-12-31 00:00:00",
      "updated_at": "2023-12-31 00:00:00",
      "deleted_at": null
    },
  ],
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description   |
|-----|--------|---------------|
| 1.  | CAT000 | Unknown error |

## Deactivate category

### This API is used to deactivate category

`[POST] /api/v1/category/{category_id}`

### Request

| No. | Name        | Required | Data Type | Description                              |
|-----|-------------|----------|-----------|------------------------------------------|
| 1.  | category_id | TRUE     | Integer   | Category ID that wants to be deactivated |

### Response

```json
{
  "data": {
    "category_id": "",
    "deleted_at": "2023-12-31 00:00:00"
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description                      |
|-----|--------|----------------------------------|
| 1.  | CAT000 | Unknown error                    |
| 2.  | CAT500 | Bad request : category not found |

# Product API

## Product Properties

### Products

| No. | Name        | Data Type | Description               |
|-----|-------------|-----------|---------------------------|
| 1.  | product_id  | UUID      | Product's ID              |
| 2.  | name        | String    | Product's name            |
| 3.  | category_id | UUID      | Product's category ID     |
| 4.  | image       | String    | Product's image           |
| 5.  | created_at  | Timestamp | Time product created      |
| 6.  | updated_at  | Timestamp | Time product last updated |
| 7.  | deleted_at  | Timestamp | Time product deleted      |

### Variants

| No. | Name       | Data Type | Description               |
|-----|------------|-----------|---------------------------|
| 1.  | variant_id | UUID      | Variant's ID              |
| 2.  | sku        | String    | Variant's SKU             |
| 3.  | stock      | Integer   | Variant's stock           |
| 4.  | price      | Double    | Variant's price           |
| 5.  | image      | String    | Variant's image           |
| 6.  | attributes | Array     | Variant's attributes      |
| 7.  | created_at | Timestamp | Time variant created      |
| 8.  | updated_at | Timestamp | Time variant last updated |
| 9.  | deleted_at | Timestamp | Time variant deleted      |

## Get product list

### This API is used to get product list. Returns 200 OK even though product is empty.
### Store API response to Redis with request as key. Expiry 1 day

`[GET] /api/v1/product`

### Request

| No. | Name         | Required | Data Type     | Description                         |
|-----|--------------|----------|---------------|-------------------------------------|
| 1.  | page         | FALSE    | Integer       | Page of products (Default 1)        |
| 2.  | limit        | FALSE    | Integer       | Limit item to retrieve (Default 20) |
| 3.  | name         | FALSE    | String        | Search by product name              |
| 4.  | category_ids | FALSE    | Array of UUID | Filter by category ids              |
| 5.  | is_active    | TRUE     | Boolean       | Filter by active products           |

### Response

```json
{
  "data": {
    "products": [
      {
        "product_id": "",
        "name": "",
        "category_id": "",
        "image": "",
        "is_active": true,
        "created_at": "2023-12-31 00:00:00",
        "updated_at": "2023-12-31 00:00:00",
        "deleted_at": null
      }
    ],
    "page": 1,
    "limit": 20,
    "total": 100,
    "last": false
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description   |
|-----|--------|---------------|
| 1.  | PRD000 | Unknown error |

## Get product variants by IDs

### This API is used to get product variants by IDs

`[GET] /api/v1/product/{product_id}`

### Request

| No. | Name       | Required | Data Type | Description          |
|-----|------------|----------|-----------|----------------------|
| 1.  | product_id | TRUE     | UUID      | Search by product id |

### Response

```json
{
  "data": {
    "variants": [
      {
        "variant_id": "",
        "sku": "",
        "stock": 10,
        "price": 10000,
        "image": "",
        "attributes": [
          "key": "value"
        ],
        "created_at": "2023-12-31 00:00:00",
        "updated_at": "2023-12-31 00:00:00",
        "deleted_at": null
      }
    ]
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description       |
|-----|--------|-------------------|
| 1.  | PRD000 | Unknown error     |
| 2.  | PRD200 | Product not found |

## Create product

### This API is used to create product

`[POST] /api/v1/product`

### Request

| No. | Name                | Required | Data Type | Description                                           |
|-----|---------------------|----------|-----------|-------------------------------------------------------|
| 1.  | category_id         | TRUE     | UUID      | Product's category ID ([Category API](#category-api)) |
| 2.  | name                | TRUE     | String    | Product's name                                        |
| 3.  | image               | TRUE     | String    | Product's image                                       |
| 4.  | variants            | TRUE     | Array     | Product's variants                                    |
| 5.  | variants.sku        | TRUE     | String    | Variant's SKU                                         |
| 6.  | variants.stock      | TRUE     | Integer   | Variant's stock                                       |
| 7.  | variants.price      | TRUE     | Double    | Variant's price                                       |
| 8.  | variants.image      | TRUE     | String    | Variant's image                                       |
| 9.  | variants.attributes | FALSE    | Array     | Variant's attributes with custom key value            |
| 10. | is_active           | TRUE     | Boolean   | Product's activation                                  |

```json
{
  "category_id": "",
  "name": "",
  "image": "",
  "variants": [
    {
      "sku": "",
      "stock": 10,
      "price": 10000,
      "image": "",
      "attributes": [
        "key": "value"
      ]
    }
  ],
  "is_active": true
}
```

### Response

```json
{
  "data": {
    "product_id": "",
    "name": "",
    "category_id": "",
    "image": "",
    "variants": [
      {
        "variant_id": "",
        "sku": "",
        "stock": 10,
        "price": 10000,
        "image": "",
        "attributes": [
          "key": "value"
        ],
        "created_at": "2023-12-31 00:00:00",
        "updated_at": "2023-12-31 00:00:00",
        "deleted_at": null
      }
    ],
    "is_active": true,
    "created_at": "2023-12-31 00:00:00",
    "updated_at": "2023-12-31 00:00:00",
    "deleted_at": null
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description                          |
|-----|--------|--------------------------------------|
| 1.  | PRD000 | Unknown error                        |
| 2.  | PRD300 | Bad request : category not found     |
| 3.  | PRD301 | Bad request : product already exists |
| 4.  | PRD302 | Bad request : invalid image          |

## Update Product

### This API is used to update product

`[PATCH] /api/v1/product/{product_id}`

### Request

| No. | Name                | Type | Required | Data Type | Description                                           |
|-----|---------------------|------|----------|-----------|-------------------------------------------------------|
| 1.  | product_id          | Path | TRUE     | UUID      | Product ID to update                                  |
| 2.  | category_id         | JSON | FALSE    | UUID      | Product's category ID ([Category API](#category-api)) |
| 3.  | name                | JSON | FALSE    | String    | Product's name                                        |
| 4.  | image               | JSON | FALSE    | String    | Product's image                                       |
| 5.  | variants            | JSON | FALSE    | Array     | Product's variants                                    |
| 6.  | variants.sku        | JSON | TRUE     | String    | Variant's SKU                                         |
| 7.  | variants.stock      | JSON | FALSE    | Integer   | Variant's stock                                       |
| 8.  | variants.price      | JSON | FALSE    | Double    | Variant's price                                       |
| 9.  | variants.image      | JSON | FALSE    | String    | Variant's image                                       |
| 10. | variants.attributes | JSON | FALSE    | ARRAY     | Variant's attributes with custom key value            |
| 11. | is_active           | JSON | FALSE    | Boolean   | Product's activation                                  |

```json
{
  "category_id": "",
  "name": "",
  "image": "",
  "variants": [
    {
      "variant_id": "",
      "sku": "",
      "stock": 10,
      "price": 10000,
      "attributes": [
        "key": "value"
      ]
    }
  ],
  "is_active": true
}
```

### Response

```json
{
  "data": {
    "product_id": "",
    "name": "",
    "category_id": "",
    "image": "",
    "variants": [
      {
        "variant_id": "",
        "sku": "",
        "stock": 10,
        "price": 10000,
        "image": "",
        "attributes": [
          "key": "value"
        ],
        "created_at": "2023-12-31 00:00:00",
        "updated_at": "2023-12-31 00:00:00",
        "deleted_at": null
      }
    ],
    "is_active": true,
    "created_at": "2023-12-31 00:00:00",
    "updated_at": "2023-12-31 00:00:00",
    "deleted_at": null
  },
  "error_code": "",
  "message": ""
}
```

### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

### Error Codes

| No. | Name   | Description                          |
|-----|--------|--------------------------------------|
| 1.  | PRD000 | Unknown error                        |
| 2.  | PRD400 | Bad request : category not found     |
| 3.  | PRD401 | Bad request : product already exists |
| 4.  | PRD402 | Bad request : invalid image          |

# External API

## Authenticate

### This API is used to authenticate user based on given client id and secret

`[POST] /api/v1/authenticate`

### Request

`Header : Authorization Basic base64(clientId:clientSecret)`

### Response
```json
{
  "token": "",
  "type": "Bearer",
  "expiry": "2023-12-31 00.00.00"
}
```

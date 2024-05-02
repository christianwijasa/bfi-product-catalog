# API Design

## Category API

### Category Properties

#### Categories

| No. | Name               | Data Type | Description                |
|-----|--------------------|-----------|----------------------------|
| 1.  | category_id        | UUID      | Category's ID              |
| 2.  | parent_category_id | UUID      | Category's Parent ID       |
| 3.  | name               | String    | Category's name            |
| 4.  | created_at         | Timestamp | Time category created      |
| 5.  | updated_at         | Timestamp | Time category last updated |
| 6.  | deleted_at         | Timestamp | Time category deleted      |

### Get category list

> [!NOTE]
> This API is used to get category list. Returns 200 OK even though category is empty
> Store API response to Redis with request as key. Expiry 1 day

`[GET] /api/v1/category`

#### Request

| No. | Name  | Required | Data Type | Description                         |
|-----|-------|----------|-----------|-------------------------------------|
| 1.  | page  | FALSE    | Integer   | Page of categories (Default 1)      |
| 2.  | limit | FALSE    | Integer   | Limit item to retrieve (Default 20) |

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description   |
|-----|--------|-------------|---------------|
| 1.  | CAT000 | 500         | Unknown error |

### Create category

> [!NOTE]
> This API is used to create category

`[POST] /api/v1/category`

#### Request

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

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                             |
|-----|--------|-------------|-----------------------------------------|
| 1.  | CAT000 | 500         | Unknown error                           |
| 2.  | CAT200 | 400         | Bad request : parent category not found |

### Update category

> [!NOTE]
> This API is used to update category

`[PATCH] /api/v1/category/{category_id}`

#### Request

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

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                                                                                 |
|-----|--------|-------------|---------------------------------------------------------------------------------------------|
| 1.  | CAT000 | 500         | Unknown error                                                                               |
| 2.  | CAT300 | 400         | Bad request : category not found                                                            |
| 3.  | CAT301 | 400         | Bad request : parent category not found                                                     |
| 4.  | CAT302 | 400         | Bad request : name is required (this only happened if parent category id and name are null) |

### Create bulk categories

> [!NOTE]
> This API is used to create multiple categories

`[POST] /api/v1/category/bulk`

#### Request

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

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description   |
|-----|--------|-------------|---------------|
| 1.  | CAT000 | 500         | Unknown error |

### Deactivate category

> [!NOTE]
> This API is used to deactivate category

`[POST] /api/v1/category/{category_id}`

#### Request

| No. | Name        | Required | Data Type | Description                              |
|-----|-------------|----------|-----------|------------------------------------------|
| 1.  | category_id | TRUE     | Integer   | Category ID that wants to be deactivated |

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                      |
|-----|--------|-------------|----------------------------------|
| 1.  | CAT000 | 500         | Unknown error                    |
| 2.  | CAT500 | 400         | Bad request : category not found |

## Product API

### Product Properties

#### Products

| No. | Name        | Data Type | Description               |
|-----|-------------|-----------|---------------------------|
| 1.  | product_id  | UUID      | Product's ID              |
| 2.  | category_id | UUID      | Product's category ID     |
| 3.  | name        | String    | Product's name            |
| 4.  | image       | String    | Product's image           |
| 5.  | created_at  | Timestamp | Time product created      |
| 6.  | updated_at  | Timestamp | Time product last updated |
| 7.  | deleted_at  | Timestamp | Time product deleted      |

#### Variants

| No. | Name       | Data Type | Description                                                                                                 |
|-----|------------|-----------|-------------------------------------------------------------------------------------------------------------|
| 1.  | variant_id | UUID      | Variant's ID (this is required if the business will have multiple tenants)                                  |
| 2.  | sku        | String    | Variant's SKU (this can be primary key and remove variant id if the business only run one stand-alone shop) |
| 3.  | stock      | Integer   | Variant's stock                                                                                             |
| 4.  | price      | Double    | Variant's price                                                                                             |
| 5.  | image      | String    | Variant's image                                                                                             |
| 6.  | attributes | Array     | Variant's attributes                                                                                        |
| 7.  | created_at | Timestamp | Time variant created                                                                                        |
| 8.  | updated_at | Timestamp | Time variant last updated                                                                                   |
| 9.  | deleted_at | Timestamp | Time variant deleted                                                                                        |

### Get product list

> [!NOTE]
> This API is used to get product list. Returns 200 OK even though product is empty.
> Store API response to Redis with request as key. Expiry 1 day

`[GET] /api/v1/product`

#### Request

| No. | Name         | Required | Data Type     | Description                         |
|-----|--------------|----------|---------------|-------------------------------------|
| 1.  | page         | FALSE    | Integer       | Page of products (Default 1)        |
| 2.  | limit        | FALSE    | Integer       | Limit item to retrieve (Default 20) |
| 3.  | category_ids | FALSE    | Array of UUID | Filter by category ids              |
| 4.  | name         | FALSE    | String        | Search by product name              |
| 5.  | is_active    | TRUE     | Boolean       | Filter by active products           |

#### Response

```json
{
  "data": {
    "products": [
      {
        "product_id": "",
        "category_id": "",
        "name": "",
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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description   |
|-----|--------|-------------|---------------|
| 1.  | PRD000 | 500         | Unknown error |

### Get product variants by ID

> [!NOTE]
> This API is used to get product variants by ID

`[GET] /api/v1/product/{product_id}`

#### Request

| No. | Name       | Required | Data Type | Description          |
|-----|------------|----------|-----------|----------------------|
| 1.  | product_id | TRUE     | UUID      | Search by product id |

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description       |
|-----|--------|-------------|-------------------|
| 1.  | PRD000 | 500         | Unknown error     |
| 2.  | PRD200 | 404         | Product not found |

### Create product

> [!NOTE]
> This API is used to create product

`[POST] /api/v1/product`

#### Request

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

#### Response

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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                          |
|-----|--------|-------------|--------------------------------------|
| 1.  | PRD000 | 500         | Unknown error                        |
| 2.  | PRD300 | 400         | Bad request : category not found     |
| 3.  | PRD301 | 400         | Bad request : product already exists |
| 4.  | PRD302 | 400         | Bad request : invalid image          |

### Update Product

> [!NOTE]
> This API is used to update product

`[PATCH] /api/v1/product/{product_id}`

#### Request

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

#### Response

```json
{
  "data": {
    "product_id": "",
    "category_id": "",
    "name": "",
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

#### Error Response

```json
{
  "data": null,
  "error_code": "",
  "message": ""
}
```

#### Error Codes

| No. | Name   | HTTP Status | Description                          |
|-----|--------|-------------|--------------------------------------|
| 1.  | PRD000 | 500         | Unknown error                        |
| 2.  | PRD400 | 400         | Bad request : category not found     |
| 3.  | PRD401 | 400         | Bad request : product already exists |
| 4.  | PRD402 | 400         | Bad request : invalid image          |

## External API

### Authenticate

> [!NOTE]
> This API is used to authenticate user based on given client id and secret

`[POST] /api/v1/authenticate`

#### Request

`Header : Authorization Basic base64(clientId:clientSecret)`

#### Response
```json
{
  "token": "",
  "type": "Bearer",
  "expiry": "2023-12-31 00.00.00"
}
```

## Notes

1. Basically there are 3 crucial services:
- Product service (which documented here)
-- stock in this case should be implemented later in inventory service
- Order service
- Inventory service

2. When implementing order service, use message broker when doing several things:
- Notify user about order status
- Update stock to inventory service

3. For message broker implementation, can use this architecture to make sure all messages consumed
- https://microservices.io/patterns/data/transactional-outbox.html

---

# System Design

[![System Design](https://i.ibb.co/txPwv0w/Screenshot-2024-05-02-at-13-14-26.png)]

# Database Design

## ERD
[![ERD](https://i.ibb.co/MfnxHPL/Screenshot-2024-05-02-at-10-41-04.png)]

## Table
```sql
CREATE TABLE categories
(
  category_id         UUID NOT NULL,
  parent_category_id  UUID,
  name                TEXT NOT NULL,
  created_at          TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
  updated_at          TIMESTAMP WITH TIME ZONE,
  deleted_at          TIMESTAMP WITH TIME ZONE,
  deleted             BOOLEAN DEFAULT FALSE,
  
  CONSTRAINT categories_category_id_pkey PRIMARY KEY (id),
  CONSTRAINT categories_parent_category_id_fkey FOREIGN KEY (parent_category_id) REFERENCES categories(category_id)
);
CREATE INDEX IF NOT EXISTS categories__index_query_by_name ON categories (name);

CREATE TABLE products
(
  product_id  UUID NOT NULL,
  category_id UUID NOT NULL,
  name        TEXT NOT NULL,
  image       TEXT,
  is_active   BOOLEAN DEFAULT FALSE,
  created_at  TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
  updated_at  TIMESTAMP WITH TIME ZONE,
  deleted_at  TIMESTAMP WITH TIME ZONE,
  deleted     BOOLEAN DEFAULT FALSE,

  CONSTRAINT products_product_id_pkey PRIMARY KEY (product_id),
  CONSTRAINT products_category_id_fkey FOREIGN KEY (category_id) REFERENCES categories(category_id)
);
CREATE INDEX IF NOT EXISTS products__index_query_by_name ON products (name);

CREATE TABLE variants
(
  variant_id  UUID NOT NULL,
  product_id  UUID NOT NULL,
  sku         TEXT NOT NULL,
  stock       INTEGER DEFAULT 0,
  price       FLOAT DEFAULT 0,
  image       TEXT,
  attributes  JSONB,
  created_at  TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
  updated_at  TIMESTAMP WITH TIME ZONE,
  deleted_at  TIMESTAMP WITH TIME ZONE,
  deleted     BOOLEAN DEFAULT FALSE,

  CONSTRAINT variants_variant_id_pkey PRIMARY KEY (variant_id),
  CONSTRAINT variants_product_id_fkey FOREIGN KEY (product_id) REFERENCES products(product_id)
);
CREATE UNIQUE INDEX IF NOT EXISTS unique_products__sku ON products (sku);
```

## Queries

### [Get category list](#get-category-list)
```sql
SELECT category_id, parent_category_id, name, created_at, updated_at, deleted_at FROM categories LIMIT 20 OFFSET 0
```

### [Create category](#create-category)
```sql
INSERT INTO categories (parent_category_id, name) VALUES (?, ?)
```

### [Update category](#update-category)
```sql
UPDATE categories SET parent_category_id = ?, name = ?, updated_at = NOW() WHERE id = ?
```

### [Deactivate category](#deactivate-category)
```sql
UPDATE categories SET updated_at = NOW(), deleted_at = NOW(), deleted = TRUE WHERE id = ?
```

### [Get product list](#get-product-list)
```sql
SELECT product_id, category_id, name, image, is_active, created_at, updated_at, deleted_at FROM products LIMIT 20 OFFSET 0
```

### [Get variant](#get-product-variants-by-id)
```sql
SELECT variant_id, sku, stock, price, image, attributes, created_at, updated_at, deleted_at FROM variants WHERE product_id = ?
```

### [Create product](#create-product)
```sql
INSERT INTO products (category_id, name, image, is_active) VALUES (?, ?, ?, ?)
INSERT INTO variants (product_id, sku, stock, price, image, attributes) VALUES (?, ?, ?, ?, ?, ?)
```

### [Update product](#update-product)
```sql
UPDATE products SET category_id = ?, name = ?, image = ?, is_active = ?, updated_at = NOW() WHERE product_id = ?
UPDATE variants SET sku = ?, stock = ?, price = ?, image = ?, attributes = ?, updated_at = NOW() WHERE variant_id = ?
```

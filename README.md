# Woocommerce Stores Hub

## Introduction

**WooCommerce Stores Hub** API provides a range of functionalities for gathering data on WooCommerce stores. It allows users to retrieve details like product inventories, pricing, and stock status. Additionally, the API provides insights into store analytics, customer reviews, and metadata, making it valuable for tracking store performance, conducting market analysis, or integrating WooCommerce data with other systems. Users can leverage this API for monitoring e-commerce trends, centralizing store information, and supporting data-driven decision-making in their e-commerce operations.

## Authentication

The URL you need to use is the following: `https://woocommerce-stores-hub.p.rapidapi.com/`
The API requires the headers listed below:

- **`x-rapidapi-host`**: `woocommerce-stores-hub.p.rapidapi.com`
- **`x-rapidapi-key`**: `YOUR_API_KEY`

Make sure to replace `YOUR_API_KEY` with your API key. You can register one [here](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/woocommerce-stores-hub/pricing).
Some frameworks automatically add extra headers, you have to make sure to remove them in order to get a response from the API.

## Endpoints

The API is configured to accept only **GET** requests. Below are the available endpoints with their descriptions and required parameters.

### 1. **`GET /store/info`**

- **Description**: Retrieves detailed information about a specific store.

| Parameter | Type   | Default | Description                                       | Required |
|-----------|--------|---------|---------------------------------------------------|----------|
| `url`     | string | -       | The URL of the store to retrieve information for | Yes      |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/store/info?url=https%3A%2F%2Foscarwareinc.com', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": {
    "title": "Home of the Grill Topper - Oscarware Inc",
    "description": "Oscarware Grill Toppers are designed to cook smaller, more delicate foods as well as traditional favorites on the grill. Made in the USA",
    "url": {
      "url": "oscarwareinc.com",
      "canonicalURL": "https://oscarwareinc.com/"
    },
    "language": "en-US",
    "creationDate": "2003",
    "installedPlugins": [
      "getwid",
      "social-share-buttons-lite",
      "save-share-cart",
      "addify-abandoned-cart-recovery",
      "contact-form-7",
      "woocommerce",
      "wooswipe",
      "wp-menu-cart-pro",
      "shareasale-wc-tracker",
      "yotpo-social-reviews-for-woocommerce",
      "woocommerce-google-analytics-integration",
      "klaviyo",
      "woocommerce-extend-tabs"
    ],
    "socialMedia": {
      "instagram": "https://www.instagram.com/oscarwareinc/",
      "facebook": "https://www.facebook.com/oscarwareinc",
      "pinterest": "",
      "twitter": "",
      ...
```

### 2. **`GET /products/search`**

- **Description**: Allows you to search for products in a given store based on various parameters.

| Parameter | Type     | Default | Description                                  | Required |
|-----------|----------|---------|----------------------------------------------|----------|
| `url`     | string   | -       | The URL of the store to search products from | Yes      |
| `page`    | integer  | 1       | The page number of the results to retrieve   | No       |
| `perPage` | integer  | 14      | The number of results per page (max=70)      | No       |
| `query` * | string   | -       | The search term to filter products           | No       |
| `sku`   * | string   | -       | The SKU to filter products                   | No       |
| `onSale`  | boolean  | -       | Filter products that are on sale             | No       |
| `minPrice`| string   | -       | The minimum price to filter products         | No       |
| `maxPrice`| string   | -       | The maximum price to filter products         | No       |

*: Either `query` or `sku` must be provided. If both are missing, the request will return a 400 error with the message "Please provide either the query or the sku".

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/products/search?url=https%3A%2F%2Fkarminhairtools.com%2F&query=removal', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": [
    {
      "id": 616,
      "name": "Karmin Silk Series IPL Hair Removal Handset",
      "slug": "karmin-silk-series-ipl-hair-removal-handset",
      "parent": 0,
      "type": "variable",
      "variation": "",
      "permalink": "https://karminhairtools.com/product/karmin-silk-series-ipl-hair-removal-handset",
      "sku": "",
      "short_description": "",
      "description": "<p>The Karmin Silk Series is a Professional at Home IPL Hair Removal Device for Safe, Painless and Effective Permanent Hair Removal from the comfort of your home.</p>",
      "on_sale": false,
      "prices": {
        "price": "19995",
        "regular_price": "19995",
        "sale_price": "19995",
        "price_range": null,
        "currency_code": "USD",
        "currency_symbol": "$",
        "currency_minor_unit": 2,
        "currency_decimal_separator": ".",
        "currency_thousand_separator": ",",
        "currency_prefix": "$",
        "currency_suffix": ""
      },
      "price_html": "<span class=\"woocommerce-Price-amount amount\"><span class=\"woocommerce-Price-currencySymbol\">&#036;</span>199.95</span>",
      "average_rating": "0",
      "review_count": 0,
      ...
```

### 3. **`GET /products/reviews`**

- **Description**: Retrieves reviews for a specific product from a given store URL.

| Parameter   | Type    | Default | Description                                    | Required |
|-------------|---------|---------|------------------------------------------------|----------|
| `url`       | string  | -       | The URL of the store to retrieve reviews from   | Yes      |
| `productId` | string  | -       | The ID of the product to retrieve reviews for   | Yes      |
| `page`      | integer | 1       | The page number of the results to retrieve      | No       |
| `perPage`   | integer | 12      | The number of reviews per page (max=70)         | No       |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/products/reviews?url=https%3A%2F%2Fkarminhairtools.com&productId=615', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": [
    {
      "idReview": 567,
      "date_created": "2020-07-28T21:48:19",
      "formatted_date_created": "July 28, 2020",
      "product_id": 615,
      "reviewerName": "Sherry",
      "reviewText": "<p>Convenient hair removal and money well spent!</p>\n<p>Removes hair with ease (a bit of a pinch but who said hair removal was pain free) I love that I save money each month on waxing appointments. I recommend this for anyone who would rather remove their hair at home on their own time.</p>\n",
      "rating": 4,
      "verified": false,
      "reviewer_avatar_urls": "https://secure.gravatar.com/avatar/?s=96&d=mm&r=g"
    },
    {
      "idReview": 566,
      "date_created": "2020-07-28T21:46:58",
      "formatted_date_created": "July 28, 2020",
      "product_id": 615,
      "reviewerName": "Ashley",
      "reviewText": "<p>Game changer</p>\n<p>Probably one of the best things I have ever bought that’s also a self torture device. Yes it is painful and yes you have to work yourself up to it sometimes but it’s so worth it. I used to get so much razor burn and after using this I am bump free. The sensitive guard actually ‘lessens’ the pain but sometimes I take it off to get stubborn hairs around my bikini line, if you press too hard the red light comes on. I have tried other epilators and couldn’t even get past a few seconds with it, this one tops them all. I do my arms, legs, armpits, and down there. I’d also say that my arms and legs don’t hurt at all while using this it’s more of a scratching feeling, it’s the sensitive areas that are “painful”. All in all I am so happy with this purchase.</p>\n",
      "rating": 5,
      "verified": false,
      "reviewer_avatar_urls": "https://secure.gravatar.com/avatar/?s=96&d=mm&r=g"
    },
    {
      "idReview": 565,
      "date_created": "2020-07-28T21:45:32",
      "formatted_date_created": "July 28, 2020",
      "product_id": 615,
      "reviewerName": "Ange",
      ...
```

### 4. **`GET /products/description`**

- **Description**: Retrieves the description of a specific product from a given store URL.

| Parameter   | Type   | Default | Description                                      | Required |
|-------------|--------|---------|--------------------------------------------------|----------|
| `url`       | string | -       | The URL of the store to retrieve product description from | Yes      |
| `productId` | string | -       | The ID of the product to retrieve description for       | Yes      |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/products/description?url=https%3A%2F%2Fkarminhairtools.com&productId=615', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": {
    "id": 615,
    "name": "Karmin 5 in 1 Wet and Dry Epilator/Shaver",
    "slug": "karmin-5-in-1-wet-and-dry-epilator-shaver",
    "parent": 0,
    "type": "simple",
    "variation": "",
    "permalink": "https://karminhairtools.com/product/karmin-5-in-1-wet-and-dry-epilator-shaver",
    "sku": "KRM51",
    "short_description": "",
    "description": "<div class=\"woocommerce-product-details__short-description\">\n<p>Interchangeable heads provide you with a 5 in 1 tool allowing you to shave, exfoliate and smooth and buff rough and/or calloused feet for complete head to toe softness.</p>\n</div>",
    "on_sale": false,
    "prices": {
      "price": "15995",
      "regular_price": "15995",
      "sale_price": "15995",
      "price_range": null,
      "currency_code": "USD",
      "currency_symbol": "$",
      "currency_minor_unit": 2,
      "currency_decimal_separator": ".",
      "currency_thousand_separator": ",",
      "currency_prefix": "$",
      "currency_suffix": ""
    },
    "price_html": "<span class=\"woocommerce-Price-amount amount\"><span class=\"woocommerce-Price-currencySymbol\">&#036;</span>159.95</span>",
    "average_rating": "4.58",
    "review_count": 19,
    "images": [
    ...
```

### 5. **`GET /store/search`**

- **Description**: Allows you to search through the WooCommerce store and paginate the results.

| Parameter | Type    | Default | Description                            | Required |
|-----------|---------|---------|----------------------------------------|----------|
| `query`   | string  | -       | The search term used to query the store | Yes      |
| `page`    | integer | 1       | The page number of the results to retrieve | No       |
| `perPage` | integer | 14      | The number of results per page (max=70)   | No       |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/store/search?query=fit', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": {
    "total": 14449,
    "page": 1,
    "perPage": 14,
    "data": [
      {
        "domain": "totofit.com",
        "companyName": "Toto Fit K-9 Fitness",
        "category": "Animal",
        "language": "en",
        "popularity": "1",
        "twitter": "totofit",
        "facebook": "totofitllc",
        "count_emailaddresses": "3"
      },
      {
        "domain": "dogoutfit.co.uk",
        "companyName": "Dog outfit",
        "category": "Animal",
        "language": "en",
        "popularity": "3",
        "twitter": "",
        "facebook": "dogoutfit",
        "count_emailaddresses": "0"
      },
      {
        "domain": "fitnesshealthyoga.com",
        "companyName": "Fitness Health Yoga",
        "category": "Animal",
        ...
```

### 6. **`GET /store/analytics`**

- **Description**: Retrieves analytics data for a given store URL.

| Parameter | Type    | Default | Description                            | Required |
|-----------|---------|---------|----------------------------------------|----------|
|   `url`   | string  | -       | The URL of the store to retrieve analytics for | Yes      |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/store/analytics?url=https%3A%2F%2Fkarminhairtools.com%2F', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": {
    "domainName": "karminhairtools",
    "image": "https://site-images.similarcdn.com/image?url=karminhairtools.com&t=0&s=1&h=676c9f021d2fbd0a2bf8595521698ee9d1237256099aa827716ee3e4d70af2e6",
    "icon": "https://site-images.similarcdn.com/image?url=karminhairtools.com&t=2&s=1&h=676c9f021d2fbd0a2bf8595521698ee9d1237256099aa827716ee3e4d70af2e6",
    "imageLarge": "https://site-images.similarcdn.com/image?url=karminhairtools.com&t=1&s=1&h=676c9f021d2fbd0a2bf8595521698ee9d1237256099aa827716ee3e4d70af2e6",
    "title": "home - karmin hair tools",
    "domain": "karminhairtools",
    "isSubDomain": false,
    "yearFounded": "2001",
    "employeeRange": "10 - 50",
    "engagementOverview": {
      "BounceRate": 0.5130962726047121,
      "AvgMonthVisits": 2435.024842486897,
      "AvgVisitDuration": 12.620779545184119,
      "PagesPerVisit": 1.740537439604142,
      "TotalPagesViews": 4238.2519047146225
    },
    "trafficRanks": {},
    "topCountries": [],
    "genderDistribution": {},
    "audienceInterest": {},
    "competitors": [],
    "organicCompetitors": [
      {
        "Category": "Lifestyle~Beauty_and_Cosmetics",
        "Affinity": 1,
        "Domain": "selfcutsystem.com",
        "Rank": 1344322,
        "HasAdsense": false,
        ...
```

### 7. **`GET /store/competitors`**

- **Description**: Retrieves a list of competitors for a given store URL.

| Parameter | Type    | Default | Description                                   | Required |
|-----------|---------|---------|-----------------------------------------------|----------|
| `url`     | string  | -       | The URL of the store to find competitors for  | Yes      |
| `limit`   | integer | 10      | The number of competitors to retrieve         | No       |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/store/competitors?url=https%3A%2F%2Fkarminhairtools.com%2F', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": [
    {
      "domainName": "selfcutsystem",
      "image": "https://site-images.similarcdn.com/image?url=selfcutsystem.com&t=0&s=1&h=b7ca15ba74f4e9b2ef3e91972c409f9d74588baf2f1ea1ee1da4b37f267b3711",
      "icon": "https://site-images.similarcdn.com/image?url=selfcutsystem.com&t=2&s=1&h=b7ca15ba74f4e9b2ef3e91972c409f9d74588baf2f1ea1ee1da4b37f267b3711",
      "imageLarge": "https://site-images.similarcdn.com/image?url=selfcutsystem.com&t=1&s=1&h=b7ca15ba74f4e9b2ef3e91972c409f9d74588baf2f1ea1ee1da4b37f267b3711",
      "title": "cut your own hair | self-cut system – self cut system | perfecting men's grooming",
      "domain": "selfcutsystem",
      "isSubDomain": false,
      "yearFounded": "",
      "employeeRange": "10 - 50",
      "monthlyVisits": 19454.7843447954,
      "rankings": {
        "globalRanking": 1344322,
        "highestTrafficCountryRanking": 408059,
        "categoryRanking": 13988
      },
      "category": "Lifestyle/Beauty_and_Cosmetics",
      "url": "https://selfcutsystem.com"
    },
    {
      "domainName": "barberdepots",
      "image": "https://site-images.similarcdn.com/image?url=barberdepots.com&t=0&s=1&h=bbcd2364df409b1ddecdc3b18eca47427280755b131542f9e27cc4936d6a1b95",
      "icon": "https://site-images.similarcdn.com/image?url=barberdepots.com&t=2&s=1&h=bbcd2364df409b1ddecdc3b18eca47427280755b131542f9e27cc4936d6a1b95",
      "imageLarge": "https://site-images.similarcdn.com/image?url=barberdepots.com&t=1&s=1&h=bbcd2364df409b1ddecdc3b18eca47427280755b131542f9e27cc4936d6a1b95",
      "title": "barber depot - professional barber supply for barbers",
      "domain": "barberdepots",
      "isSubDomain": false,
      "yearFounded": "",
      ...
```

### 8. **`GET /store/all`**

- **Description**: Retrieves a paginated list of all stores.

| Parameter | Type    | Default | Description                            | Required |
|-----------|---------|---------|----------------------------------------|----------|
| `page`    | integer | 1       | The page number of the results to retrieve | No       |
| `perPage` | integer | 14      | The number of results per page (max=70)   | No       |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/store/all?page=1&perPage=15', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": {
    "total": 338377,
    "page": 1,
    "perPage": 15,
    "data": [
      {
        "domain": "grupocatala.com",
        "companyName": "Grupo Catala",
        "category": "Animal",
        "language": "es",
        "popularity": "1",
        "twitter": "grupocatala_",
        "facebook": "",
        "count_emailaddresses": "10"
      },
      {
        "domain": "windyacresfarmstand.com",
        "companyName": "Windy Acres Farm",
        "category": "Animal",
        "language": "en",
        "popularity": "1",
        "twitter": "windyacresfs",
        "facebook": "windyacresfarmstand",
        "count_emailaddresses": "0"
      },
      {
        "domain": "loose-wein.de",
        "companyName": "Weingut Loose – Sächsischer | Meissener Wein",
        "category": "Animal",
        ...
```

### 9. **`GET /products/all`**

- **Description**: Retrieves a paginated list of products for a given store URL.

| Parameter | Type    | Default | Description                                  | Required |
|-----------|---------|---------|----------------------------------------------|----------|
| `url`     | string  | -       | The URL of the store to retrieve products from | Yes      |
| `page`    | integer | 1       | The page number of the results to retrieve     | No       |
| `perPage` | integer | 14      | The number of results per page (max=70)        | No       |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/products/all?url=https%3A%2F%2Fwww.dogoutfit.co.uk&page=1&perPage=1', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": [
    {
      "id": 6630,
      "name": "Lintbells YuMove Advance For Cats 60caps pack of 1",
      "parent": 0,
      "type": "external",
      "variation": "",
      "permalink": "https://www.dogoutfit.co.uk/shop/lintbells-yumove-advance-for-cats-60caps-pack-of-1/",
      "sku": "",
      "short_description": "<p>LINTBELLS<br />\n60caps PackSize<br />\nProduct Type HEALTH &amp; HYGIENE REMEDIES&amp;SUPPLIMENTS</p>",
      "description": "<p>Yumove Enhance For Cats<br />\nLINTBELLS<br />\n60caps PackSize<br />\nProduct Sort HEALTH &amp; HYGIENE REMEDIES&amp;SUPPLIMENTS<br />\nYMAC60<br />\n<div class=\"main-cross-sell\" data-asin=\"B01MSD8P9P\">\n\r\n\t<div class=\"WooZone-cross-sell-loader\">\r\n\t\t<div>\r\n\t\t\t<div id=\"floatingBarsG\">\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_01\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_02\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_03\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_04\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_05\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_06\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_07\"></div>\r\n\t\t\t\t<div class=\"blockG\" id=\"rotateG_08\"></div>\r\n\t\t\t</div>\r\n\t\t\t<div class=\"WooZone-cross-sell-loader-text\"></div>\r\n\t\t</div>\r\n\t</div>\r\n\r\n\t\t\n</div>\n<div style=\"clear:both\"></div></p>",
      "on_sale": false,
      "prices": {
        "price": "2499",
        "regular_price": "2499",
        "sale_price": "2499",
        "price_range": null,
        "currency_code": "GBP",
        "currency_symbol": "£",
        "currency_minor_unit": 2,
        "currency_decimal_separator": ".",
        "currency_thousand_separator": ",",
        "currency_prefix": "£",
        "currency_suffix": ""
      },
      "price_html": "<span class=\"woocommerce-Price-amount amount\"><span class=\"woocommerce-Price-currencySymbol\">&pound;</span>24.99</span>",
      "average_rating": "0",
      "review_count": 0,
      "images": [
      ...
```

### 10. **`GET /products/searchby-category`**

- **Description**: Retrieves a paginated list of products for a given store URL and category ID.

| Parameter   | Type    | Default | Description                                       | Required |
|-------------|---------|---------|---------------------------------------------------|----------|
| `url`       | string  | -       | The URL of the store to search products from      | Yes      |
| `page`      | integer | 1       | The page number of the results to retrieve        | No       |
| `perPage`   | integer | 14      | The number of results per page (max=70)           | No       |
| `categoryId`| string  | -       | The ID of the category to filter products by      | Yes      |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/products/searchby-category?url=https%3A%2F%2Fkarminhairtools.com%2F&page=1&perPage=1&categoryId=26', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
  "data": [
    {
      "id": 615,
      "name": "Karmin 5 in 1 Wet and Dry Epilator/Shaver",
      "slug": "karmin-5-in-1-wet-and-dry-epilator-shaver",
      "parent": 0,
      "type": "simple",
      "variation": "",
      "permalink": "https://karminhairtools.com/product/karmin-5-in-1-wet-and-dry-epilator-shaver",
      "sku": "KRM51",
      "short_description": "",
      "description": "<div class=\"woocommerce-product-details__short-description\">\n<p>Interchangeable heads provide you with a 5 in 1 tool allowing you to shave, exfoliate and smooth and buff rough and/or calloused feet for complete head to toe softness.</p>\n</div>",
      "on_sale": false,
      "prices": {
        "price": "15995",
        "regular_price": "15995",
        "sale_price": "15995",
        "price_range": null,
        "currency_code": "USD",
        "currency_symbol": "$",
        "currency_minor_unit": 2,
        "currency_decimal_separator": ".",
        "currency_thousand_separator": ",",
        "currency_prefix": "$",
        "currency_suffix": ""
      },
      "price_html": "<span class=\"woocommerce-Price-amount amount\"><span class=\"woocommerce-Price-currencySymbol\">&#036;</span>159.95</span>",
      "average_rating": "4.58",
      "review_count": 19,
      ...
```

### 11. **`GET /categories`**

- **Description**: Retrieves the categories of products available in a given store URL.

| Parameter | Type    | Default | Description                                      | Required |
|-----------|---------|---------|--------------------------------------------------|----------|
| `url`     | string  | -       | The URL of the store to retrieve product categories from | Yes      |
| `page`    | integer | 1       | The page number of the results to retrieve       | No       |
| `perPage` | integer | 14      | The number of categories per page (max=70)       | No       |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/categories?url=https%3A%2F%2Fkarminhairtools.com', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
[
  {
    "id": 27,
    "name": "Hair Care Products",
    "slug": "hair-care-products",
    "description": "",
    "parent": 0,
    "count": 1,
    "image": {
      "id": 504,
      "src": "https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Care_Products.png",
      "thumbnail": "https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Care_Products-300x300.png",
      "srcset": "https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Care_Products.png 500w, https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Care_Products-300x300.png 300w, https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Care_Products-100x100.png 100w, https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Care_Products-150x150.png 150w",
      "sizes": "(max-width: 500px) 100vw, 500px",
      "name": "Hair_Care_Products",
      "alt": ""
    },
    "review_count": 19,
    "permalink": "https://karminhairtools.com/product-category/hair-care-products"
  },
  {
    "id": 24,
    "name": "Hair Dryers",
    "slug": "hair-dryers",
    "description": "",
    "parent": 0,
    "count": 3,
    "image": {
      "id": 505,
      "src": "https://karminhairtools.com/wp-content/uploads/2023/02/Hair_Dryers.png",
      ...
```

### 12. **`GET /store/contacts`**

- **Description**: Retrieves contact information associated with a specific store URL.

| Parameter | Type   | Default | Description                                       | Required |
|-----------|--------|---------|---------------------------------------------------|----------|
| `url`     | string | -       | The URL of the store to retrieve contact information from | Yes      |

Example request:

```javascript
fetch('https://woocommerce-stores-hub.p.rapidapi.com/store/contacts?url=https%3A%2F%2Foscarwareinc.com', {
  method: 'GET',
  headers: {
    'x-rapidapi-host': 'woocommerce-stores-hub.p.rapidapi.com',
    'x-rapidapi-key': 'API_KEY' // Replace 'API_KEY' with your API key
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

Example response:

```json
{
    "data": {
        "emails": [
            "debra.dudley@oscarwareinc.com",
            "kelly.busick@oscarwareinc.com",
            "atinfo@oscarwareinc.com"
        ],
        "phones": [
            "1 888 672 2797"
        ],
        "twitter": [],
        "linkedIn": [
            "https://www.linkedin.com/in/kelly-busick-cpa-0b557a6a",
            "https://linkedin.com/company/oscarware-grill-toppers"
        ],
        "instagram": [
            "https://instagram.com/oscarwareinc"
        ]
    }
}
```

## Error Handling

The  API returns standard HTTP status codes to indicate the success or failure of API requests. Below are common errors and suggestions for handling them.

|Status Code|Message|Description|Suggested Handling|
|--|--|--|--|
| **400** | Bad Request | The request was malformed or missing required parameters (e.g., `domain` parameter not provided). | Verify that all required parameters are included and correctly formatted. |
| **401** | Unauthorized | Invalid or missing API key in the request headers. | Check that a valid API key is included in `x-rapidapi-key`. |
| **403** | Forbidden | Access to the requested resource is denied, possibly due to rate limits or restricted access. | Review rate limits and ensure API permissions. Retry after a delay if rate limit exceeded. |
| **404** | Not Found | The requested domain information could not be found (e.g., domain does not exist). | Check the spelling or availability of the domain. |
| **429** | Too Many Requests | The API rate limit has been exceeded. | Implement rate-limiting logic and retry after the specified rate limit reset time. |
| **500** | Internal Server Error | A server error occurred while processing the request. | Retry the request after a few seconds. If the error persists, contact API support. |
| **503** | Service Unavailable | The API service is temporarily unavailable (e.g., due to maintenance). | Retry the request later or check the API status page for maintenance alerts. |

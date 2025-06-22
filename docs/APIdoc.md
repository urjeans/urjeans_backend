I'll help you test your API endpoints in Postman. First, let me check what API endpoints are available in your backend by looking at the routes.

Ran tool
Let me check the products.js file to see what endpoints are available:

Read file: backend/routes/products.js
Let me also check if the server is running and on which port:

Read file: backend/server.js
Perfect! Now I can help you test your API in Postman. Here are all the available endpoints and how to test them:

Base URL: `http://localhost:3000/api/products`

1. **Get All Products**
   - Method: GET
   - URL: `http://localhost:3000/api/products`
   - No body needed

2. **Get Products by Brand**
   - Method: GET
   - URL: `http://localhost:3000/api/products/brand/{brandName}`
   - Example: `http://localhost:3000/api/products/brand/Izmir`
   - No body needed

3. **Get Single Product**
   - Method: GET
   - URL: `http://localhost:3000/api/products/{id}`
   - Example: `http://localhost:3000/api/products/1`
   - No body needed

4. **Create New Product**
   - Method: POST
   - URL: `http://localhost:3000/api/products`
   - Headers: 
     - Content-Type: application/json
   - Body (raw JSON):
   ```json
   {
       "brand_name": "New Brand",
       "colors": "Blue,Black",
       "images": ["url1.jpg", "url2.jpg"],
       "fabric": "98% Cotton, 2% Elastane",
       "sizes": "28,30,32,34",
       "description": "New stylish jeans"
   }
   ```

5. **Update Product**
   - Method: PUT
   - URL: `http://localhost:3000/api/products/{id}`
   - Example: `http://localhost:3000/api/products/1`
   - Headers:
     - Content-Type: application/json
   - Body (raw JSON):
   ```json
   {
       "brand_name": "Updated Brand",
       "colors": "Blue,Black,White",
       "images": ["url1.jpg", "url2.jpg", "url3.jpg"],
       "fabric": "95% Cotton, 5% Spandex",
       "sizes": "28,30,32,34,36",
       "description": "Updated description"
   }
   ```

6. **Delete Product**
   - Method: DELETE
   - URL: `http://localhost:3000/api/products/{id}`
   - Example: `http://localhost:3000/api/products/1`
   - No body needed

Before testing, make sure:
1. Your MySQL server is running
2. Your backend server is running (start it with `npm run dev` in the backend directory)
3. You have some data in your database (the sample data should be there from the schema)

To start the backend server:

```bash
cd backend && npm run dev
```
Would you like me to:
1. Start the backend server for you?
2. Help you test a specific endpoint?
3. Show you how to set up a Postman collection for all these endpoints?

Just let me know what you'd like to do first!



I'll help you create a Postman collection for all the Urjeans API endpoints. Here's a step-by-step guide:

1. **Create a New Collection**
   - Open Postman
   - Click "Collections" in the sidebar
   - Click the "+" button to create a new collection
   - Name it "Urjeans API"

2. **Set up Environment Variables** (This will make it easier to manage the base URL)
   - Click "Environments" in the sidebar
   - Click "+" to create a new environment
   - Name it "Urjeans Local"
   - Add these variables:
     - `base_url`: `http://localhost:3000`
     - `api_path`: `/api/products`
   - Click "Save"
   - Select this environment from the environment dropdown in the top right

3. **Create the following requests in your collection:**

   A. **Get All Products**
   - Method: GET
   - URL: `{{base_url}}{{api_path}}`
   - Name: "Get All Products"
   - Description: "Retrieve all jeans products"

   B. **Get Products by Brand**
   - Method: GET
   - URL: `{{base_url}}{{api_path}}/brand/{{brand_name}}`
   - Name: "Get Products by Brand"
   - Description: "Retrieve products by brand name"
   - Add a variable:
     - In the "Variables" tab of the collection:
       - `brand_name`: "Izmir" (or any brand you want to test with)

   C. **Get Single Product**
   - Method: GET
   - URL: `{{base_url}}{{api_path}}/{{product_id}}`
   - Name: "Get Single Product"
   - Description: "Retrieve a single product by ID"
   - Add a variable:
     - In the "Variables" tab of the collection:
       - `product_id`: "1" (or any product ID you want to test with)

   D. **Create New Product**
   - Method: POST
   - URL: `{{base_url}}{{api_path}}`
   - Name: "Create New Product"
   - Description: "Create a new jeans product"
   - Headers:
     - Key: `Content-Type`
     - Value: `application/json`
   - Body (raw JSON):
   ```json
   {
       "brand_name": "New Brand",
       "colors": "Blue,Black",
       "images": ["url1.jpg", "url2.jpg"],
       "fabric": "98% Cotton, 2% Elastane",
       "sizes": "28,30,32,34",
       "description": "New stylish jeans"
   }
   ```

   E. **Update Product**
   - Method: PUT
   - URL: `{{base_url}}{{api_path}}/{{product_id}}`
   - Name: "Update Product"
   - Description: "Update an existing product"
   - Headers:
     - Key: `Content-Type`
     - Value: `application/json`
   - Body (raw JSON):
   ```json
   {
       "brand_name": "Updated Brand",
       "colors": "Blue,Black,White",
       "images": ["url1.jpg", "url2.jpg", "url3.jpg"],
       "fabric": "95% Cotton, 5% Spandex",
       "sizes": "28,30,32,34,36",
       "description": "Updated description"
   }
   ```

   F. **Delete Product**
   - Method: DELETE
   - URL: `{{base_url}}{{api_path}}/{{product_id}}`
   - Name: "Delete Product"
   - Description: "Delete a product by ID"

4. **Add Collection Tests** (Optional but recommended)
   For each request, you can add tests to verify the response. Here's an example for the "Get All Products" request:

   In the "Tests" tab of the request:
   ```javascript
   pm.test("Status code is 200", function () {
       pm.response.to.have.status(200);
   });

   pm.test("Response is JSON", function () {
       pm.response.to.be.json;
   });

   pm.test("Response has products array", function () {
       var jsonData = pm.response.json();
       pm.expect(Array.isArray(jsonData)).to.be.true;
   });
   ```

5. **Save the Collection**
   - Click "Save" to save your collection
   - You can also export the collection by:
     - Click the three dots next to your collection
     - Select "Export"
     - Choose "Collection v2.1"
     - Save the JSON file

Here's a sample collection JSON that you can import directly into Postman:

```json
{
    "info": {
        "name": "Urjeans API",
        "description": "API collection for Urjeans backend",
        "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
    },
    "item": [
        {
            "name": "Get All Products",
            "request": {
                "method": "GET",
                "url": {
                    "raw": "{{base_url}}{{api_path}}",
                    "host": ["{{base_url}}"],
                    "path": ["{{api_path}}"]
                }
            }
        },
        {
            "name": "Get Products by Brand",
            "request": {
                "method": "GET",
                "url": {
                    "raw": "{{base_url}}{{api_path}}/brand/{{brand_name}}",
                    "host": ["{{base_url}}"],
                    "path": ["{{api_path}}", "brand", "{{brand_name}}"]
                }
            }
        },
        {
            "name": "Get Single Product",
            "request": {
                "method": "GET",
                "url": {
                    "raw": "{{base_url}}{{api_path}}/{{product_id}}",
                    "host": ["{{base_url}}"],
                    "path": ["{{api_path}}", "{{product_id}}"]
                }
            }
        },
        {
            "name": "Create New Product",
            "request": {
                "method": "POST",
                "header": [
                    {
                        "key": "Content-Type",
                        "value": "application/json"
                    }
                ],
                "url": {
                    "raw": "{{base_url}}{{api_path}}",
                    "host": ["{{base_url}}"],
                    "path": ["{{api_path}}"]
                },
                "body": {
                    "mode": "raw",
                    "raw": "{\n    \"brand_name\": \"New Brand\",\n    \"colors\": \"Blue,Black\",\n    \"images\": [\"url1.jpg\", \"url2.jpg\"],\n    \"fabric\": \"98% Cotton, 2% Elastane\",\n    \"sizes\": \"28,30,32,34\",\n    \"description\": \"New stylish jeans\"\n}"
                }
            }
        },
        {
            "name": "Update Product",
            "request": {
                "method": "PUT",
                "header": [
                    {
                        "key": "Content-Type",
                        "value": "application/json"
                    }
                ],
                "url": {
                    "raw": "{{base_url}}{{api_path}}/{{product_id}}",
                    "host": ["{{base_url}}"],
                    "path": ["{{api_path}}", "{{product_id}}"]
                },
                "body": {
                    "mode": "raw",
                    "raw": "{\n    \"brand_name\": \"Updated Brand\",\n    \"colors\": \"Blue,Black,White\",\n    \"images\": [\"url1.jpg\", \"url2.jpg\", \"url3.jpg\"],\n    \"fabric\": \"95% Cotton, 5% Spandex\",\n    \"sizes\": \"28,30,32,34,36\",\n    \"description\": \"Updated description\"\n}"
                }
            }
        },
        {
            "name": "Delete Product",
            "request": {
                "method": "DELETE",
                "url": {
                    "raw": "{{base_url}}{{api_path}}/{{product_id}}",
                    "host": ["{{base_url}}"],
                    "path": ["{{api_path}}", "{{product_id}}"]
                }
            }
        }
    ]
}
```

To use this collection:
1. Open Postman
2. Click "Import" in the top left
3. Paste the JSON above
4. Click "Import"
5. Set up the environment variables as described above
6. Select the "Urjeans Local" environment from the dropdown

Would you like me to:
1. Explain any part of the collection setup in more detail?
2. Show you how to add more advanced tests to the requests?
3. Help you test any specific endpoint?
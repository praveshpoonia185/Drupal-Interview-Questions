# API & Integration Questions

### 1. What is the REST API in Drupal?

Drupal has a built-in REST API that lets other applications create, read, update, and delete content using HTTP requests (GET, POST, PATCH, DELETE).  

You can enable REST resources for nodes, users, etc., and use them with tools like Postman or JavaScript frontends.

### 2. What is JSON:API?

JSON:API is a standard way to expose Drupal content as JSON.  

It is included in Drupal core.  
It follows the JSON:API specification and is very good for decoupled (headless) Drupal sites.  
It supports filtering, sorting, includes (related entities), and sparse fieldsets.

### 3. What is GraphQL in Drupal?

GraphQL is a query language for APIs.  
With the GraphQL module, frontends can request exactly the data they need in one request.  

It is popular for modern JavaScript frameworks (React, Vue, Next.js) when using Drupal as a backend.

### 4. How do you integrate third-party APIs?

Common ways:  
- Use Guzzle (Drupal’s HTTP client) to call external APIs  
- Create a custom service that handles the API calls  
- Store API keys in configuration or environment variables  
- Use contributed modules if available (example: for payment gateways, social media)  
- Handle errors and rate limits properly

### 5. What is OAuth authentication?

OAuth is a secure way for applications to access user data without sharing passwords.  

In Drupal, you can use modules like Simple OAuth or the core OAuth features to protect APIs.  
Clients get an access token and use it to make authenticated requests.

### 6. How do you upload files through an API?

Using JSON:API or REST:  
1. First upload the file to the file endpoint (usually `/jsonapi/file/file` or similar)  
2. Get the file UUID  
3. Then create or update the entity and reference that file UUID  

You need proper permissions and authentication (OAuth or basic auth for development).

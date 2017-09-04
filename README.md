# AWS-Serverless-API

Introduction: 
1. What's AWS?
- Amazon Web Services - AWS offers a broad-range of cloud computing services which means services using their infrastructure which is hosted on various datacenters all over the world which one can rent to run your own solutions/apps.
  - Cloud hosting
    - EC2, Elastic Beanstalk, Lambda, Auto Scaling, Elastic Load Balancing
  - Storage
    - Simple Storage Service (S3)
  - Networking and Content Delivery
    - CloudFront, Elastic Load Balancing
2. What's Serverless Computing is?
  - Traditional Web Hosting - apps (web & mobile)
    - REST API for client to exchange data
      - run business logic
      - access database
      - server could serve HTML page
  - Serverless Computing shines when you have a decoupled frontend and backend
  - backend is such an API, frontend (mobile or web)
  - How does code on the server run? 
    - Write our own code to listen to incoming requests on certain API endpoints
    - URL for services to sent requests to
    - runs on a servers, provision with EC2, virtual machine
    - scaling we need more servers - AWS or our own
      - Issue: re-invent the wheel to creating the API
        - logic to handle incoming requests, incoming endpoints in code
        - infrastructure and not business logic
      - Issue: Servers are online even if not requested
        - danger of over or under provisioning
          - too many (pay too much), or not enough for traffic spikes
      - Issue: Over and Under provisioning
      - Issue: Keep OS & Software Updated of Servers
        - don't break
    - Challenges above of managing our own servers
  - Serverless Apps
    - AWS Lambda Service host our code and allows us to execute on demand when needed
    - We don't have to worry about how many servers we need, we don't need to pay idle time
    - Only pay if requests are coming in and don't need to update software
    - node.js, python, java, C# lambda - serverless API
    - host our web page in a serverless manner.
  - Traditional vs Serverless
    - (Traditional) - Provision capacity, server capacity (CPU, RAM, Memory)
    - (Traditional) - scaling (pay too much on server issues)
    - (Traditional) Update OS and Software, security issues 
    - (Traditional) - lots of overhead for SPA + API apps, great support for fullstack apps, no seperation has great support
    - (Serverless) - Runs on demand, unlimited capacity, only pay for code executions
    - (Serverless) - Scales automatically - pay what you need
    - (Serverless) - runs in up-to-date and secure environment
    - (Serverless) - great for SPA + API apps, limited support for fullstack apps (node/express apps)
 - API Gateway
    - New API, first-api
    - define all the resources API, HTTP methods in editor
    - there are advanced ways of creating such an API (importing API definition files) 
    - Resources -> Actions -> Create Resource
      - define which HTTP request to react, actions -> create method (GET)
        - Lambda Function, HTTP endpoint, Mock, AWS Service
        - Mock (Dummy data)
        - Integration response -> Body Mapping Templates
    - Deploy API
      - Actions -> Deploy API
      - Stage different versions 
      - Deploy with invoke URL
      - Missing auth token because not handling root, change to api endpoint
      - JSON object, API Gateway 
  - Why AWS?
    - Microsoft Azure, Google Cloud Platform
    - Market Leader, Aggressive Pricing
    - Most Serverless Services (allow elaborate apps)
    - Rapid Innovation and New Features
    - Cutting-edge technologies
- Structure
  - Core Serverless Services (which is required for serverless app)
  - Business Logic with Lambda and API Gateway
  - Data Storage with DynamoDB
  - Authentication with Cognito, protect against unauthenticated accoess
  - Content Delivery and Hosting with S3, CloudFront, and Route53 => Web apps in a serverless manner
  - Beyond the Basics (Outlook) 

3. Core AWS Serverless Services
  - Which AWS services we need to use to build a serverless solution
  - Which services do we need?
    - We can do more than host backend
    - Web app, can host on AWS and scale dynamically, don't have to provision capacities
      - Serve Static App (React.js App) -> S3 (Simple Storage Service), File storage server, no server-side code, no capacities
      - REST API -> API Gateway - service that makes it easy to create paths and HTTP methods
      - Logic -> Execute code on demand -> Lambda, custom API endpoint
      - Data -> Store and Retrieve Data (DB) -> DynamoDB (NoSQL) - don't want to manage DB Servers, don't need to provision
      - Auth -> Authenticate Users -> Cognito, easily create user pools to signups/signin and protect REST API
      - DNS -> Translate URL -> Route 53, configure our own domain we actually load from S3 buckets
      - Cache -> Improve Performance (e.g. caching) -> CloudFront, all over the world copied to have the quickest route possible
    - For backend (API, Logic, Data, Auth)
  - Project description
    - Frontend app, use finished app to host and give it domain, to build an API + Authentication
    - Compare Yourself app
    - Host S3 Web App, enter data into form (Income, height, etc.)
    - When data is submitted, use API Gateway (GET, POST, DELETE)
    - Authentication to protect API endpoints
    - Business Logic - Lambda functions runs whenever requests reach endpoints
    - Store data - DynamoDB
    - polish it with Route 53 and CloudFront for caching
4. REST API with API Gateway & AWS Lambda
  - What is the API Gateway?
    - Creates a RESTful API with ease
  - How it works
    - Application (web app, mobile app, postman)
    - Clients will send requests to REST API (database query etc.), node.js
    - Endpoints can connect to client with URLs 
    - Don't need to write code to API Endpoints & HTTP Methods
    - Authentication - authorize access
    - Action -> directly access some AWS services
    - Run Lambda Code (and forward Request Data), hosts code
  - API Gateway
    - Resources, deploy on stage
    - API Keys -> shared with others developers, creating their own apps (Google Maps API), register on Google, key to pass and Google can throttle you
    - send keys to identify, and block users without API keys
    - usage plan - only access 1000 times a minute
    - not important if you API on your own
    - Custom Domain Names, don't have the generic AWS domain
    - Client Certificates to forward requests, to validate requests stems from API gateway, proves to final API endpoint on another API
    - Settings -> generate log files to give the right provision
  - AWS Security Model and IAM (Identity and Access Management) 
    - https://youtu.be/9CKsX6MOPDQ
    - https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html
    - By default, AWS doesn't give any permissions to any of your services. That means, that no service may interact with other services.
  - Menu items of the API and how does it work?
    - Resources -> Actions -> Create Resource -> Create method
    - Resources manage resources and methods, new path in the final URL you want to use
    - Resources is not live, we have to use actions -> Deploy API -> Select stage 
    - Stages are like deployed snapshots
    - Authorizers - add authentication to API
      - How to authenticate users (AWS Cognito) 
    - Models 
      - Allow to define the shape of the data 
      - Define JSON schema, how the JSON should be structured
      - Validate incoming data, reject if not
    - Documentation 
      - Binary Support
    - Dashboard (Governance), API Calls, Latency
    - Resources -> Select Method -> How API Gateway works behind the scene
  - API Gateway Request-Response Cycle
    - Endpoint (Path and Type) - GET Requests
    - Hit Endpoint we hit cycle
      - Flow of data of our API
      - Client (Test) - orange markers to get hints or show all hints => 
      - Method Request - how incoming reqeust is handled by API gateway
      - How requests look like, reject requests if it doesn't fit schema
        - We can set to Authorization, we can block with error code
        - Request Validator (query parameters, http request headers - after the question mark, request headers, request headers)
        - API Key - lock API if they don't have keys
      - Method request to fulfill the requirements
    - Integration Request
      - Mapping incoming data into the shape we want for the action (e.g. lambda, mock, http)
      - Integration Request to trigger (lambda etc.)
        - Transform incoming data, and pass it to the endpoint
    - Integration Response
        - When done sends it back, same above (extract data and pass to action)
        - Allows us to configure response we're getting back
    - Method Response
        - Not a gatekeeper, defines our shape of response
        - Status codes, headers to have, type of data
    - Request is received, checked by the gate keeper, possibly rejected, transformed with integration request and pass it onto action, action does something with it, integration response - take the data action returned and transform and set it up for response -> method response - defines the boundary and shape of the response -> then sent back to client
    - Four ways to create an API
      - New API
      - Clone from existing API 
      - Import from Swagger - definition file, define API as a text file (automatically generate)
      - API snapshots - Swagger file, JSON file
      - Example API 
    - Configure proxy resource - catch all and will be flexible, will catch all requests => serverless API is great, lambda you can express.js route in Lambda, full-stack serverless approach (hacky) 
    - Enable API Gateway CORS
      - What is CORS?
        - Cross Origin Resource Sharing
        - Security Model can't access resources on another resources
        - Two different domains 
        - Create an option to send right headers to client so that browser have no issues from our API
        - CORS Header - Access-Control-Allow-Headers	
        - Any domain can send these requests
- What is AWS Lambda?
  - AWS lambda is a service allowing you to host your code and run it on certain events
  - How it works?
    - Event Source (S3 - e.g. file gets uploaded) - transform it, people upload, compress, and analyze with ML
      - CloudWatch (Scheduled - regular basis)
      - API gateway (requests hits API gateway, HTTP request)
    - Event Source -> Code (Node.js, Python, Java, C#) 
    - Result -> interact with other AWS Services (DynamoDB) -> Return Response, callback is done and shutdown, pass data back to the event source. 
    - AWS API Gateway + AWS Lambda
    - Each endpoint triggers different Lambda Function
- Creating a Lambda Function
  - Lambda => Event Triggers 
    - We don't set a trigger here, triggerleess function, logic in API Gateway not in Lambda
    - Better to use IDE and upload code (zip file, or S3)
    - could pass environmental variables 
    - Function handler -> what actually gets called
    - Upload files in a zip files (need file named index.js) - Lambda Docs
    `exports.fn = (event, context, callback) => {`
    `// TODO implement`
    `callback(null, { message: 'Hi, I\'m Lambda!'});`
    - Callback is a function itself takes two - (error arg, data we want to pass back) -> first object would be return, can control what to throw
    - Role configurations - no permission granted in AWS initially,
    - permission to write log files
    - tags -> key,value pairs 
    - How much memory is allocated, more expensive it is, free contingent each month
    - VPC (Virtual Private Cloud) - 
    - Active Tracing - cost expensive
    - Encrypt environment keys
    - DLQ
 - Connecting Lambda Functions to API Gateway Endpoints
  - Go to API Gateway and connect 
  - Find AWS Lambda and give permission 
- Connect our API Gateway and Lambda
  - Want to test outside of API Gateway test
  - We need to deploy API Gateway to call it outside
  - Stages is our snapshot
  - resources -> Deploy API
  - Testing API -> codepen.io -> testing purposes on their servers
    - disable auto-updating preview
    
    - `var xhr = new XMLHttpRequest();`
    - `xhr.open('POST', 'https://a69nt0aobf.execute-api.us-west-2.amazonaws.com/dev/compare-yourself');`
    - `xhr.onreadystatechange = function(event) {`
    -  `console.log(event.target.response);`
    - `}`
    - `xhr.send();`
  - CORS No Access-Control-Allow-Origin 
  - 1. Add new header under Method Response `Access-Control-Allow-Origin`
  - 2. Integration Response -> can now set value for header -> '*'     *
  - Deployment history 
  - CORS error won't come up in AWS console

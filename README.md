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

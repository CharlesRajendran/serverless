# serverless

5 important things in serverless function
  - Function - Lambda functions
  - Events - Events can be http requests, sqs got some message and etc.
  - Resources - AWS services which we can access with AWS
  - Services - YAML.....
  - Plugins - for development like typescript, browserify
  
Installation
  - `npm install -g serverless`
  
Configure
  - Serverless needs a user which contain permission to relevant services that we going to use inside the functions we write
  - Create a IAM User with full permission (Even though it is not recommended)
    - We can give permission to a user either only CLI or Management Console or both.
  - Add the key information to serverless configuration
    - `sls config credentials --provider aws --key {key of the IAM User} --secret {secret of the IAM User}`
    
Creating project
  - sls create command will generate a boilerplate application for the the type of serverless project we want to create
  - Also it has some parameters, like, template, name, path.
    - `sls create --template aws-nodejs`
  
  - This will create 3 files
    - a .gitignore file 
    - handler.js (which will have all the functions)
    - serverless.yml file (services file)
      - in this file we specify all the things like, functions, resources used, and etc.
    
Deploying the function
  - `sls deploy`
  - when deploying the serverless function 
    - it will create a cloudformation template
    - all the functions code and resources will be put to s3 bucket
    - Also it will create a aws cloud watch log group 
    - will have a serverless function
    
Testing the serverless function
  - `sls invoke --function <function-name>`
  - Running locally (When using aws resources it won't work)
    - `sls invoke local --function <function-name>`
    
Events for functions
  - if we want to execute our function with a http request then I have to create a API resource with API Gateway and connect the API with the lambda.
  - I can do the same thing with serverless using `events` property, if the event is http then I can use `http`
~~~
events:
  - http:
    path:
    method:
~~~

Event Object
  - in each lambda function, we have a event argument which have all the information about the event
  - in a http event we have information like, queryParameters, pathParameters, body params, method type and etc.
  
AWS Resources
  - If we want to use other aws resources, such as using a s3 bucket, adding a rds database and etc.

Console Logging
  - `sls logs -f myFunctionName -t`

# What is this?
```
no more YAML. use your favorite programming language (JS, python and more) to build :

Build out the Fargate infrastructure for your  spring boot application, 
RDS,
including logging, 
Secret env variable in task definition (RDS Password),
cloudwatch dashboard and 
custom metric autoscaling with target tracking.

```
# Prepwork

Use AWS Cloud9.


## Create a DB password for RDS .. replace it with your own password value
```
aws ssm put-parameter --name "/mysqlpassword" --value "P@ssW%rd#1" --type "SecureString"

```


## Deploy using aws cdk
```bash
export AWS_REGION=ap-southeast-1  # or any region

npm install
npx cdk@0.36.1 bootstrap
npx cdk@0.36.1 deploy  --require-approval never  "*"

```

## Test the app:
This is a spring boot CRUD app with RDS (mysql).

```
# use httpie to POST to ALB endpoint / api/notes , eg:

http POST sprin-sprin-????????????.ap-southeast-1.elb.amazonaws.com/api/notes title="title 2" content="sample content"

# view the list of notes :

http sprin-sprin-????????????.ap-southeast-1.elb.amazonaws.com/api/notes

      Connection: keep-alive
      Content-Type: application/json;charset=UTF-8
      Date: Mon, 08 Jul 2019 06:15:10 GMT
      Transfer-Encoding: chunked

      [
          {
              "content": "aa",
              "createdAt": "2019-07-08T06:10:41.000+0000",
              "id": 1,
              "title": "title1",
              "updatedAt": "2019-07-08T06:10:41.000+0000"
          },
          {
              "content": "sample content",
              "createdAt": "2019-07-08T06:14:28.000+0000",
              "id": 2,
              "title": "title 2",
              "updatedAt": "2019-07-08T06:14:28.000+0000"
          }
      ]
```
# sam-eventbridge-api
Demo of eventbridged with api gateway as origin and destinations 

The sample has three folders
```
api-to-eb
- template.yml
eb-to-api
- template.yml
artillery-api-eb
- api-to-eb-to-api.yaml
- message.csv
- pakage.json
```

The folder `api-to-eb`  have the configurations of Api Gateway to eventBridge infrastructure

The folder `eb-to-api` have the version de a demo make by Marcia Villalba, of Api Gateway destinations for eventBridge

The folder `artillery-api-eb` have the *artillery* configurations for run a load test over the pattern Api Gateway eventBridge Api destinations. 

The goal of this demo is build and eventBridge Api -> eventBridge -> Api out the AWS, without lambdas in the middle and run a load Test wiht artillery.

# How deploy the DEMO

1- Deploy the infrastructure in the folder `api-to-eb`

```bash
cd api-to-eb
sam deploy --guided --capabilities CAPABILITY_NAMED_IAM
```
   Filled the parameters answer in the deployment process

2- Deploy the insfrastructure in the folder `eb-to-ap``

```bash
cd api-to-eb
sam deploy --guided --capabilities CAPABILITY_NAMED_IAM
```
Filled the parameters answer in the deployment process
- One of the parameters is the URI of destinations 

# How Run the test

1- Run artillery load test
```bash
cd artillery-api-eb
$(npm bin)/artillery run api-to-eb-to-api.yml --output test.json
```
2- Built html report
```bash
$(npm bin)/artillery report --output report.html test.json
open report.html
```
## References
- https://github.com/mavi888/sam-eventbridge/blob/api-destinations/blueDragon/template.yml#L10
- https://serverlessland.com/patterns/eventbridge-api-destinations
- https://www.artillery.io/ 

# templates
It contains templates for automation

Template parameters
Parameter
Purpose
pLambdaName
Name of the Lambda function
pRDSType
Whether the database is db-instance or db-cluster
pDBEndPoint
Endpoint of RDS, Aurora, or RDS Proxy e.g. database-1.c54cuigo631e.ap-south-1.rds.amazonaws.com
pRDSPort
Database port (default: 3306)
pVPCid
VPC where the NLB and Lambda will be deployed
pSubnetsGroup
Private subnets for Lambda and NLB (minimum 2)
pSecurityGroup
Security group for Lambda
pTargetRoleARN
Role ARN from the source account that is allowed to connect to PrivateLink e.g. arn:aws:iam::111111111111:root


![privatelink_architecture_diagram](https://github.com/user-attachments/assets/d9651434-8027-4164-8d3a-33a62442efc1)

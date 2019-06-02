## Whispli challenge 

Deployment of API and UI into AWS using ECS Fargate with ALB and S3 static website repectively

### Assumptions

The following packages are installed on a *nix based operating system:

- awscli
- jq

The executing environment contains a valid AWS credentials profile and, if required, a config file with require assume role profile

### Usage

4 shell scripts are used to execute the deployment. These scripts utilse Cloudformation and S3 client for uploading the static website

Cloudformation scripts are stored in the folder cloudformation and the static website source is store in the ui folder

The scripts need to be executed in a specific order to satisfy stack dependancies:

- create_fabric - initialises VPC, security groups, role and a public Load Balancer
- create_databse - initialises a single MySQL RDS instance
- create_api - initialise a ECS service and task using Fargate and registers it with the Load Balancer, output of script will supply the API URL
- create_ui - initialise a static website S3 bucket and will sync the contents of the ui folder into this buckey, output of the script will supply the URL of the Website

The scripts will execute using the default system AWS profile, if you wish to execute into a specific account you can set a new profile using:

export AWS_PROFILE=(profile)

### Caveat

I dont think it is possible to achieve production quality anything without consistent effort and multiple feedback iterations but I think this submission is a good place to start
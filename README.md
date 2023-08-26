# UdaPeople_CICD_Project

## Project Overview

This project deploys a full stack (frontend and backend) [NodeJS](https://nodejs.org/en/) application of the **UdaPeople** using the concept of CI/CD to enable automated building, testing and deployment.
[CI/CD](https://en.wikipedia.org/wiki/CI/CD) in this project helps in deploying the application to production using Integrated Pipelines and [circleci](https://circleci.com/) as the CI/CD tool.

### Prerequisites

To get this project done ensure to have this tool installed and running on your local machine

* [Git](https://git-scm.com/)

* Create an account on [CircleCi](https://circleci.com/) and  setup the project from the documentaion. 

* Create an account on [AWS](https://aws.amazon.com/)

#### Project Sections

- **Continuous Integration (Build, Test and Analyze)**

The config file present in the **.circleci** of the repository `config.yml` contains the jobs for the pipelines used for this project. 
The goal of a build phase is to compile/lint the source code to check for syntax errors or unintentional typos in code seprately in the frontend and backend.
Test phase checks if the code is trustworthy and the Analyze(audit) phase checks for security vulnerability in the code.

- **Configuration Management**

In this section, we will create and configure infrastructure before deploying code to it. This can be accomplished by building [Ansible Playbooks](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html) for use in the CircleCI configuration which is included as `ansible` in the .circleci directory.
  
- **Setup - AWS**

  - Create and download a new key pair in AWS. Name this key pair "udacity" so that it works with the Cloud Formation templates in `.circleci/files/` of this repository. Look for "Option 1: Create a key pair using Amazon EC2" [in this tutorial](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/getstarted-keypair.html), if you need help. You'll be using this key pair (pem file) in future steps so keep it in a memorable location.
  - Create IAM user for programmatic access only and copy the access key id and secret access key. [Refer to this tutorial](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html), if you need help. We will need these credentials to add to CircleCI configuration 
  - Add a PostgreSQL database in RDS that has public accessibility. [This tutorial may help](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html). As long as you marked "Public Accessibility" as "yes", you won't need to worry about VPC settings or security groups.

- **Setup - CircleCI**
  - Add SSH Key pair from EC2 to the CircleCI Project Settings > SSH Keys > Additional SSH Keys. To get the actual key pair, you'll need to open the pem file in a text editor and copy the contents. Then you can paste them into Circle CI as shown in the image below.
  
![SSH Image](https://video.udacity-data.com/topher/2021/October/616d50a0_screenshot-2021-10-12-at-1.01.28-pm/screenshot-2021-10-12-at-1.01.28-pm.png)

  - Add the following environment variables to your Circle CI project by navigating to {project name} > Settings > Environment Variables as shown below.

![Env Var](https://video.udacity-data.com/topher/2021/October/616d513a_screenshot-2021-10-18-at-4.18.16-pm/screenshot-2021-10-18-at-4.18.16-pm.png)
  
> **Having proceeded with the steps above, CircleCI runs the Pipeline upon commits made on git**

- **Monitoring**

This Project uses [Prometheus](https://prometheus.io/) as a monitoring solution since it is open-source and versatile. Once configured properly, Prometheus will turn our server’s errors into sirens that no one can ignore

##### Running the application

The application can be accessed using either the CloudFront domain name or the public URL for your S3 Bucket. Upon a succesful deployment we should have a similar frontend shown below.

![frontend images](https://video.udacity-data.com/topher/2021/October/616e6ef4_screenshot-2021-10-14-at-1.23.28-am/screenshot-2021-10-14-at-1.23.28-am.png)

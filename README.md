# Deployment_1.1

**GitHub**
- Create a new repository.

- Under the tab `Add file`, select `Upload files`.

- Upload files from your local server, then commit to your GitHub repository.

**Jenkins**
<img width="1428" alt="Screen Shot 2023-08-15 at 6 44 07 PM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/bec5f98d-b616-4b10-81d3-cb32a3f7dfa4">

- Navigate to your Jenkins server with port 8080. This is the port that will listen for incoming traffic that attempts to connect via ssh.

- Log into your Jenkins server. 

- Select `New Item` on the left-hand side to create a new build to test our application code from your GitHub repository.

<img width="371" alt="Screen Shot 2023-08-15 at 6 45 34 PM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/b0cc9e56-14d1-4d26-af59-e371e3c9182e">

- Enter your item name, select `Pipeline`, then `OK`.

- <img width="1366" alt="Screen Shot 2023-08-15 at 6 47 32 PM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/d99e7dc9-45a9-40c1-b7db-3eec398a0dff">

- Scroll to `Pipeline` and under the drop-down, select `Pipeline script from SCM`.

Under each selection you choose will be the following drop-down. Select the following:
- SCM --> Git
- Repositories --> Repository URL (enter git repo URL).
- Head to your GitHub repo. Under the green `Code` tab, copy the HTTPS URL, then copy it in the `Repository URL`.
- Under `Credentials` find your GitHub username, with the associated token.

- Scroll to `Branches to build`. Change name from `master` to `main`.

- Scroll down to click `Apply` and then `Save`.

- On the left-hand side, find `Build Now` -- select this then start your build under `Build Now`.

- The pipeline for the deployment was successful, so can now move to creating and deploying a Python URL Shortener on AWS Elastic Beanstalk.

**Deploying application**

- Create a separate folder for the application files, then compress it by using a .zip

- Navigate to the `IAM` AWS console and create IAM Roles and Permissions so the EC2 instance and Elastic Beanstalk have permission to communicate with one 
another, and to also assume the role, and perform actions on your behalf.

- Select `Roles` on the left-hand side.

- Select `Create Role`.

- Under `Trusted entity type`, select `AWS service`.
- 
- Click the AWS Service that allows *AWS services like EC2, Lambda, or others to perform actions in this account.* field and then *Elastic Beanstalk - Customizable*.

- After clicking next, click the `Role name` field and enter *aws-elasticbeanstalk-service-role*.

- Click `Create role`

- "Create role" to create a second Role; Go through the same process, but this time, click the *EC2Allows EC2 instances to call AWS services on your behalf.* field.

- <img width="1366" alt="Screen Shot 2023-08-15 at 7 49 19 PM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/efe14127-282d-4eb8-b561-293d82d7de85">

- Click `Next`

- Filter policies by property or policy name and press enter. Search for and select *AWSElasticBeanstalkWebTier*, *AWSElasticBeanstalkWorkerTier*, and *AWSElasticBeanstalkMulticontainerDocker*

- On the next page, click the `Role name` field and enter `Elastic-EC2`, then create the role.

- Navigate to the AWS Elastic BeanStalk console to create a new application.

- Give your application a name, and under the Platform Tab, select Python.

- Specify the `Platform-Branch` to be even more detailed, by selecting `Python 3.9 running on 64bit Amazon Linux 2023`.
   
- Upload your application .zip file from your local computer and select v1 for the version label.

- Click `Next`.

- For the `EC2 instance profile`, click on the IAM role we previously created, `ElasticEC2`.

- Click `Next`.

- Under `VPC`, select your default VPC. The VPC allows you to have your own slice of the private cloud that no one without permission can access.

- Click `Next`.

- Configure your root volume to `General Purpose (SSD)`, 10 `GB`, and an instance type of `T.2 MICRO`.

- Continue to click `Next` until you see the page with `Submit` at the bottom.

- Click `Submit`.

**NOTE: By default, Elastic Beanstalk is going to look for a file named `application.py` in the root of the source code by default when deploying; if you use a different filename like `app.py`, it won't automatically detect it as the entry point.
This can lead to errors in deploying your application or the application not starting properly. Take the time to go back to your previously zipped file and rename the file from `app.py` to `application.py`.**

- If you see another error about your instance profile, it means an IAM instance profile must be associated with the Elastic Beanstalk environment for it to launch properly.

- In my case, I ended up re-creating a new environment, as I realized, I provided the wrong role to my configuration. I provided it an *Elastic-EC2* role, versus *aws-elasticbeanstalk-service-role*.

- I had already previously terminated the environment, due to the application.py being named incorrectly. I also removed any lingering resources like S3 buckets.

- <img width="1420" alt="Screen Shot 2023-08-17 at 7 53 00 AM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/9d327ccb-4944-44c9-a3fe-7bd852b025b0">

<img width="1420" alt="Screen Shot 2023-08-17 at 8 17 27 AM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/f4f44b92-d2e6-4925-aa2e-98833ae6753a">

<img width="1420" alt="Screen Shot 2023-08-17 at 8 17 50 AM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/356e16db-96e6-4e62-8f5f-3c488e7ddf8f">

- Then, I proceeded with the instructions from before to complete the configuration process - ensuring I had the appropriate *EC2 instance profile* of *Elastic-EC2*.

- The configuration was successfully uploaded, and my application is now running!

- <img width="1420" alt="Screen Shot 2023-08-17 at 8 52 10 AM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/b13e7970-dd2b-49e8-9c36-08ad7b955cc1">

- <img width="1420" alt="Screen Shot 2023-08-17 at 8 54 11 AM" src="https://github.com/belindadunu/Deployment_1.1/assets/139175163/59bda3d9-0397-4eb6-ace8-df4b7c8f0ef8">

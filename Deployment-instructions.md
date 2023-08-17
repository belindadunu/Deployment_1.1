<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>

## Deployment Instructions:
1. Log into the instructor's Jenkins server
2. Create and run a Jenkins build for the application (Review Jenkins setup lesson video)
3. Make sure you include your name and the number 1.1 in your build's name (first name_letter of last name_1.1)
4. Observe the pipeline stages via the console output
5. **IF** the pipeline is successful, download the application files from your repository and proceed to the next step: https://scribehow.com/shared/How_to_Create_and_Deploy_a_Python_URL_Shortener_on_AWS_Elastic_Beanstalk__MS9pB8lfRaGFiKAq2FU-cw
6. Once you deploy, your deployment to elastic beanstalk will fail or you will see a degraded health status
7. Navigate to the elastic beanstalk log tab and request the last 100 logs. Download and view  the logs
8. Use the internet or ChatGPT to assist you in discovering the issue.
9. **HINT:** The issue is located in the /var/log/web.stdout.log section 

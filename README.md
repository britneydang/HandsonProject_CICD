# HandsonProject: Continuous Integration and Continuous Deliver/Deployment

Project Description: Create CI/CD pipelines in Azure Devops to release Azure Data Factory pipelines to higher environments (Testing and Production). Also configure the Development Data Factory with the source control tool (Git) to enable collaborative development.

Azure DevOps: Saas platform on Azure for implement project. It is a combination of Development teams who are responsible for writing code and testing them and operations teams who are responsible for deploying and supporting that code in production. It includes: Boards, Repors, Pipelines, Test Plans, Artifacts
CI/CD: 

- Plan: gather the requirements, write users' stories, break down the tasks, and plan the work for a sprint or an iteration.
- Code
- Build
- Test
- Release
- Deploy to necessary environments
- Monitor
- Improve
- Once deployed your application, monitor and improve the quality of the application. That means more planning, coding, testing, releasing, deploying, and the cycle goes on.
- Continuous Integration: include the code needs to be continuously integrated to a source control system, such as Git. And build is taken for every code merged, and run some automated testing.
- Continuous Delivery/Deployment: The tested code then needs to be released and deployed. there are 2 options: continuously deploy the code to production automately (C Deployment) or with manual aprroval (C Delivery) 
- Continuous improvement: is achieved through observing the performance of the application and acting upon that.
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/a2ac57b6-26b7-4045-81f2-7c13df951523)

Azure DevOps Environment Set-up
- dev.azure.com
- Submit the Azure DevOps Parallelism Request form to get the parallelism enabled to run the CI/CD pipelines
- Create a new project:

![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/09713709-553c-40db-96d6-023278cd2b1c)

Azure Data Factory Set-up: Generally, there are Dev-ADF, Test-ADF, Prod-ADF
- enable Git in Dev-ADF
- keep 3 data factories in different resource group which is specific for their environment
- Create data factories -> create 3 resource group for 3 factories
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/4fefbb47-f746-4496-bfba-5db0fa5cade3)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/82c4c5c1-c72c-4402-bb98-0e9301fd4ad9)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/ed370683-9481-452d-a3b3-e1246ad640b8)

ADF Git Configuration: configure a Git repository to the development data factory

- Data Factory calls the master branch as the collaboration branch. No direct development should be allowed in the master branch. Developers will create feature branches to do the development work and that will merged to the master branch via a pull request later. Once publish the code from the master branch, that creates the adf_publish branch with the ARM template.
- Option (1) Create Git Repository in DevOps: DevOps -> In the project -> Repos -> Create. Option (2) to create in ADF studio
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/1af1fd87-1a99-4da3-b2b6-b2c2dabd5e5f)
- Review the branches policy
- Azure Data Factory studio for DEV -> Manage hub -> Git configuration ->
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/60ab9ed7-d603-409c-b4e7-8c78ea3a10dd)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/9a560dfa-6ef4-4f43-9296-901e46898c2d)






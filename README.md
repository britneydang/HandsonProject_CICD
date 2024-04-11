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

![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/e557f72e-2e98-4e3f-b75b-ec6dc9dd8260)

Continuous Integration:
- Process of Git-enabled Data Factory
    1. Create feature branch: ADF -> Author hub -> main branch -> new branch
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/08b1bbf1-a812-48b5-8959-a8af9b0da717)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/f644519c-1668-4329-b261-01bac268b65a)
    2. Develop pipeline: create a new simple pipeline.
    3. Debug pipeline. After debug, Save All (In previous Azure projects, I always saved by hitting publish on the top row. Now it is different. Publish is only available in the master branch)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/f647b152-b7af-49d1-9461-d16afc1162ca)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/93e73e51-d9ad-42b3-8a87-816a729a354e)
    4. Create pull request: ADF -> feature branch -> Create pull request
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/a4443cb2-8fd5-4623-80b8-fa704e0baa03)
    5. Review Change and approve pull request: Normally, other team members will need to review and approve.But with my own project, I will approve for myself.
    6. Merge the change to collaboration branch (master): click Complete -> select Merge
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/7b2d762a-9be1-4840-8baa-2d6abaaf88da)

    - Create a feature branch based on the master
    - Update the current pipeline with changes
    - Debug pipeline -> Save All
    - Pull Request
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/e5cc7eb0-1d96-4dd8-ae6d-15bfeb437bef)
    - Review change and approve
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/684e026e-d4bd-4535-941d-132c56738048)
    - Complete Merge
    7.  Publish the changes on the master branch which will submit to the DEV Data Factory Repository and also create ARM Template in the adf_publish branch
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/472d822f-cfc1-4d1c-aea0-4660c13b2b83)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/ff2ac5fe-b463-4ac9-849f-db8565e7ced3)

Continuous Delivery (with manual approval prior to deployment to production): input is the ARM in adf_publosh branch from previous process
- From the Master branch -> ARM Template -> Release ->
   - Test stage: Pre Deployment PowerShell Script (stop trigger) -> ARM Deployment -> Post Deployment PowerShell Script (start trigger) -> TEST-ADF
   - Production stage: Approval and wait for test deployment complete -> Pre Deployment PowerShell Script (stop trigger) -> ARM Deployment -> Post Deployment PowerShell Script (start trigger) -> PROD-ADF
- Create Release pipeline: DevOps -> Project -> Release -> Pipeline -> select empty job 
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/ebb65363-8429-42b3-b2bd-2c1cbc89dc3d)
    - Create Task: click on task in Stage -> + agent job -> search for ARM template -> Manager Resource Connection -> Advanced -> Add an Azure Resource Manager service connection, select the TEST resource group (Pipeline will be able to deploy the ARM template into the TEST resource group)
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/86621ded-298d-4262-bcea-fb348ca10216)
*** Azure student account doesnt support Service Principle Management, I will use Managed Service Identity instead.*** Wait for approve from https://aka.ms/azpipelines-parallelism-request 

![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/53e14b34-9c26-4c2b-8c9a-e7d1cc3c2e2c)
    - Deployment mode:
          - Incremental: t takes the objects or the resources from the ARM template and updates them within the resource group
          - Complete: it will delete every resource within the resource group and applies the ARM template to that resource group
          - Validation only: looks to see whether the ARM template has got the right information and there are no syntax errors
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/a5fe822b-e7e7-4e12-822f-3484db3c9cbd)
    - Click Trigger on Artifact
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/190a4bde-33e6-4939-aeb7-759fbcce2fe6)
- Create Release -> click on Hyperlink new release -> 
![image](https://github.com/britneydang/HandsonProject_CICD/assets/110323703/f8579b17-ba0d-4e76-9b89-5a976a5a57d6)







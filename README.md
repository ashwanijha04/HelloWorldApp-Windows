# HelloWorldApp-Windows

This is a github repository that saves the effort of manually doing it.
This was created from the below tutorial:
    https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-windows.html
    

## STEP 1:   Prepare the Windows Instance

   
   ### IAM ROLE
   1. > Go to the IAM console and select 'create role'.
   
   2. > The EC2 service is going to use this role so select EC2 from the list of services that will use this role.
   
   3. > Attach the following roles:  AmazonS3FullAccess, AWSCodeDeployRoleForECS, AWSCodeDeployFullAccess, AWSCodeDeployRole.[Feel free to change this, this repo addresses the use cases in general.]
      
   
   
   ### CodeDeploy Agent Installation - Powershell
    Set-ExecutionPolicy RemoteSigned
    --------------------------------
    Import-Module AWSPowerShell
    --------------------------------
    New-Item -Path "c:\temp" -ItemType "directory" -Force
    --------------------------------
    powershell.exe -Command Read-S3Object -BucketName aws-codedeploy-us-east-1 -Key latest/codedeploy-agent.msi -File c:\temp\codedeploy-agent.msi
    --------------------------------
    c:\temp\codedeploy-agent.msi /quiet /l c:\temp\host-agent-install-log.txt
    --------------------------------
    powershell.exe -Command Get-Service -Name codedeployagent
    --------------------------------


## STEP 2:     Deploy using CodeDeploy

   > Before proceeding further, verify that the permissions are properly set and the codedeploy-agent is properly installed.   

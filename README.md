# HelloWorldApp-Windows

This is a github repository that saves the effort of manually doing it.
This was created from the below tutorial:
    https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-windows.html
    

## STEP 1:
   Prepare the Windows Instance
   
   ### IAM ROLE
   
   
   
   ### CodeDeploy Agent Installation - Powershell
    Set-ExecutionPolicy RemoteSigned
    Import-Module AWSPowerShell
    New-Item -Path "c:\temp" -ItemType "directory" -Force
    powershell.exe -Command Read-S3Object -BucketName aws-codedeploy-us-east-1 -Key latest/codedeploy-agent.msi -File c:\temp\codedeploy-agent.msi

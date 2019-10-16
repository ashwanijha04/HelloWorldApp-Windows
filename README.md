# A sample Windows Hello World application - Deploy using CodeDeploy

### This is a github repository that saves the effort of manually doing it. Please feel free to fork this repository and use it to test the deployment to a windows EC2 instance.

### ASSUMPTION: The windows instance is launched using AWS console and aws cli comes pre-installed. If not, please install the AWS CLI manually for your windows machine.

This was created from the below tutorial:
    https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-windows.html
    

## STEP 1:   Prepare the Windows Instance

   
   ### IAM ROLE
   1. > Go to the IAM console and select 'create role'.
   
   2. > The EC2 service is going to use this role so select EC2 from the list of services that will use this role.
   
   3. > Attach the following roles:  AmazonS3FullAccess, AWSCodeDeployRoleForECS, AWSCodeDeployFullAccess, AWSCodeDeployRole.[Feel free to change this, this repo addresses the use cases in general.]
      
   
   
   ### CodeDeploy Agent Installation - Powershell
   Launch the instance and use the security groups as mentioned in this documentation:
       https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorials-windows-launch-instance.html
   
   Do not forget to add tags to the instance. You can do this later, but why forget important things like permitting some good-hearted API to use other services.
   Use powershell to execute the below command.
   
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
   
   1. Create a deployment group and add the instance to this group using tags.
   2. Select github repository. [Fork this repository in your account]
   3. Connect to github and use this repository that has been forked.
   4. Attach a service role which permits CodeDeploy to use the following roles:  AutoScalingFullAccess, AmazonS3FullAccess,  AWSCodeDeployRole. Please feel free to change these policies as per needs.




# A Simple Resource

In this example, the template picks an existing VPC and Subnet that have been created separate to this example. The reason for this is to show how values can be passed into CloudFormation as Parameters, also for the first example we can show less which is easier to follow. In example 3 we will include the creation of other resources that are required to support the instance.

This will create an Amazon Linux Instnace that you can ssh to, in this case, the user would need access to the CloudFormation console to be able to get the DNS Name and IP address of the host. They will also need a copy of the key that is used here, if you are running this example yourself, you will need to create they key in the Console under Network & Security, Key Pairs.

NOTE: This was deployed into a Public Subnet (one that has an IGW assigned), that already had the 'Automatically assign a Public IP at Launch' set to True. Without these settings, you would need to specify the public IP setting in the template.

## Using the console
You can apply the template directly from the CloudFormation console, if you are cloning this repo, or downloading the files, you can 'browse' to the step 1 sample template and run the template. It is best if you copy these templates in their folders into S3 in the following way:

yourbucket/
  step1/templates
  step2/templates
  step3/templates
  step4/templates
  
If you follow this formate then the templates will not need editing in anyway and when you run the template you'll be able to chose the 'step' and it'll install the correct resources using CloudFormation. If you chose to place the templates into S3 immediately before attempting these steps you can use the following URL structure to run the first template:

https://s3-{region}.amazonaws.com/{yourbucket}/step{number}/{template}

 * region is like = us-west-2
yourbucket = the name you gave your bucket
number = in this excersise that would be 1
template = the file name, fo rthis it's simple-stack.template

## Using the console

In the same way you have the option of using a local or remote file with the Console, you can either use a local or remote (S3) file with the CLI. Generally, putting the files in S3 first is the easiest, if you don't want to keep typing out the URL you caould always make a variable in a shell. Below is the command you can run to create a stack, note that you need to make sure ALL of the parameters have values when you run a script from the CLI. This example uses the template file that is located locally in the same folder you're running this command from, you can substitute this with an S3 URL, much in the same way you can with the Console.

```sh

aws cloudformation create-stack \
--stack-name your-stack-name \
--template-body file://sample-stack.template \
--parameters \
ParameterKey=AvailabilityZone1,ParameterValue=$AWS_AZ01 \
ParameterKey=AvailabilityZone2,ParameterValue=$AWS_AZ02 \
ParameterKey=AvailabilityZone3,ParameterValue=$AWS_AZ03 \
ParameterKey=KeyName,ParameterValue=artemis-key \
ParameterKey=PrivateSubnet1,ParameterValue=$PRIVNET01 \
ParameterKey=PrivateSubnet2,ParameterValue=$PRIVNET02 \
ParameterKey=PrivateSubnet3,ParameterValue=$PRIVNET03 \
ParameterKey=Project,ParameterValue=$PROJECT \
ParameterKey=PublicSubnet1,ParameterValue=$PUBNET01 \
ParameterKey=PublicSubnet2,ParameterValue=$PUBNET02 \
ParameterKey=PublicSubnet3,ParameterValue=$PUBNET03 \
ParameterKey=StackType,ParameterValue=$STACKTYPE \
ParameterKey=ArtemisWebSg,ParameterValue=$WEBSG \
ParameterKey=ArtemisAdminSg,ParameterValue=$ADMINSG \
ParameterKey=WebInstanceRole,ParameterValue=$WEBROLE \
ParameterKey=AdminInstanceRole,ParameterValue=$ADMINROLE \
ParameterKey=BuildNo,ParameterValue=$BUILD_NUMBER

```
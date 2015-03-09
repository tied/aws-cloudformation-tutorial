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

region is like = us-west-2
yourbucket = the name you gave your bucket
number = in this excersise that would be 1
template = the file name, fo rthis it's simple-bastion.template
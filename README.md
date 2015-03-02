# CFN Tutorial & Best Practices

Welcome to the guide. This guide will attempt to quickly help you use AWS Cloudformation, define some of the best practices and caveats and then lead you to the rest of the documentation that will help you become an expert in Cloudformation usage.

Where possible, I will try and link to the specific pages in the document that you can read if this guide isn't making sense. 

## Basics
If you're not familiar with AWS, or you haven't done this part, each AWS authored guide has a section on getting started, you might already be an expert however it might also be worth a quick read just to make sure the reader of this guide is in the same place, please have a look at:

http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/GettingStarted.html

## What is Cloudformation?




One of the most common syntax errors in a template is a missing comma between sibling property declarations and between resources.

If you make an update to an Ec2 Instance Type in Cfn, it will replace the host if the parameter is immutable, that is to say, it must replace the instance. Some of the optional parameters for each resource will only cause a reboot. If you are working with Cfn and Auto-Scaling Launch Configuraitons, you can make changes and it will not affect the running nodes. It's only if you replace them by terminating them or another even takes place, that they will take on the new configuration.

This works well if you are doing green/blue (immutable infra), in which case you just build a new stack, test it, swap the entry points and then cast away the old one once you've validated the new version. If there is an issue, you swap the endpoints back to the previous version.
# CFN Tutorial & Best Practices

Welcome to the guide. This guide will attempt to quickly help you use AWS Cloudformation, define some of the best practices and caveats and then lead you to the rest of the documentation that will help you become an expert in Cloudformation usage.

Where possible, I will try and link to the specific pages in the document that you can read if this guide isn't making sense. 

## Basics
If you're not familiar with AWS, or you haven't done this part, each AWS authored guide has a section on getting started, you might already be an expert however it might also be worth a quick read just to make sure the reader of this guide is in the same place, please have a look at:

http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/GettingStarted.html

## What is Cloudformation?

It can be best described as a tool that helps deploy infrastructure as code. The specific code is JSON formatted and when fed to CloudFormation, will direct it on what resources to create. There are other tools that do this for other products, OpenStack uses Heat (Which can also interface with other platforms), VMWare use vRealize, Azure and GCE even have their own versions but they are not as mature. Users can write templates and deploy them as stacks using the Cloudformation GUI, CLI or API. One of the great benefits of using the tool is that when it comes to cleanup, you can delete the stack and all resources that were created in it will be removed.

Stacks (Created via Templates) can be very simple, maybe a single template that just brings up a few resources like an Ec2 Instance, or they can be incredibly complex and create entire environments from the ground up. In this guide, you'll see how you can start with a simple template and eventually update it to the point of being complex (which should obviously be driven by some purpose, otherwise keep them as simple as possible).

### Template Components

All templates are JSON formated and consist of the following:
Parameters
Mappings
Conditions
Resources
Outputs
The anatomy of which looks like the following:
```sh
{
  "AWSTemplateFormatVersion" : "version date",

  "Description" : "JSON string",

  "Parameters" : {
    set of parameters
  },

  "Mappings" : {
    set of mappings
  },

  "Conditions" : {
    set of conditions
  },

  "Resources" : {
    set of resources
  },

  "Outputs" : {
    set of outputs
  }
}
```
You can view the documentation for the Template Anatomy here:
http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html


**NOTE:** One of the most common syntax errors in a template is a missing comma between sibling property declarations and between resources. The other one which isn't mentioned in the manuals is an extra trailing comma after the last resource in a set of braces, which will also cause it to fail.


### Template Limits
Limits are ever changing, whenever new services and updates are released to AWS, limits can change. Some limits can also be changed by asking AWS if you have a valid reason. For Cloudformation specific limits, please check here:
http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html




If you make an update to an Ec2 Instance Type in Cfn, it will replace the host if the parameter is immutable, that is to say, it must replace the instance. Some of the optional parameters for each resource will only cause a reboot. If you are working with Cfn and Auto-Scaling Launch Configuraitons, you can make changes and it will not affect the running nodes. It's only if you replace them by terminating them or another even takes place, that they will take on the new configuration.

This works well if you are doing green/blue (immutable infra), in which case you just build a new stack, test it, swap the entry points and then cast away the old one once you've validated the new version. If there is an issue, you swap the endpoints back to the previous version.
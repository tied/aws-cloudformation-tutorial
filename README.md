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


## Template Design
This section is probably the hardest to write becauase the ways in which Cloudformation can be consumed are very broad. What needs to be decided first is the kind of environment that's needed. Sometimes it is sufficient to use only Cloudformation to complete the configuration and deployment of a service.
A scenario here could be that we want to deploy 2 LDAP servers into the VPC that we own, in which case we could configure these purely using Cloudformation, or they could be part of a bigger management stack that would deploy multiple tiers and services, most likely from separate child templates linked together by a parent.

The following steps in this repo are an intended fast track into seeing how templates and Cloudformation usage can evolve over time. At the beginning of any project most templates are a single file, however over time and with discovery of new options or services that are needed, templates split apart and operate in a Parent/Child model, or become separate entities managed by a higher level orchestration tool, maybe Jenkins.

If you intend to follow the guide because you can't wait to get your hands dirty, it is worth coming back and reading the rest of this page to understand some of the pitfalls and caveats of using Cloudformation as there are some activities that aren't obvious which can influence the way you deploy, or even break your existing resources.



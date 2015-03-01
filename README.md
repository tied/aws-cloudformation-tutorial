# My CFN Tutorial

One of the most common syntax errors in a template is a missing comma between sibling property declarations and between resources.

If you make an update to an Ec2 Instance Type in Cfn, it will replace the host if the parameter is immutable, that is to say, it must replace the instance. Some of the optional parameters for each resource will only cause a reboot. If you are working with Cfn and Auto-Scaling Launch Configuraitons, you can make changes and it will not affect the running nodes. It's only if you replace them by terminating them or another even takes place, that they will take on the new configuration.

This works well if you are doing green/blue (immutable infra), in which case you just build a new stack, test it, swap the entry points and then cast away the old one once you've validated the new version. If there is an issue, you swap the endpoints back to the previous version.

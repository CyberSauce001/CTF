# Secret Seeker - Part 1

## Introduction
This guide will walk you through the process of discovering and decoding a secret flag within a Kubernetes environment.
Website can be found here: https://eksclustergames.com

### Prerequisites
- Access to a Kubernetes cluster
- Basic familiarity with terminal commands

## Steps

1. **Identify Current Environment**
   - Determine the current working directory: `pwd`
   - Identify the current user: `whoami`
   - Check Kubernetes user: `kubectl whoami`

2. **Authorization Check**
   - Review available authorizations: `kubectl auth can-i --list`
   - Explore authorization commands: `kubectl auth can-i --help`

3. **Discover Secrets**
   From the list you can see that there is a secret under resources.
   - List available secrets: `kubectl get secrets`
   You should see log-rotate when you get secrets. 
   - Select a secret for further investigation: e.g., `kubectl get secrets log-rotate`

4. **Decode Secret**
   - Output the data of secret: `kubectl get secrets log-rotate -o yaml` or ' `kubectl get secrets log-rotate -o json | jq`
   - Identify the encoded flag within the output.
   - Decode the flag:
     - Option 1: Use terminal command `base64 -d <<< '[insert your flag base64]'`
     - Option 2: Utilize CyberChef tool:
       [CyberChef Tool](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=aHR0cHM6Ly9la3NjbHVzdGVyZ2FtZXMuY29tLw)
       - Drag "From Base64" to Recipe
       - Paste the encoded flag and decode.

5. **Proceed to Next Stage**
   - Enter the decoded flag to progress to the next stage.

# Registry Hunt - Part 2

## Conclusion
By following these steps, you can effectively navigate through a Kubernetes environment, identify secrets, and decode hidden information.

For more information and troubleshooting, refer to Kubernetes documentation or seek assistance from your administrator.

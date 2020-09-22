# VMworld2020

This repository contains the code which was used to create the NSX-T demo security framework as shown during the VMworld 2020 session `ISNS2315/ISNS2315D - Permit This, Deny That - Design Principles for the NSX Distributed Firewall`.

The complete configuration is written within a single JSON file that describes the groups, security policies and rules which are to be created on the NSX-T Manager.

It is not meant to be a turn key security policy that can be applied to every environment. It is meant to give you an example of one way of doing things, and maybe foster some ideas for how you could design your own security framework within your own organisation.

## Instructions

> IMPORTANT: This configuration should only be applied in a lab/dev/test NSX Manager. It modifies the default rule with an action of DROP, which will do exactly as it says and will drop all traffic. There are also other rules which may permit or deny existing traffic which may cause adverse results. Consider yourself warned!!!

The example code below shows how to apply the configuration against a NSX-T manager with the following details:

- NSX-T Manager: `192.168.172.104`
- NSX-T Username: `admin`
- NSX-T Password: `VMware1!VMware1!`

> As Mentioned in the presentation, it will be your responsibility to deploy your own test VMs and add them to groups or tag them.

### Visual Studio Code (VSCode)

- Search for and install the VSCode Extension called `REST Client` by `Huachao Mao`
- In VSCode, Open the file `ISNS2315D.http`
- Modify the `NSXManager`, `NSXUsername` and `NSXPassword` variables at the top of the file to suit your environment.
- Click the `Send Request` link above the request
- The request will get sent to the NSX Manager and a new window will open with the response or any error messages received from the NSX-T Manager.

### cURL

- Issue the following cURL command

```bash
curl --request PATCH \
  --url https://192.168.172.104/policy/api/v1/infra \
  --header 'authorization: Basic YWRtaW46Vk13YXJlMSFWTXdhcmUxIQ==' \
  --header 'content-type: application/json' \
  --data @ISNS2315D.json \
  --insecure
```

- If there are no errors, there will be no response

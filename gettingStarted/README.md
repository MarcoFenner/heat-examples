## Getting started 

This template can be used to deploy a single server with every CLI-Clients you need to start working with the SysEleven Stack. It is meant as an alternative to install OpenStack Clients by hand on 
your local machine, which is documented [here](https://doc.syselevenstack.com/en/tutorials/openstack-cli/).

Prerequisites:  
- You need to import a valid SSH public key as described [here](https://doc.syselevenstack.com/en/tutorials/firststeps/)


### Launch the heat template

- Navigate to Orchestration --> Stacks --> Launch Stack to start a template.
- Select "URL" in the Template Source select box.
- Paste the URL of the template into Template URL:  
  `https://raw.githubusercontent.com/syseleven/heattemplates-examples/master/gettingStarted/sysElevenStackKickstart.yaml`
- Don't change the field Environment Source and click Next.
- Write "kickstart" into the field Stackname.
- Write the name of our public SSH-Key as parameter key_name.
- Afterwards we click Launch.

After a couple of seconds you should see a new machine spawning under --> "Compute" --> "Instances".  
Copy the IP address from "Floating IPs" and you should be ready to login via SSH.

```bash
ssh syseleven@< Floating IP >
```

The home directory has a prepared ["openrc" file](https://doc.syselevenstack.com/en/tutorials/api-access/#setting-up-the-environment-variables), 
which allows you to work with openstack endpoints. The required values can be found under [Project --> Access and Security --> API Access](https://dashboard.cloud.syseleven.net/horizon/project/access_and_security/?tab=access_security_tabs__api_access_tab) --> View Credentials.

Open it with a text editor of your choice.

```bash
syseleven@kickstart:~$ nano openrc
```

You just need to adjust `OS_TENANT_NAME`, `OS_USERNAME` and `OS_PASSWORD` to the actual values.
To be able to use the command line tools just source the environment variables:

```bash
source openrc
```

Now you are ready to deploy any template from this repository or any other heat template.
As a quick test we can list our currently running machines:

```bash
syselevenstack@kickstart:~$ openstack server list
+--------------------------------------+-----------+--------+--------------------------------------------+
| ID                                   | Name      | Status | Networks                                   |
+--------------------------------------+-----------+--------+--------------------------------------------+
| a54d0883-988b-4730-a533-2c91fc66c518 | kickstart | ACTIVE | kickstart-net=10.0.0.10, 185.56.135.235    |
+--------------------------------------+-----------+--------+--------------------------------------------+
```


# Simple CoreOS example

## Overview

Using this template you can start any number of CoreOS instances. 

## Usage

1. Upload the CoreOS image. Use our helper script:

    ```$ ./upload_replacing_coreos_image.sh```

    It will download the [official coreOS image](https://coreos.com/os/docs/latest/booting-on-openstack.html), delete any of your existing images named `private_coreos` and upload it your SysEleven Stack image store.
    
    The script will ensure you always use the latest production release.

2. Launch the CoreOS cluster.

    ```$ openstack stack create -t cluster.yaml <stack name> --parameter key_name=<ssh key name> --wait```

    There should be a number of instances with 1 NginX docker container deployed and running on every machine listening on port 80.

## Parameters

- **key_name** – ssh key name
- **number_instances** number of CoreOS instances to spawn
  - default: 1
- **flavor** instance types. You can find a list of the available [flavors in the documentation](https://doc.syselevenstack.com/en/documentation/compute/#instance-types)


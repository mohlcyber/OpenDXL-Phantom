# OpenDXL-Phantom
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This integration is focusing on the threat intelligence sharing with McAfee OpenDXL and the orchestrations platform Phantom. This App provides the capability to publish Threat Information from Phantom to the McAfee Data Exchange Layer messaging bus.
This App supports the following actions:

1. lookup md5 Hash with McAfee Active Response - **lookup hash**
2. push md5 hash into the TIE Database with a reputation score - **post hash**
3. push an event over the McAfee DXL fabric - **post ip**
4. validate the asset configuration for DXL connectivity - **test connectivity**

More actions will follow in the future.

## Component Description

**Phantom** is a community powered security automation and orchestration platform. https://www.phantom.us/

## Prerequisites

Phantom Platform tested with version 3.0.251

McAfee OpenDXL Certificate Files Creation ([Link](https://opendxl.github.io/opendxl-client-python/pydoc/certcreation.html))

## Configuration

Download the [Latest release](https://github.com/mohl1/OpenDXL-Phantom/releases) and extract the files. Move the certificates and config files (mentioned in the prerequisites) into the certs folder.
The app includes already OpenDXL library files (DXL 3.1.0.586, TIE 0.1.0, MAR 0.1.2-beta) that don't need to be configured.

Open the Phantom platform and go to Apps. Under Apps click **install app** and upload the tgz file.

<img width="1058" alt="screen shot 2017-08-09 at 09 29 29" src="https://user-images.githubusercontent.com/25227268/29109981-58d21984-7ce5-11e7-8e93-98d8e6439420.png">

Configure a new asset and provide an asset name. In the asset settings define a DXL topic and a test message.

<img width="570" alt="screen shot 2017-08-09 at 09 34 06" src="https://user-images.githubusercontent.com/25227268/29110149-f2cd6372-7ce5-11e7-9642-070c9515d431.png">

Click test connectivity. This will publish a DXL message on the configured topic.

<img width="480" alt="screen shot 2017-08-09 at 11 18 11" src="https://user-images.githubusercontent.com/25227268/29114397-78c4bc74-7cf4-11e7-80e2-37a73441cbf3.png">

Optional create a OpenDXL subscriber to listen and visualize the test message.

For the TIE component the Python client must be authorized to send messages to the /mcafee/service/tie/file/reputation/set topic which is part of the TIE Server Set Enterprise Reputation authorization group.
Follow the following KB. 

https://opendxl.github.io/opendxl-tie-client-python/pydoc/basicsetreputationexample.html

The same authotization must be granted to the McAfee Active Response Server API. 

https://opendxl.github.io/opendxl-client-python/pydoc/marsendauth.html

## Summary

With this integration it is possible to extend capabilities of the McAfee DXL messaging fabric as well as the Phantom Platform by performing key action for containment and remediation. 

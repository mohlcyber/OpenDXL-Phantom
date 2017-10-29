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

McAfee ePolicy Orchestrator 5.3. - 5.x

McAfee DXL Broker 4.x

## Configuration

The app includes already OpenDXL library files (DXL 4.0.0.416, TIE 0.1.0, MAR 0.1.2-beta) that don't need to be configured.

Open the Phantom platform and go to Apps. Under Apps click **install app** and upload the tgz file.

<img width="1325" alt="screen shot 2017-10-29 at 22 38 05" src="https://user-images.githubusercontent.com/25227268/32148603-e9b81b84-bcf9-11e7-9b42-1d70a7f3a459.png">

Configure a new asset and provide an asset name. In the asset settings define the ePO IP/Hostname, ePO Username, ePO Password, DXL topic and a test message.

<img width="710" alt="screen shot 2017-10-29 at 22 40 00" src="https://user-images.githubusercontent.com/25227268/32148624-25af1c46-bcfa-11e7-87b7-43a7a1788532.png">

Click test connectivity. This will check if certificates got created already if not it will generate new certiticates and add them to ePO. After the certificates got created the app will publish a DXL message on the configured topic.

<img width="899" alt="screen shot 2017-10-29 at 22 44 26" src="https://user-images.githubusercontent.com/25227268/32148671-e4ea5652-bcfa-11e7-8fed-153962256afc.png">

Optional create a OpenDXL subscriber to listen and visualize the test message. (e.g. https://github.com/opendxl/opendxl-console)

For the TIE component the Python client must be authorized to send messages to the /mcafee/service/tie/file/reputation/set topic which is part of the TIE Server Set Enterprise Reputation authorization group.
Follow the following KB. 

https://opendxl.github.io/opendxl-tie-client-python/pydoc/basicsetreputationexample.html

The same authotization must be granted to the McAfee Active Response Server API. 

https://opendxl.github.io/opendxl-client-python/pydoc/marsendauth.html

## Summary

With this integration it is possible to extend capabilities of the McAfee DXL messaging fabric as well as the Phantom Platform by performing key action for containment and remediation. 

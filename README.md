# OpenDXL-Phantom
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This integration is focusing on the threat intelligence sharing with McAfee OpenDXL and the orchestrations platform Phantom. This App provides the capability to subscribe and publish DXL Threat Information.
This App supports the following actions:

1. validate the asset configuration for DXL connectivity (topic: /phantom/event/test)- **test connectivity**
2. push an IP over the McAfee DXL fabric (topic: /phantom/event/ip) - **post ip**
3. push md5 hash into the TIE Database with a reputation score - **set reputation**
4. lookup md5 Hash with McAfee Active Response - **hunt file**
5. communicate to a DXL services and parse response - **lookup service**
6. subscribe to DXL Topics and poll DXL messages - **on poll**

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

<img width="1335" alt="screen shot 2017-12-06 at 16 38 28" src="https://user-images.githubusercontent.com/25227268/33669897-f2962fc6-daa3-11e7-9f73-aac7ae298a00.png">

Configure a new asset and provide an asset name. In the asset settings define the ePO IP/Hostname, ePO Username, ePO Password, DXL topic and a test message. Also define a parser and a DXL topic for subscription. The parser for ATD DXL messages is already included.

<img width="703" alt="screen shot 2017-12-06 at 16 40 12" src="https://user-images.githubusercontent.com/25227268/33669981-2947f9d2-daa4-11e7-83d2-35fea8846ca6.png">

Click test connectivity. This will check if certificates got created already if not it will generate new certiticates and add them to ePO. After the certificates got created the app will publish a DXL message on the configured topic.

<img width="899" alt="screen shot 2017-10-29 at 22 44 26" src="https://user-images.githubusercontent.com/25227268/32148671-e4ea5652-bcfa-11e7-8fed-153962256afc.png">

Optional create an OpenDXL subscriber to listen and visualize the test message. (e.g. https://github.com/opendxl/opendxl-console).

To use the Phantom app to subscribe to DXL messages go to Ingest settings and define the label that should apply to objects from this source. Click poll now. 

The poll now will check if a DXL subscriber script is running already and will stop it. It will check if the configured DXL topic is already in the DXL subscriber script. If not it will add the new topic to the script and start the subscriber.

<img width="898" alt="screen shot 2017-11-20 at 09 50 55" src="https://user-images.githubusercontent.com/25227268/33009834-64c8afe8-cdd8-11e7-886b-cbbf8645e6d0.png">


For the TIE component the Python client must be authorized to send messages to the /mcafee/service/tie/file/reputation/set topic which is part of the TIE Server Set Enterprise Reputation authorization group.
Follow the following KB. 

https://opendxl.github.io/opendxl-tie-client-python/pydoc/basicsetreputationexample.html

The same authotization must be granted to the McAfee Active Response Server API. 

https://opendxl.github.io/opendxl-client-python/pydoc/marsendauth.html

## Summary

With this integration it is possible to extend capabilities of the McAfee DXL messaging fabric as well as the Phantom Platform by performing key action for containment and remediation. 

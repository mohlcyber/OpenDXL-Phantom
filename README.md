# OpenDXL-Phantom
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This integration is focusing on the threat intelligence sharing with McAfee OpenDXL and the orchestrations platform Phantom. This App provides the capability to subscribe and publish DXL Threat Information.
This App supports the following actions:

1. **test connectivity** - Validate the asset configuration for DXL connectivity.
2. **post ip** - Push an event over the McAfee DXL fabric
3. **set reputation** - Push a MD5 Hash into the TIE Database
4. **file reputation** - Receive File Reputations from McAfee TIE
5. **hunt file** - Lookup MD5 Hash with McAfee Active Response
6. **lookup service** - Communicate to a DXL services and parse response.
7. **on poll** - Subscribe to DXL Topics and poll DXL messages.

More actions will follow in the future.

## Component Description

**Phantom** is a community powered security automation and orchestration platform. https://www.phantom.us/

## Prerequisites

Phantom Platform tested with version 4.1.94

McAfee ePolicy Orchestrator 5.3. - 5.x

McAfee DXL Broker 4.x

## Configuration

The app includes already OpenDXL library files (DXL 4.1.0.185, TIE 0.2.0, MAR 0.2.0) that don't need to be configured.

Open the Phantom platform and go to Apps. Under Apps click **install app** and upload the tgz file.

<img width="1423" alt="Screenshot 2019-06-13 at 17 48 56" src="https://user-images.githubusercontent.com/25227268/59447889-5d6dc880-8e04-11e9-8b32-fdc6fc2cbfb6.png">

Configure a new asset and provide an asset name. In the asset settings define the ePO IP/Hostname, ePO Username, ePO Password, DXL topic and a test message. Also define a parser, Phantom Authorization Token and a DXL topic for subscription.
The authorization token can be created in the User Management.

The parser for ATD DXL messages is already included.

<img width="711" alt="Screenshot 2019-06-13 at 17 49 54" src="https://user-images.githubusercontent.com/25227268/59447949-76767980-8e04-11e9-8739-d83c7a78accb.png">

Click test connectivity. This will check if certificates got created already if not it will generate new certiticates and add them to ePO. After the certificates got created the app will publish a DXL message on the configured topic.

<img width="812" alt="screenshot 2018-11-16 at 16 00 56" src="https://user-images.githubusercontent.com/25227268/48629091-095b4c80-e9b9-11e8-90b9-91a5aecf8a55.png">

Optional create an OpenDXL subscriber to listen and visualize the test message. (e.g. https://github.com/opendxl/opendxl-console).

To use the Phantom app to subscribe to DXL messages go to Ingest settings and define the label that should apply to objects from this source. Click poll now. 

The poll now will check if a DXL subscriber script is running already and will stop it. It will check if the configured DXL topic is already in the DXL subscriber script. If not it will add the new topic to the script and start the subscriber.

<img width="811" alt="screenshot 2018-11-16 at 16 01 11" src="https://user-images.githubusercontent.com/25227268/48629205-52ab9c00-e9b9-11e8-9ece-a24fa4f42044.png">

For the TIE component the Python client must be authorized to send messages to the /mcafee/service/tie/file/reputation/set topic which is part of the TIE Server Set Enterprise Reputation authorization group.
Follow the following KB. 

https://opendxl.github.io/opendxl-tie-client-python/pydoc/basicsetreputationexample.html

The same authotization must be granted to the McAfee Active Response Server API. 

https://opendxl.github.io/opendxl-client-python/pydoc/marsendauth.html

## Summary

With this integration it is possible to extend capabilities of the McAfee DXL messaging fabric as well as the Phantom Platform by performing key action for containment and remediation. 

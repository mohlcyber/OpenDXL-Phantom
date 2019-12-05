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

The app includes already OpenDXL libraries that don't need to be configured. The dxl.tgz will download all required dependencies from the internet. If no internet connection is available please use the dxl_standalone.tgz that includes all dependencies already.

Open the Phantom platform and go to Apps. Under Apps click **install app** and upload the tgz file.

<img width="1423" alt="Screenshot 2019-06-13 at 17 48 56" src="https://user-images.githubusercontent.com/25227268/59447889-5d6dc880-8e04-11e9-8b32-fdc6fc2cbfb6.png">

Configure a new asset and provide an asset name. In the asset settings define the ePO IP/Hostname or OpenDXL Broker IP/Hostname, Port, Username and Password. Optionally DXL test message, DXL topic for subscription and a Phantom Authorization Token. The authorization token can be created in the Phantom User Management.

The parser for ATD DXL messages (Topic: /mcafee/event/atd/file/report) and TIE File Reputation Changes (Topic: /mcafee/event/tie/file/repchange/broadcast) are included already.

<img width="711" alt="Screenshot 2019-06-13 at 17 49 54" src="https://user-images.githubusercontent.com/25227268/59447949-76767980-8e04-11e9-8739-d83c7a78accb.png">

Click test connectivity. This will check if certificates got created already if not it will generate new certiticates and add them to ePO or OpenDXL Broker. After the certificates got created the app will publish a DXL message on the configured following test topic - /phantom/event/test.

<img width="907" alt="Screenshot 2019-06-13 at 17 51 59" src="https://user-images.githubusercontent.com/25227268/59447987-89894980-8e04-11e9-8281-a3013bacae4c.png">

Optional create an OpenDXL subscriber to listen and visualize the test message. (e.g. https://github.com/opendxl/opendxl-console).

To use the Phantom app to subscribe to DXL messages go to Ingest settings and define the label that should apply to objects from this source. Click poll now. 

The poll now will check if a DXL subscriber script is running already and will stop it. It will check if the configured DXL topic is already in the DXL subscriber script. If not it will add the new topic to the script and start the subscriber.

<img width="900" alt="Screenshot 2019-06-13 at 17 54 05" src="https://user-images.githubusercontent.com/25227268/59448035-a4f45480-8e04-11e9-836f-614780d0672d.png">

For the TIE component, the certificates must be authorized to Set Enterprise / External Reputations.
Follow the following KB. 

https://opendxl.github.io/opendxl-tie-client-python/pydoc/basicsetreputationexample.html

The same authotization must be granted to the McAfee Active Response Server API. 

https://opendxl.github.io/opendxl-client-python/pydoc/marsendauth.html

!!! Please keep in mind the username and password will only be used during setup (certificate creation process). Afterward the username and password can be changed !!!

## Summary

With this integration it is possible to extend capabilities of the McAfee DXL messaging fabric as well as the Phantom Platform by performing key action for containment and remediation. 

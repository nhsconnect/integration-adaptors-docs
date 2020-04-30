# integration-adaptors-docs
Documentation for National Integration Adaptors project


## Summary
The purpose of this page is to provide an overview of National Integration Adaptors and how they play a part in the wider GP Connect API strategy.  It will also provide a more detailed view, technical guidance to install, integrate and test each adaptor.  

The content of this repository will eventually be moved into the [NHS Digital Developer](https://digital.nhs.uk/developer) portal.

## National Integration Adaptors Overview
The NHS are introducing a number of client-side adaptors to complement the existing [API technologies](https://digital.nhs.uk/developer/developer-reference/api-technologies-at-nhs-digital) on offer to accelerate integration with national NHS systems.
These adaptors hide the complexity of integration with the interfaces provided by the current set of national systems by implementing an client side adaptor layer. The integrating supplier sees only a simplified and standardised set of interfaces which the adaptor layer presents. The adaptor layer is responsible for interacting with the legacy NHSD interface estate.


NHS Digital are providing adaptors shown as the "Adaptor Layer". This list of adaptors shown here is only an illustrative example.  A full list and roadmap of adaptors and when they will be available will be published in due course.
![NIA Overview](img/High%20Level%20Architecture.png)
 
A supplier is therefore required only to implement a simplified set of standard clients to the adaptor layer, integrating with a simplified and standardised set of interfaces exposed by the Adaptor layer. This set of clients is shown in the "Interface Layer" as highlighted in the diagram above.


## Pre-requisites for Integration Adaptors

### Onboarding

The purpose of each adaptor is to enable access to national NHS Systems.  As an enabler, the adaptor will need to be configured to integrate with the relevant NHS environment(s).  Therefore you will need to register your intention to use adaptors through the standard NHS onboarding process which can be found [here](https://digital.nhs.uk/services/operations) within the NHS Operations overview. 

### Open Test and Path To Live Access

In order to perform end-to-end testing of the MHS Adaptor, you will require access to an NHS Digital test environment. The MHS adaptor connects to the following two test endpoints which are available in an NHS Digital test environment:
•	Spine Core Mocked endpoint - which you will use to send and receive messages
•	SDS mocked directory - which is used to lookup routing and reliability information

NHS Digital provides several environments to test these adaptors against:  

OpenTest as an environment which can be used to perform initial test activities such as proof of concepts where an Health & Social Care Network (HSCN) connection is not available. 

All other integration test activities are to be performed within a Path To Live environment.  These activities include Development, Integration, Deployment and Non-functional tests.

To set up and configure OpenTest up please use [Set up NHS Digital OpenTest connection](https://github.com/nhsconnect/integration-adaptors/blob/develop/setup-opentest.md). 

To set up and configure Path to Live connectivity, please see [Path to Live environments](https://digital.nhs.uk/services/path-to-live-environments). 

## Adaptors

### Message Handling System (MHS)

The MHS Adaptor implements a messaging standard called the External Interface Specification, which defines in some detail a number of patterns for transport layer communication with the NHS Spine. The intent of this MHS Adaptor is to hide this implementation detail from the supplier, and so make it easier to connect to Spine and perform business operations such as interacting with Spine services like PDS.

For specific documentation relating to MHS then please click [here](MHS/README.md). 


### NHAIS

The NHAIS adaptor allows General Practice (GP) Surgeries to keep their patient registration and demographics data in sync with the regional Health Authorities (HA).


For specific documentation relating to NHAIS then please click [here](NHAIS/README.md). 





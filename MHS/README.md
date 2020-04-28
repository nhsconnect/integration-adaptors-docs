# Message Handling System

The MHS Adaptor implements a messaging standard called the External Interface Specification, which defines in some detail a number of patterns for transport layer communication with the NHS Spine. The intent of this MHS Adaptor is to hide this implementation detail from the supplier, and so make it easier to connect to Spine and perform business operations such as interacting with Spine services like PDS.
The MHS adaptor is composed of three main services, coloured in orange, which are executed in Docker containers:
1.	The MHS Outbound Service which is responsible for listening for requests from the wider local system context and transmitting these to Spine
2.	Spine Route Lookup, which is used to lookup routing and reliability information from Spine's directory service.
3.	the MHS Inbound Service which is responsible for listening for incoming requests from Spine.
This Link provides a view of the services and Python modules which make up the MHS Adaptor based on the AWS Architecture Exemplar.  ***Remove???? Or simpify***
The Integration-Adaptors MHS Github repo has significant details about this Adaptor including API Documentation, example Postman collection requests, AWS and Azure Deployment Exemplars and Terraform resources that you may find useful.  



## Onboarding
As outlined in section 2, the purpose of each adaptor is to enable access to national NHS Systems.  As an enabler, the adaptor will need to be configured to integrate with the relevant NHS environment(s).  Therefore you will need to register your intention to use adaptors through the standard NHS onboarding process which can be found here within the NHS Operations overview. 


## Installation & Configuration inc dependencies 

### Open Test and Path To Live Access

In order to perform end-to-end testing of the MHS Adaptor, you will require access to an NHS Digital test environment. The MHS adaptor connects to the following two test endpoints which are available in an NHS Digital test environment:
•	Spine Core Mocked endpoint - which you will use to send and receive messages
•	SDS mocked directory - which is used to lookup routing and reliability information
NHS Digital provides OpenTest as an environment which can be used to perform test activities where an Health & Social Care Network (HSCN) connection is not available. 


To set up and configure OpenTest up please use Set up NHS Digital OpenTest connection.  ***Dev work/spikes/POC’s***

To set up and configure Path to Live connectivity, please see Path to Live environments.  ***Int env testing***



## MHS Services and how to Deploy them

The installation guides within this section are based on NHSD’s recommended implementation patterns.  These patterns are detailed in two Exemplar Architectures available for AWS and Azure. 

A Docker image for each MHS service has been created and can be found within Docker Hub along with the relevant install guidelines.

### Outbound
The MHS Outbound Service which is responsible for listening for requests from the wider local system context and transmitting these to Spine.

The MHS Adaptor presents a simple HTTP synchronous interface which is used to make requests to Spine via the Outbound API.
Please refer to OutBound API Documentation for specific details.  ***Meeting with Tony H today to define format****  

The docker image and associated installation guide for this service can be found here.  ****Install instructions still moving to GITHUB???****


### Inbound
The MHS Inbound Service which is responsible for listening for incoming requests from Spine only.

The docker image and associated installation guide for this service can be found  here.


### Spine Route Lookup
Spine Route Lookup, which is used to lookup routing and reliability information from Spine's directory service.

The docker image and associated installation guide for this service can be here.


## Integration Testing
MM to add

## Operating/Administration Considerations

Click here for suggestions on how you might operate this Adaptor in your own Infrastructure.  This covers areas such as Log consumption, Tooling, Audit etc 

## Troubleshooting

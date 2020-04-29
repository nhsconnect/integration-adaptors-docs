# Message Handling System

The MHS Adaptor implements a messaging standard called the External Interface Specification, which defines in some detail a number of patterns for transport layer communication with the NHS Spine. The intent of this MHS Adaptor is to hide this implementation detail from the supplier, and so make it easier to connect to Spine and perform business operations such as interacting with Spine services like PDS.

The following illustration shows the MHS adaptor in the wider systems context:
![MHS System Context](../img/MHS%20HLD.png)


The MHS adaptor is composed of three main services which are executed in Docker containers:
1.	The MHS Outbound Service which is responsible for listening for requests from the wider local system context and transmitting these to Spine
2.	Spine Route Lookup, which is used to lookup routing and reliability information from Spine's directory service.
3.	the MHS Inbound Service which is responsible for listening for incoming requests from Spine.


This [Link](https://github.com/nhsconnect/integration-adaptors/blob/develop/documentation/MHSLogicalArchitecture.pdf) provides a view of the services and Python modules which make up the MHS Adaptor based on the AWS Architecture Exemplar. 

The Integration-Adaptors MHS [Github repo](https://github.com/nhsconnect/integration-adaptors/tree/develop/mhs) has significant details about this Adaptor including API Documentation, example Postman collection requests, AWS and Azure Deployment Exemplars and Terraform resources that you may find useful.  

## MHS Services and how to Deploy them

The installation guides within this section are based on NHSD’s recommended implementation patterns.  These patterns are detailed in two Exemplar Architectures available for [AWS](https://github.com/nhsconnect/integration-adaptors/blob/develop/documentation/MHSAWSDeploymentDiagram.pdf) and Azure. 

A Docker image for each MHS service has been created and can be found within Docker Hub along with the relevant install guidelines.

### Outbound
The MHS Outbound Service which is responsible for listening for requests from the wider local system context and transmitting these to Spine.

The MHS Adaptor presents a simple HTTP synchronous interface which is used to make requests to Spine via the Outbound API.
Please refer to [OutBound API](https://github.com/nhsconnect/integration-adaptors/blob/develop/mhs/outbound/openapi-docs.html) Documentation for specific details.   

The docker image and associated installation guide for this service can be found [here](https://hub.docker.com/r/nhsdev/nia-mhs-outbound).  

### Inbound
The MHS Inbound Service which is responsible for listening for incoming requests from Spine only.

The docker image and associated installation guide for this service can be found [here](https://hub.docker.com/r/nhsdev/nia-mhs-inbound).


### Spine Route Lookup
Spine Route Lookup, which is used to lookup routing and reliability information from Spine's directory service.

The docker image and associated installation guide for this service can be found [here](https://hub.docker.com/r/nhsdev/nia-mhs-route).


## Integration Testing
MM to add

## Operating/Administration Considerations

Click [here](https://github.com/nhsconnect/integration-adaptors/blob/develop/mhs/operating-mhs-adaptor.md) for suggestions on how you might operate this Adaptor in your own Infrastructure.  This covers areas such as Log consumption, Tooling, Audit etc 

## Troubleshooting

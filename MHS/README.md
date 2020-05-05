# Message Handling System (MHS)

The MHS Adaptor implements a messaging standard called the External Interface Specification, which defines in some detail a number of patterns for transport layer communication with the NHS Spine. The intent of this MHS Adaptor is to hide this implementation detail from the supplier, and so make it easier to connect to Spine and perform business operations such as interacting with Spine services like PDS.  This is done by providing a simple interface to allow HL7 messages to be sent to a remote Message Handler.

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
This section explains how to send requests to OpenTest which is the NHS Spine Test System. The requests are sent via the docker containers which can be setup following the section [Starting the services as docker containers](https://github.com/nhsconnect/integration-adaptors/tree/develop/integration-tests/integration_tests#starting-the-services-as-docker-containers)

1. Open Visual Studio (or your preferred IDE)
2. Check out the [integration-adaptor](https://github.com/nhsconnect/integration-adaptors) project from the develop branch in Gitbub
3. In the project root, create the directory `.vscode` if it doesnt exist already
4. In the vscode folder, create a file called `settings.json`
5. Add the information below to the `settings.json` file

`{
    "python.pythonPath": "/usr/local/bin/python3",
    "workbench.settings.editor": "json",
    "workbench.settings.useSplitJSON": true,
    "rest-client.environmentVariables": {
        "$shared": {},
        "$sample_mhs_environment": {
            "BASE_URL": "http://localhost",
                        "INBOUND-PORT": "8082",
                        "OUTBOUND-PORT": "80",
                        "ROUTE-LOOKUP-PORT": "8088",
                        "FAKE-SPINE-PORT": "8091",
                        "ASID": "9XXXXXXXXXXX",
                        "PARTY-KEY": "A9XXXX-XXXXXXX"
        }
    }
}`

6. Navigate the code directories to the requests: `/rest-client/mhs/outbound`
7. Navigate to the folder of the message pattern type you wish to run a request for and open a request .http file
8. In the bottom right corner of VS Code, click `No Environment` and select `$sample_mhs_environment`
9. Change the data `@PATIENT_NHS_NUMBER` to be a number which is valid in OpenTest.  A valid number can be found in the correct integration test for the same message pattern type

Example integration tests have been provided and can be found in:
`/integration-tests/integration_tests/integration_tests/end_to_end_tests`
1. Click the `Send Request` link which can be found inside the .http file request

## Operating/Administration Considerations

Click [here](https://github.com/nhsconnect/integration-adaptors/blob/develop/mhs/operating-mhs-adaptor.md) for suggestions on how you might operate this Adaptor in your own Infrastructure.  This covers areas such as Log consumption, Tooling, Audit etc 

## Troubleshooting/FAQ

### Spine External Interface Specification (EIS)
Integrators may find it beneficial to familarise themselves with Spines EIS and in particular, Part 3 - Message Interaction Map.  The [EIS](https://digital.nhs.uk/developer/api-specifications/spine-external-interface-specification) is a complete set of technical documents with the necessary information to connect to the Spine national services via HL7 V3 APIs.  

### Sync-async=true Requests - Performance
This request type effectively turns synchronous requests into synchronous ones. This request type by its own nature will be slower than the asynchronous requests because they must wait for a reply from Spine. There are two specific variables that control how often and for how long the MHS workflow will wait for a reply:

    * 'MHS_RESYNC_RETRIES' (outbound only) The total number of attempts made to the sync-async store during resynchronisation, defaults to '20'

    * 'MHS_RESYNC_INTERVAL' (outbound only) The time in between polls of the sync-async store, the interval is in seconds and defaults to '1'


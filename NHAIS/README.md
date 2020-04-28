# NHAIS

NHAIS is a system that allows General Practice (GP) Surgeries to keep their patient registration and demographics data in sync with the regional Health Authorities (HA). Since the creation of this service the regional or area health authorities (approx 80) have since been replaced by a fewer number of successor organisations. There is however still a notion of every GP Practice’s patient being registered with one of the HAs.


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

A Docker image for each service has been created and can be found within Docker Hub along with the relevant install guidelines.

### Outbound

### Inbound

### MESH Wrapper

## Integration Testing
MM to add

## Operating/Administration Considerations

Click here for suggestions on how you might operate this Adaptor in your own Infrastructure.  This covers areas such as Log consumption, Tooling, Audit etc 

## Troubleshooting

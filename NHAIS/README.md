# NHAIS

NHAIS is a system that allows General Practice (GP) Surgeries to keep their patient registration and demographics data in sync with the regional Health Authorities (HA). Since the creation of this service the regional or area health authorities (approx 80) have since been replaced by a fewer number of successor organisations. There is however still a notion of every GP Practice’s patient being registered with one of the HAs.

The patient registration and demographics portion is called HA/GP Links. Whilst the NHAIS NHS Service supports features in addition to GP Links, this adapter currently only provides functionality specific to GP Links.

## Architecture overview

The following illustration shows the NHAIS adaptor in the wider systems context:
![NHAIS System Context](../img/NHAIS%20Arc%20Overview.png)

Some of the services that make up the adaptor can be configured according to the GP Suppliers preferred host and implementation patterns.  These services are illustrated above in the grey boxes.

### Useful NHAIS and GP Links specifications

The following table provides links to various specifications:

Title | Description | Link
------------ | ------------- | -------------
National Health Application and Infrastructure Services (NHAIS) | NHAIS developer document library | https://digital.nhs.uk/services/nhais
Guide to NHAIS/GP links documentation | Describes how to use the “NHAIS developer document library” and provides updates and clarifications to the original documentation | https://digital.nhs.uk/services/nhais/guide-to-nhais-gp-links-documentation
NHAIS developer document library | Hosts the documents comprising the “HA/GP links registration GP systems specification” | https://digital.nhs.uk/services/nhais/nhais-developer-document-library

## GP Links - supported transaction types

HA/GP Links messaging is comprised of several types "transactions" used to update and reconcile patient lists and 
patient demographic data. The following transaction types are supported by the NHAIS Adaptor:

GP Links to HA

| Abbreviation | Description 
|--------------|-------------
| ACG          | Acceptance transaction  
| AMG          | Amendment transaction  
| REG          | Removal (Out of Area) transaction  
| DER          | Deduction Request transaction  

HA to GP Links 

| Abbreviation | Description 
|--------------|-------------
| AMF          | Amendment transaction  
| DEF          | Deduction transaction  
| APF          | Approval transaction  
| REF          | Rejection (Wrong HA) transaction  
| FPN          | FP69 Prior Notification transaction – Section 3.21  
| FFR          | FP69 Flag Removal transaction  
| DRR          | Deduction Request Rejection transaction  
| *            | Close Quarter Notification (chapter 3.20, Chapter 3 page 154) (may be considered optional)

\* Close Quarter Notification is acknowledged by the adaptor but not forwarded to the GP System

## Workflows

### Acceptance - Approved

![NHAIS System Context](../img/High-level%20Acceptance%20Workflow,%20Approved.png)

### Acceptance - Error

![NHAIS System Context](../img/High-level%20Acceptance%20Workflow,%20Error.png)

## Adaptor status and version

The current status for the NHAIS adaptor is [**Alpha:**](https://digital.nhs.uk/developer/guides-and-documentation/reference-guide)

The latest version of the adaptor is: **v0.0.1**

## Onboarding
The purpose of each of the National Integration Adaptors is to enable access to national NHS Systems.  As such, the NHAIS adaptor will need to be configured to integrate with the relevant NHS environment(s).  Therefore you will need to register your intention to use adaptors through the standard [NHS onboarding process.](https://digital.nhs.uk/developer/guides-and-documentation/onboarding-process)

## Open test and Path to live - Access
In order to perform end-to-end testing of the MHS Adaptor, you will require access to an NHS Digital test environment. The MHS adaptor connects to the following two test endpoints which are available in an NHS Digital test environment:
- Spine Core Mocked endpoint - which you will use to send and receive messages
- SDS mocked directory - which is used to lookup routing and reliability information

NHS Digital provides several environments to test these adaptors against:
- OpenTest is an environment which can be used to perform initial test activities such as proof of concepts where an Health & Social Care Network (HSCN) connection is not available.
- All other integration test activities are to be performed within a Path To Live environment. These activities include Development, Integration, Deployment and Non-functional tests.

To set up and configure OpenTest up please use [Set up NHS Digital OpenTest connection.](https://digital.nhs.uk/services/path-to-live-environments/opentest-environment)
To set up and configure Path to Live connectivity, please see [Path to Live environments.](https://digital.nhs.uk/services/path-to-live-environments)

## NHAIS Services and how to deploy them

### Client side integration - deployment patterns
The installation guides within this section are based on NHSD’s recommended implementation patterns.  These patterns are detailed in two Exemplar Architectures available for AWS and Azure. 

### Docker Images
A single Docker image for all NHAIS services has been created and can be found within Docker Hub along with the relevant install guidelines.  The published docker image includes the following NHAIS adaptor services:

**Outbound**
The GP System will send outbound messages using a HL7 FHIR R4 REST API.  An [Open API specification]((https://github.com/nhsconnect/integration-adaptor-nhais/tree/develop/specification)) has been created for the Outbound service. 

**Inbound**
The GP System will receive inbound messages from an AMQP message queue. The messages will be HL7 FHIR R4.

**MESH Wrapper**

## Integration Testing
MM to add

## Operating/Administration Considerations

### Local Install
The integration-adaptor-nhais Github repository contains additional information including how to run a [local install](https://github.com/nhsconnect/integration-adaptor-nhais#Development).

The [NHAIS github repository](https://github.com/nhsconnect/integration-adaptor-nhais/tree/develop/pipeline) also contains addtional information on how you might operate this Adaptor in your own Infrastructure.  This covers areas such as Log consumption, Tooling, Audit etc 

## Troubleshooting
This section contains details of common questions

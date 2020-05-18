# NHAIS

NHAIS is a system that allows General Practice (GP) Surgeries to keep their patient registration and demographics data in sync with the regional Health Authorities (HA). Since the creation of this service the regional or area health authorities (approx 80) have since been replaced by a fewer number of successor organisations. There is however still a notion of every GP Practice’s patient being registered with one of the HAs.

The patient registration and demographics portion is called HA/GP Links. Whilst the NHAIS NHS Service supports features in addition to GP Links, this adapter currently only provides functionality specific to GP Links.


### Useful NHAIS and GP Links Specifications

The following table provides links to various specifications:

Title | Description | Link
------------ | ------------- | -------------
National Health Application and Infrastructure Services (NHAIS) | NHAIS developer document library | https://digital.nhs.uk/services/nhais
Guide to NHAIS/GP links documentation | Describes how to use the “NHAIS developer document library” and provides updates and clarifications to the original documentation | https://digital.nhs.uk/services/nhais/guide-to-nhais-gp-links-documentation
NHAIS developer document library | Hosts the documents comprising the “HA/GP links registration GP systems specification” | https://digital.nhs.uk/services/nhais/nhais-developer-document-library

## GP Links - Supported Transaction Types

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

## NHAIS Services and how to Deploy them

The installation guides within this section are based on NHSD’s recommended implementation patterns.  These patterns are detailed in two Exemplar Architectures available for AWS and Azure. 

A Docker image for each service has been created and can be found within Docker Hub along with the relevant install guidelines.

### Outbound
The GP System will send outbound messages using a HL7 FHIR R4 REST API:

### Inbound
The GP System will receive inbound messages from an AMQP message queue. The messages will be HL7 FHIR R4.

### MESH Wrapper

## Integration Testing
MM to add

## Operating/Administration Considerations

Click here for suggestions on how you might operate this Adaptor in your own Infrastructure.  This covers areas such as Log consumption, Tooling, Audit etc 

## Troubleshooting

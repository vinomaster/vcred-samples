# Verifiable Credential Samples
This repo is intended as a sandbox for iterating on best practice JSON-LD models for self-sovereign identity credentials associated with industry standard card data formats.

## Goals
Today the common physical rendering format for an identity instrument is a paper/plastic card. For compliance purposes each industry defines standards that issuing institutions must comply with when issuing identity instruments. This repo attempts to define several exemplars of [Verifiable Credential](https://w3c.github.io/vc-data-model/) schemas that can be used for compliance activity when issuers consider the issuance of digital credentials. 

Objectives are:

1. Iteratively refine sample schemas using JSON-LD best practices
2. Register sample schemas as Credential Schemas with the [Sovrin Network](http://sovrin.org).

## Standards
This repo will explore several industry standards to help drive the requirements for several verifiable credential schema candidates:

* [Auto Insurance ID Card](https://www.acord.org/) - ACORD 360
* [ISO-Compliant Driving License](https://www.iso.org/standard/41920.html) - ISO 18013 Part 1
* [ISO Electronic registration identification for Vehicles](https://www.iso.org/standard/51849.html) - ISO 24534
* [WEDI Health Identification Card Implementation Guide](https://www.wedi.org/knowledge-center/resource-view/resources/2015/06/19/wedi-health-identification-card-implementation-guide-version-1.1-with-errataWedi)

## Organization
This repo is organized using the subsequent file structure:

* `/vocabs`: JSON-LD allows for inline and remote [@context](https://json-ld.org/spec/latest/json-ld/#the-context) *vocabulary* descriptions that enable end-points in a conversation to use shortcut terms to communicate with one another more efficiently. These shortcut terms are specific to the situational context of the conversation. For the work herein, we generalize the conversation to the concept of a **Card Data Element**.  
* `/schemas`: The *Verifiable Credentials Specification* uses schemas to describe different types of digital identity instruments (credentials). For example, Membership Card, Healthcare Card, Passport, Driver License, etc. Ideally, schemas should refer to remotely hosted vocabularies.
* `/samples`: An *Issuer* uses a schema to create specific instances of a credential. For example, John Doe's Fishing Permit for the State of Minnesota.

## ToDo

1. Review generic vocab/schema model
2. Add others standards
3. Formalize hosting of vocabs
4. Register schemas
  

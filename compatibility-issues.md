# Compatibility Issues

## Overview
As we build technology implementations that make use of [Verifiable Credential](https://w3c.github.io/vc-data-model/) and [Hyperledger Indy](https://www.hyperledger.org/projects/hyperledger-indy) ("Indy"), we must address several implementation design and interoperability issues.

## Solution Design Principles  

1. *Selective Disclosure*: An individual (*Holder*) should have the ability to respond to a identity proof request by selecting which identity traits from their corpus of identity instruments (digital credentials) will be used in the proof response.
2. *Standards Independence*: Standards organizations, particularly deeply rooted existing organizations should not be required to embrace new schema vocabularies in order to support **Verifiable Credentials**. In other words, organizations like [ACORD]((https://www.acord.org/), [ISO](https://www.iso.org/) and [WEDI](https://www.wedi.org/) should be able to provide JSON-LD versions of their schemas and these schemas should be compatible with Indy.
3. *Rendering Model Dependence*: The UI Data Model needs to be tightly coupled with the underlying schema. Specifically the mapping of meta-data for how a data element is displayed SHOULD be easily accessible by both the Edge Agent and the Verifier applicatuion.

## Issues

### Selective Disclosure
An Edge Agent, such as a *Mobile Credentials App*, needs to have the ability present pertinent identity traits to the user so that the user can select which trait they will use in a response.

* Proof Request Processing: The Edge Agent must be able to ascertain from the *proof request* the type of identity traits required for the identity challenge. For example, if the proof request requires the trait of ```surname``` the Edge Agent should be able to know that any credential held in the *Holders* digital wallet that contains identity traits such as ```surname```, ```lastname```,```clan-name``` and ```family-name``` should be presented as options. Furthermore, there are existing schema standards that allow the issuer to provide an alternative ("alias") label for such trait names.

For example, if two Issuers using disparate industry schemas issuer credentials that contain traits pertaining to *Family Name*, the Edge Agent MUST be able to find these traits in the corpus of traits in the *Holder's* digital wallet and present them all to the user for selection. *HINT: Common element name, even when an alias is used*.

```
{
  "elementName": "Family Name",
  "elementValue": "Smith",
  "elementCategory": "iso18013-1-01",
  "elementCategoryVersion": "2005-00",
  "elementAlias": "Clan-Name"
}
```

```
{
  "elementName": "Family Name",
  "elementValue": "Smith",
  "elementCategory": "wedi-1-01",
  "elementCategoryVersion": "2010-03",
  "elementAlias": "Lastname"
}
```

* Proof Response Processing: A Verifier must be able to determine the applicability of all identity traits used in a proof response based on the requirements of a proof request. Some proof requests may be *flexible* and require only similar ```elementName``` traits. Other requests may be more restrictive and require the same ```elementName```, same underlying schema data model: ```elementCategory``` and ```elementCategoryVersion```.

### Standards Independence

1. An Issuer needs to be able to convey that the credential being issued is compliant with a regulatory standard. Regardless of what *alias* an Issuer uses for a specific identity trait, a claim about the identity trait should cary with it some meta data that correlates the claim to a specific element in the regulatory standard. For example, if two different US State Governments published driver license schema variations based on the ISO18013 Standard, traits from credentials instances derived from those different schemas should be viewed as instances of the same data element. This is important for verifiers across jurisdictions that must be able to request claims made by Issuers based on a specific category of varying schemas rooted in an underlying data model. *HINT: Common element category*.

```
{
  "elementName": "Family Name",
  "elementValue": "Smith",
  "elementCategory": "iso18013-1-01",
  "elementCategoryVersion": "2005-00",
  "elementAlias": "Clan-Name"
}
```

```
{
  "elementName": "Family Name",
  "elementValue": "Jones",
  "elementCategory": "iso18013-1-01",
  "elementCategoryVersion": "2005-00",
  "elementAlias": "Surname"
}
```

2. An Issuer SHOULD be able to use JSON-LD to describe meta-data about an identity trait in their schema without impacting compatibility with Indy processing. *This is currently not possible today*.

### Rendering Model Dependence
Applications for stakeholders at all ends of a SSI/VC flow, namely Issuer, Holder and Verifier, need to be able to correlate the display labels for an identity trait with the underlying schema relationship between element Name, Category and Standard Version. 

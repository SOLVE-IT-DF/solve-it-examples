# A series of examples making use of the SOLVE-IT knowledge base

## Introduction
The SOLVE-IT knowledge base was introduced at [DFRWS EU 2025](https://dfrws.org/presentation/solve-it-a-proposed-digital-forensic-knowledge-base-inspired-by-mitre-attck/). The associated academic paper in [FSI:Digital Investigation](https://www.sciencedirect.com/science/article/pii/S2666281725000034) can be cited as:

```Hargreaves, C., van Beek, H., Casey, E., SOLVE-IT: A proposed digital forensic knowledge base inspired by MITRE ATT&CK, Forensic Science International: Digital Investigation, Volume 52, Supplement, 2025, 301864, ISSN 2666-2817, https://doi.org/10.1016/j.fsidi.2025.301864```

The main code repo is [here](https://github.com/SOLVE-IT-DF/solve-it), but this repository contains a series of examples showing how SOLVE-IT can be used in practice. There is also another [dedicated repository](https://github.com/SOLVE-IT-DF/solve-it-applications-ai-review) showing how SOLVE-IT can be used to understand the applicability of AI to digital forensic techniques. 

## Forensic workflow example: forensic imaging
Forensic imaging is often defined as a single process. However, when mapped against SOLVE-IT techniques it reveals a series of techniques are used. This example shows how to compile the techniques used for a process and examine the weaknesses and the extent to which they are mitigated within an implementation of the workflow. 
See full example [here](forensic_workflow_example_forensic_imaging).

## Dependencies in digital forensic tools
This (in progress) example will illustrate how techniques can have dependencies and how that means that some weaknesses in one technique can cause weaknesses in others. 

## Subtleties in mitigation approaches: a file system example
This (in progress) example illustrates how mitigations that are sometimes used interchangeably are not, and how they need to be selected and used carefully in specific circumstances. 

## Mapping of techniques: a drone forensics example
This (in progress) example illustrates how a domain within digital forensics can be taken, and the knowledge based used to isolate the techniques used within that area. 

## Use of other organizational schemas
This example shows how the techniques can be reorganized by whatever schema or process model you want. 
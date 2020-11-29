# Generation of shipping documents from common schema

This project is for generating document schemas from a common class data model in accordance to [edi3.org](https://edi3.org) method and tooling.

## Benefits

The benefits of this model-driven approach is:

* **Consistency** of structure and naming across document schemas. The same attribute or relationship is called the same, positioned under the same class and has the same type between all generated schemas (unless deviations are explicitly defined).
* **Efficiency** of generating new schemas, literally by dragging in the classes needed for a particular new schemas' requirements.
* **Manageability** of updates and changes, if a change is made on one schema, it is automatically reflected in all other schemas based on the same data elements (subject of course to human approval, exporting the updated schema).
* **Semantic** alignment to [CEFACT](https://service.unece.org/trade/uncefact/publication/Transport%20and%20Logistics/MMT%20RDM/HTML/041.htm).

## Getting Started

You need a few tools to get started:

First, download and install [StarUML](http://staruml.io/).

Second, install the OpenAPI extension. In StarUML, go to Tools -> Extension Manager and select "Install from Url..." and install from this url: [https://github.com/gs-gs/staruml-cefact](https://github.com/gs-gs/staruml-cefact).

Now, from Tools -> OpenAPI -> Generate Specs you can export various API and web formats based on a UML model in accordance to the edi3 [spec](https://edi3.org/specs/edi3-uml-profile/develop/).

Please note that the OpenAPI extension is still under development and updates occurs. Please keep involved and submit relevant feedback on [https://github.com/gs-gs/staruml-cefact/issues](https://github.com/gs-gs/staruml-cefact/issues).

## Model Structure

The `tl-docgen-model.mdj` file defines both the common class model and the individual "profiles" for each document schema. You will find the model structured accordingly around a common "Model" package and a range of schema-specific packages (Bill Of Lading, Shipping Instructions, etc). All classes, enums, attributes, etc must be defined within the common Model. The schema packages only define thw following:

* A _Class_ representing the document schema.  
* An _interface_ which tells the OpenAPI extension which class to export. It must have an Interface Realization relationship to its corresponding schema class.
* A _Diagram_ which defines which elements from Model is to be included in the schema.

## Schema Exporting

While the OpenAPI extension supports different ways of exporting, the `tl-docgen-model.mdj` model is entirely based on **diagram exports**.

Exported schemas must be placed alongside the model under `/docs`.

Note that "JSON" and "JSON Schema" exporting options are not the same. JSON is a swagger specification (with API endpoints, etc), just like the YML but in JSON syntax. JSON Schema is - well - a JSON Schema (with a `"model"` element defining the root element, etc). Thus, two versions of each document must be made:

1. A "JSON Schema" export.
2. A "YML" export.

## CEFACT Shout Out

This project completely depends on the good work of the CEFACT ISCO a.k.a. edi3 working group - thanks!!

Note that (so far) I've only done the latter part of the edi3 method. The `tl-docgen-model.mdj` model is hand-built, not (yet) based on a generated model in accordance to the [model interchange spec](https://edi3.org/specs/edi3-model-interchange/develop/). I've spent hours and hours steering at CEFACT, though, so please use my interpretations as requirements input the that project. :)

I encourage everyone relevant to join the [community](https://edi3.org/community/) and get engaged!

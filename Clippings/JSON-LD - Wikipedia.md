---
categories:
  - "[[Clippings]]"
title: "JSON-LD - Wikipedia"
source: "https://en.wikipedia.org/wiki/JSON-LD"
author:
  - "[[Wikipedia]]"
created: 2025-09-08
description:
tags:
  - "clippings"
  - "wikipedia"
---
<table><tbody><tr><th colspan="2" style="padding-bottom: 0.15em;background-color:#e0e0e0;">JSON-LD</th></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;"><a href="https://en.wikipedia.org/wiki/Filename_extension">Filename extension</a></th><td style="line-height: 1.35;"><style>.mw-parser-output .monospaced{font-family:monospace,monospace}</style><div>.jsonld</div></td></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;"><a href="https://en.wikipedia.org/wiki/Media_type">Internet media&nbsp;type</a></th><td style="line-height: 1.35;"><link href="mw-data:TemplateStyles:r886049734"><div>application/ld+json</div></td></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;">Type of format</th><td style="line-height: 1.35;"><a href="https://en.wikipedia.org/wiki/Semantic_Web">Semantic Web</a></td></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;"><a href="https://en.wikipedia.org/wiki/Container_format">Container&nbsp;for</a></th><td style="line-height: 1.35;"><a href="https://en.wikipedia.org/wiki/Linked_Data">Linked Data</a></td></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;">Extended&nbsp;from</th><td style="line-height: 1.35;"><a href="https://en.wikipedia.org/wiki/JSON">JSON</a></td></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;"><a href="https://en.wikipedia.org/wiki/International_standard">Standard</a></th><td style="line-height: 1.35;"><a href="http://www.w3.org/TR/json-ld/">JSON-LD 1.1</a> / <a href="http://www.w3.org/TR/json-ld-api/">JSON-LD 1.1 API</a></td></tr><tr><th scope="row" style="line-height: 1.2; padding-right: 0.65em;"><span><a href="https://en.wikipedia.org/wiki/Open_file_format">Open format</a>?</span></th><td style="line-height: 1.35;">Yes</td></tr></tbody></table>

| Abbreviation | JSON-LD |
| --- | --- |
| Status | W3C Recommendation |
| Year started | 2010 |
| Editors | Editors  - - Gregg Kellogg - Pierre-Antoine Champin - Dave Longley  Previous editors  - - Manu Sporny - Markus Lanthaler |
| Authors | Manu Sporny, Dave Longley, Gregg Kellogg, Markus Lanthaler, Niklas Lindström |
| Base standards | - [BCP 47](https://en.wikipedia.org/wiki/IETF_language_tag "IETF language tag") - [JSON](https://en.wikipedia.org/wiki/JSON "JSON") - [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework "Resource Description Framework") - [URI scheme](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier "Uniform Resource Identifier") - [Internationalized Resource Identifier](https://en.wikipedia.org/wiki/Internationalized_Resource_Identifier "Internationalized Resource Identifier") - [Unicode Bidirectional Algorithm](https://en.wikipedia.org/wiki/Bidirectional_text#Unicode_bidi_support "Bidirectional text") |
| Domain | [Semantic Web](https://en.wikipedia.org/wiki/Semantic_Web "Semantic Web"), [Data Serialization](https://en.wikipedia.org/wiki/Serialization "Serialization") |
| Website | - [json-ld.org](https://json-ld.org/) - [JSON-LD 1.1](https://www.w3.org/TR/json-ld/) - [JSON-LD 1.1 Processing Algorithms and API](https://www.w3.org/TR/json-ld-api/) - [JSON-LD 1.1 Framing](https://www.w3.org/TR/json-ld11-framing/) |

**JSON-LD** (**JavaScript Object Notation for Linked Data**) is a method of encoding [linked data](https://en.wikipedia.org/wiki/Linked_data "Linked data") using [JSON](https://en.wikipedia.org/wiki/JSON "JSON") and of serializing data similarly to traditional JSON.[^1] It is meant to be simple to create by modifying JSON documents.[^2] JSON-LD is a [World Wide Web Consortium Recommendation](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium#W3C_recommendation_\(REC\) "World Wide Web Consortium") initially developed by the JSON for Linking Data Community Group,[^3] transferred to the RDF Working Group[^4] for review, improvement and standardization,[^5] and now maintained by the JSON-LD Working Group.[^6]

## Design

JSON-LD is based on the concept of a "context" that maps JSON object properties to concepts in an [ontology](https://en.wikipedia.org/wiki/Ontology_\(information_science\) "Ontology (information science)") using an [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework "Resource Description Framework") model. In order to map the JSON-LD syntax to RDF, JSON-LD allows values to be coerced to a specified type or tagged with a language. A context can be embedded directly in a JSON-LD document or put into a separate file and referenced from traditional JSON documents via an [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol "Hypertext Transfer Protocol") Link [header](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields "List of HTTP header fields").

## Example

```
{
  "@context": {
    "name": "http://xmlns.com/foaf/0.1/name",
    "homepage": {
      "@id": "http://xmlns.com/foaf/0.1/workplaceHomepage",
      "@type": "@id"
    },
    "Person": "http://xmlns.com/foaf/0.1/Person"
  },
  "@id": "https://me.example.com",
  "@type": "Person",
  "name": "John Smith",
  "homepage": "https://www.example.com/"
}
```

The example above describes a person, based on the [FOAF (friend of a friend) ontology](https://en.wikipedia.org/wiki/FOAF_\(ontology\) "FOAF (ontology)"). First, the two JSON properties `name` and `homepage` and the type `Person` are mapped to concepts in the FOAF vocabulary and the value of the `homepage` property is specified to be of the type `@id`. In other words, the homepage id is specified to be an [IRI](https://en.wikipedia.org/wiki/Internationalized_Resource_Identifier "Internationalized Resource Identifier") in the context definition. Based on the RDF model, this allows the person described in the document to be unambiguously identified by an [IRI](https://en.wikipedia.org/wiki/Internationalized_Resource_Identifier "Internationalized Resource Identifier"). The use of resolvable IRIs allows RDF documents containing more information to be [transcluded](https://en.wikipedia.org/wiki/Transclusion "Transclusion") which enables clients to discover new data by following those links; this principle is known as 'Follow Your Nose'.[^7]

By having all data semantically annotated as in the example, an RDF processor can identify that the document contains information about a person (`@type`) and if the processor understands the FOAF vocabulary it can determine which properties specify the person's name and homepage.

## Use

The encoding is used by [Schema.org](https://en.wikipedia.org/wiki/Schema.org "Schema.org"),[^8] [Google Knowledge Graph](https://en.wikipedia.org/wiki/Google_Knowledge_Graph "Google Knowledge Graph"),[^9][^10] and used mostly for [search engine optimization](https://en.wikipedia.org/wiki/Search_engine_optimization "Search engine optimization") activities. It has also been used for applications such as [biomedical informatics](https://en.wikipedia.org/wiki/Health_informatics "Health informatics"),[^11] and representing [provenance](https://en.wikipedia.org/wiki/Provenance "Provenance") information.[^12] It is also the basis of [Activity Streams](https://en.wikipedia.org/wiki/Activity_Streams_\(format\) "Activity Streams (format)"), a format for "the exchange of information about potential and completed activities",[^13] and is used in [ActivityPub](https://en.wikipedia.org/wiki/ActivityPub "ActivityPub"), the federated social networking protocol.[^14] Additionally, it is used in the context of [Internet of Things (IoT)](https://en.wikipedia.org/wiki/Internet_of_things "Internet of things"), where a Thing Description,[^15] which is a JSON-LD document, describes the network facing interfaces of IoT devices.

## See also

- [Hypertext Application Language](https://en.wikipedia.org/wiki/Hypertext_Application_Language "Hypertext Application Language")

## References

[^1]: ["On Using JSON-LD to Create Evolvable RESTful Services"](http://m.lanthi.com/jsonld4rest-paper)., M. Lanthaler and C. Gütl in Proceedings of the 3rd International Workshop on RESTful Design (WS-REST 2012) at WWW2012.

[^2]: ["JSON-LD Syntax 1.1"](http://json-ld.org/spec/latest/json-ld-syntax/). 2010-07-16. Retrieved 2020-12-10.

[^3]: ["JSON for Linking Data Community Group"](https://json-ld.org/). json-ld.org.

[^4]: ["RDF Working Group"](http://www.w3.org/2011/rdf-wg/wiki/Main_Page). w3.org.

[^5]: ["JSON-LD 1.0, A JSON-based Serialization for Linked Data, W3C Recommendation 16 January 2014"](https://www.w3.org/TR/2014/REC-json-ld-20140116/). 2014-01-16. Retrieved 2020-12-10.

[^6]: ["JSON-LD Working Group"](https://www.w3.org/2018/json-ld-wg/). w3.org.

[^7]: ["Linked Data Patterns, Chapter 5: Follow Your Nose"](http://patterns.dataincubator.org/book/follow-your-nose.html). 2023-06-07. Retrieved 2023-06-07.

[^8]: ["Data Model"](https://schema.org/docs/datamodel.html). *Schema.org*. Retrieved 2018-06-20.

[^9]: ["Understanding structured data"](https://blog.bendevoficial.com/posts/understanding-structured-data). [Bendev Junior](https://en.wikipedia.org/w/index.php?title=Bendev_Junior&action=edit&redlink=1 "Bendev Junior (page does not exist)"). 14 June 2022.

[^10]: ["Method Entities in Search"](https://developers.google.com/knowledge-graph/reference/rest/v1/). *Google Developers*. Retrieved 2017-10-17.

[^11]: Xin, Jiwen; Afrasiabi, Cyrus; Lelong, Sebastien; Adesara, Julee; Tsueng, Ginger; Su, Andrew I.; Wu, Chunlei (2018-02-01). ["Cross-linking BioThings APIs through JSON-LD to facilitate knowledge exploration"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5796402). *BMC Bioinformatics*. **19** (1): 30. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1186/s12859-018-2041-5](https://doi.org/10.1186%2Fs12859-018-2041-5). [PMC](https://en.wikipedia.org/wiki/PMC_\(identifier\) "PMC (identifier)") [5796402](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5796402). [PMID](https://en.wikipedia.org/wiki/PMID_\(identifier\) "PMID (identifier)") [29390967](https://pubmed.ncbi.nlm.nih.gov/29390967).

[^12]: Huynh, Trung Dong; Michaelides, Danius T.; Moreau, Luc (2016). ["PROV-JSONLD: A JSON and linked data representation for provenance"](https://eprints.soton.ac.uk/395985/1/prov-jsonld-poster-abs.pdf) (PDF). In Mattoso, Marta; Glavic, Boris (eds.). *Provenance and annotation of data and processes: 6th International Provenance and Annotation Workshop, IPAW 2016, McLean, VA, USA, June 7-8, 2016, Proceedings*. Lecture Notes in Computer Science. Vol. 9672. Cham: Springer International Publishing. pp. 173–177\. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1007/978-3-319-40593-3\_15](https://doi.org/10.1007%2F978-3-319-40593-3_15). [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-3-319-40592-6](https://en.wikipedia.org/wiki/Special:BookSources/978-3-319-40592-6 "Special:BookSources/978-3-319-40592-6"). [S2CID](https://en.wikipedia.org/wiki/S2CID_\(identifier\) "S2CID (identifier)") [44036472](https://api.semanticscholar.org/CorpusID:44036472).

[^13]: Prodromou, Evan (May 2017). ["Activity Streams 2.0"](https://www.w3.org/TR/2017/REC-activitystreams-core-20170523/). *W3C Recommendation* – via W3C.

[^14]: Tallon, Jessica (Jan 2018). ["ActivityPub"](https://www.w3.org/TR/2018/REC-activitypub-20180123/). *W3C Recommendation* – via W3C.

[^15]: ["Web of Things (WoT) Thing Description, W3C Proposed Recommendation"](https://www.w3.org/TR/wot-thing-description). *www.w3.org*. Retrieved 2020-03-26.

## External links

- [JSON-LD.org](http://json-ld.org/)

![](https://en.wikipedia.org/wiki/Special:CentralAutoLogin/start?type=1x1&usesul3=1)
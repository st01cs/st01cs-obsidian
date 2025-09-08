---
categories:
  - "[[Clippings]]"
title: "RDFa - Wikipedia"
source: "https://en.wikipedia.org/wiki/RDFa"
author:
  - "[[Wikipedia]]"
created: 2025-09-08
description:
tags:
  - "clippings"
  - "wikipedia"
---
| Abbreviation | RDFa |
| --- | --- |
| Status | Published |
| Year started | 2004 |
| Editors | Ben Adida, Mark Birbeck |
| Base standards | [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework "Resource Description Framework") |
| Related standards | [RDF Schema](https://en.wikipedia.org/wiki/RDF_Schema "RDF Schema"), [OWL](https://en.wikipedia.org/wiki/Web_Ontology_Language "Web Ontology Language") |
| Domain | [Semantic Web](https://en.wikipedia.org/wiki/Semantic_Web "Semantic Web") |
| Website | [www.w3.org/TR/rdfa-primer/](http://www.w3.org/TR/rdfa-primer/) |

**RDFa** or **Resource Description Framework in Attributes**[^rdfa-primer-1] is a [W3C](https://en.wikipedia.org/wiki/W3C "W3C") Recommendation that adds a set of [attribute-level](https://en.wikipedia.org/wiki/HTML_attribute "HTML attribute") extensions to [HTML](https://en.wikipedia.org/wiki/HTML5 "HTML5"), [XHTML](https://en.wikipedia.org/wiki/XHTML "XHTML") and various XML-based document types for embedding rich [metadata](https://en.wikipedia.org/wiki/Metadata "Metadata") within web documents. The [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework "Resource Description Framework") (RDF) data-model mapping enables the use of RDFs for embedding RDF [subject-predicate-object expressions](https://en.wikipedia.org/wiki/Resource_Description_Framework#Overview "Resource Description Framework") within XHTML documents. RDFa also enables the extraction of RDF model triples by compliant [user agents](https://en.wikipedia.org/wiki/User_agent "User agent").

The RDFa community runs a [wiki](https://en.wikipedia.org/wiki/Wiki "Wiki") website to host tools, examples, and tutorials.[^rdfa_wiki-2]

## History

RDFa was first proposed by [Mark Birbeck](https://en.wikipedia.org/w/index.php?title=Mark_Birbeck&action=edit&redlink=1 "Mark Birbeck (page does not exist)") in the form of a [W3C](https://en.wikipedia.org/wiki/W3C "W3C") note entitled *XHTML and RDF*,[^xhtml_and_rdf_note1-3] which was then presented to the Semantic Web Interest Group[^4] at the W3C's 2004 Technical Plenary.[^xhtml_and_rdf_note2-5] Later that year the work became part of the sixth public Working Draft of XHTML 2.0.[^xhtml_2_wd_6-6][^timelinehistory-7] Although it is generally assumed that RDFa was originally intended only for XHTML 2, in fact the purpose of RDFa was always to provide a way to add metadata to *any* XML-based language. Indeed, one of the earliest documents bearing the *RDF/A Syntax* name has the sub-title *A collection of attributes for layering RDF on XML languages*.[^rdfa_1-8] The document was written by Mark Birbeck and [Steven Pemberton](https://en.wikipedia.org/wiki/Steven_Pemberton "Steven Pemberton"), and was made available for discussion on October 11, 2004.

In April 2007 the XHTML 2 Working Group produced a module to support RDF annotation within the XHTML 1 family.[^rdfa_modules_ed-9] As an example, it included an extended version of XHTML 1.1 dubbed [XHTML+RDFa 1.0](https://en.wikipedia.org/wiki/XHTML%2BRDFa "XHTML+RDFa"). Although described as not representing an intended direction in terms of a formal markup language from the W3C, limited use of the XHTML+RDFa 1.0 [DTD](https://en.wikipedia.org/wiki/Document_Type_Definition "Document Type Definition") did subsequently appear on the public Web.[^xhtml_rdfa_1_examples-10]

October 2007 saw the first public Working Draft of a document entitled *RDFa in XHTML: Syntax and Processing*.[^rdfa_syntax_wd1-11] This superseded and expanded upon the April draft; it contained rules for creating an RDFa parser, as well as guidelines for organizations wishing to make practical use of the technology.

In October 2008 RDFa 1.0 reached recommendation status.[^rdfa_syntax_cr1-12]

RDFa 1.1 reached recommendation status in June 2012.[^rdfa1_1_core_rec-13] It differs from RDFa 1.0 in that it no longer relies on the XML-specific namespace mechanism. Therefore, it is possible to use RDFa 1.1 with non-XML document types such as HTML 4 or HTML 5. Details can be found in an appendix to HTML 5.[^html_plus_rdfa1_1-14]

An additional *RDFa 1.1 Primer* document was last updated 17 March 2015.[^rdfa-primer-1] (The first public Working Draft dates back to 10 March 2006.[^xhtml-rdfa-primer0-15])

## Versions and variants

There are some main well-defined variants of the basic concepts, that are used as reference and as abbreviation to the W3C standards.

### HTML+RDFa

RDFa was defined in 2008 with the "RDFa in XHTML: Syntax and Processing" Recommendation.[^rdfa2008-16] Its first application was to be a [module of XHTML](https://en.wikipedia.org/wiki/XHTML_Modularization "XHTML Modularization").

The HTML applications remained, *"a collection of attributes and processing rules for extending XHTML to support RDF"* expanded to HTML5, are now expressed in a specialized standard, the "HTML+RDFa" (the last is *"HTML+RDFa 1.1 - Support for RDFa in HTML4 and HTML5"*[^html-rdfa-17]).

### RDFa 1.0

The *"HTML+RDFa"* syntax of 2008 was also termed *"RDFa 1.0"*, so, there is no "RDFa Core 1.0" standard. In general this 2008's *RDFa 1.0* is used with the old [XHTML](https://en.wikipedia.org/wiki/XHTML "XHTML") standards (as long as *RDFa 1.1* is used with XHTML5 and HTML5).

### RDFa 1.1

Is the first generic (for HTML and XML) RDFa standard; the "RDFa Core 1.1" is in the Third Edition, since 2015.[^rdfa-core-18]

### RDFa Lite

RDFa Lite is a W3C Recommendation (1.0 and 1.1) since 2009,[^rdfalite1.0-19] where it is described as follows:[^rdfalite1.1-20]

> RDFa Lite is minimal subset of RDFa ... consisting of a few attributes that may be used to express [machine-readable data](https://en.wikipedia.org/wiki/Machine-readable_data "Machine-readable data") in Web documents like HTML, SVG, and XML. While it is not a complete solution for advanced data markup tasks, it does work for most day-to-day needs and can be learned by most Web authors in a day.

RDFa Lite consists of five attributes: vocab, typeof, property, resource, and prefix.[^rdfalite1.1-20] RDFa 1.1 Lite is upwards compatible with RDFa 1.1.[^rdfalite1.1-20]

In 2009 the W3C was positioned[^21] to retain *RDFa Lite* as unique and definitive standard alternative to [Microdata](https://en.wikipedia.org/wiki/Microdata_\(HTML\) "Microdata (HTML)").[^22] The position was confirmed with the publication of the HTML5 Recommendation in 2014.

## Essence

The essence of RDFa is to provide a set of attributes that can be used to carry metadata in an XML language (hence the 'a' in RDFa).

These attributes are:

about

a [URI](https://en.wikipedia.org/wiki/URI "URI") or [CURIE](https://en.wikipedia.org/wiki/CURIE "CURIE") specifying the resource the metadata is about

rel and rev

specifying a relationship and reverse-relationship with another resource, respectively

src, [href](https://en.wikipedia.org/wiki/Href "Href") and resource

specifying the partner resource

property

specifying a property for the content of an element or the partner resource

content

optional attribute that overrides the content of the element when using the property attribute

datatype

optional attribute that specifies the [datatype](https://en.wikipedia.org/wiki/Datatype "Datatype") of text specified for use with the property attribute

typeof

optional attribute that specifies the RDF type(s) of the subject or the partner resource (the resource that the metadata is about).

## Benefits

There are five "principles of interoperable metadata" met by RDFa.[^23]

- Publisher Independence – each site can use its own standards
- Data Reuse – data are not duplicated. Separate XML and HTML sections are not required for the same content.
- Self Containment – the HTML and the RDF are separated
- Schema Modularity – the attributes are reusable

Additionally RDFa may benefit [web accessibility](https://en.wikipedia.org/wiki/Web_accessibility "Web accessibility") as more information is available to [assistive technology](https://en.wikipedia.org/wiki/Assistive_Technology_Service_Provider_Interface "Assistive Technology Service Provider Interface").[^24]

## Usage

There is a growing number of tools for better usage of RDFa vocabularies and RDFa annotation.

### HTML+RDFa statistics

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/RDFa-UsageStatistics-charts.png/330px-RDFa-UsageStatistics-charts.png)

2013 survey pizza charts of percentage usage,[^webstats2013-25] showing that 79% of URLs and 43% of domains use *HTML+RDFa*. The average 61% (the other 39% was Microformats) is the *usage indicator*.

Simplified approaches to semantically annotate information items in [webpages](https://en.wikipedia.org/wiki/Webpages "Webpages") were greatly encouraged by the [HTML+RDFa](https://en.wikipedia.org/wiki/#HTML+RDFa) (released in 2008) and [microformats](https://en.wikipedia.org/wiki/Microformats "Microformats") (since ~2005) standards.

As of 2013 these standards were encoding events, contact information, products, and so on. Despite the [vCard](https://en.wikipedia.org/wiki/VCard "VCard") semantics (only basic items of [person](https://en.wikipedia.org/wiki/Person "Person") and [organization](https://en.wikipedia.org/wiki/Organization "Organization") annotations) dominance,[^webstats2013-25] and some [cloning](https://en.wikipedia.org/wiki/Boilerplate_\(text\) "Boilerplate (text)") of annotations along the same [domain](https://en.wikipedia.org/wiki/Domain_name "Domain name"), the counting of webpages (URLs) and domains with annotations is an important statistical indicator for *usage of semantically annotated information* in the Web.

The statistics of 2017 show that usage[^webstats2017-26] of HTML+RDFa is now less than that of Microformats.

### RDFa editors

Web-based RDFa editors

There are already a few RDFa editors available online. [RDFaCE](https://en.wikipedia.org/w/index.php?title=RDFaCE&action=edit&redlink=1 "RDFaCE (page does not exist)") (RDFa Content Editor) is a [WYSIWYM](https://en.wikipedia.org/wiki/WYSIWYM "WYSIWYM") editor based on [TinyMCE](https://en.wikipedia.org/wiki/TinyMCE "TinyMCE") to support RDFa content authoring. It supports manual and semi-automatic generation of RDFa with the support of annotation services such as [DBpedia Spotlight](https://en.wikipedia.org/wiki/DBpedia_Spotlight "DBpedia Spotlight"), [OpenCalais](https://en.wikipedia.org/wiki/OpenCalais "OpenCalais"), [Alchemy API](https://en.wikipedia.org/wiki/Alchemy_API "Alchemy API"), among others.[^27] RDFaCE-Lite is a version of RDFaCE also supporting [Microdata](https://en.wikipedia.org/wiki/Microdata_\(HTML\) "Microdata (HTML)") and available as a WordPress plugin.[^28]

Desktop RDFa editors

[AutôMeta](https://en.wikipedia.org/w/index.php?title=Aut%C3%B4Meta&action=edit&redlink=1 "AutôMeta (page does not exist)") is an environment for semi-automatic (or automatic) annotation of documents for publishing on the Web using RDFa. It also includes an RDFa extraction tool to provide the user with a view of the annotated triples. It is available in both [CLI](https://en.wikipedia.org/wiki/Command-line_interface "Command-line interface") and [GUI](https://en.wikipedia.org/wiki/GUI "GUI") interfaces.[^29]

### Examples

The following is an example of adding [Dublin Core](https://en.wikipedia.org/wiki/Dublin_Core "Dublin Core") metadata to an XML element in an XHTML file. Dublin Core data elements are data typically added to a book or article (title, author, subject etc.)

```
<div xmlns:dc="http://purl.org/dc/elements/1.1/"
  about="http://www.example.com/books/wikinomics">
  <span property="dc:title">Wikinomics</span>
  <span property="dc:creator">Don Tapscott</span>
  <span property="dc:date">2006-10-01</span>
</div>
```

Moreover, RDFa allows the passages and words within a text to be associated with semantic markup:

```
<div xmlns:dc="http://purl.org/dc/elements/1.1/"
   about="http://www.example.com/books/wikinomics">
  In his latest book
  <span property="dc:title">Wikinomics</span>,
  <span property="dc:creator">Don Tapscott</span>
  explains deep changes in technology,
  demographics and business.
  The book is due to be published in
  <span property="dc:date" content="2006-10-01">October 2006</span>.
</div>
```

#### XHTML + RDFa 1.0

The following is an example of a complete XHTML+RDFa 1.0 document. It uses [Dublin Core](https://en.wikipedia.org/wiki/Dublin_Core "Dublin Core") and [FOAF](https://en.wikipedia.org/wiki/FOAF_\(software\) "FOAF (software)"), an ontology for describing people and their relationships with other people and things:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML+RDFa 1.0//EN"
    "http://www.w3.org/MarkUp/DTD/xhtml-rdfa-1.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
    xmlns:foaf="http://xmlns.com/foaf/0.1/"
    xmlns:dc="http://purl.org/dc/elements/1.1/"
    version="XHTML+RDFa 1.0" xml:lang="en">
  <head>
    <title>John's Home Page</title>
    <base href="http://example.org/john-d/" />
    <meta property="dc:creator" content="Jonathan Doe" />
    <link rel="foaf:primaryTopic" href="http://example.org/john-d/#me" />
  </head>
  <body about="http://example.org/john-d/#me">
    <h1>John's Home Page</h1>
    <p>My name is <span property="foaf:nick">John D</span> and I like
      <a href="http://www.neubauten.org/" rel="foaf:interest"
        xml:lang="de">Einstürzende Neubauten</a>.
    </p>
    <p>
      My <span rel="foaf:interest" resource="urn:ISBN:0752820907">favorite
      book is the inspiring <span about="urn:ISBN:0752820907"><cite
      property="dc:title">Weaving the Web</cite> by
      <span property="dc:creator">Tim Berners-Lee</span></span></span>.
    </p>
  </body>
</html>
```

In the example above, the document URI can be seen as representing an HTML document, but the document URI plus the "#me" string `http://example.org/john-d/#me` represents the actual person, as distinct from a document about them. The *foaf:primaryTopic* in the header tells us the URI of the person the document is about. The *foaf:nick* property (in the first `span` element) contains a nickname for this person, and the *dc:creator* property (in the `meta` element) tells us who created the document. The hyperlink to the Einstürzende Neubauten website contains `rel="foaf:interest"`, suggesting that John Doe is interested in this band. The URI of their website is a resource.

The *foaf:interest* inside the second `p` element is referring to a book by ISBN. The `resource` attribute defines a resource in a similar way to the `href` attribute, but without defining a hyperlink. Further into the paragraph, a `span` element containing an `about` attribute defines the book as another resource to specify metadata about. The book title and author are defined within the contents of this tag using the *dc:title* and *dc:creator* properties.

Here are the same triples when the above document is automatically converted to [RDF/XML](https://en.wikipedia.org/wiki/RDF/XML "RDF/XML"):

```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
    xmlns:foaf="http://xmlns.com/foaf/0.1/"
    xmlns:dc="http://purl.org/dc/elements/1.1/">
  <rdf:Description rdf:about="http://example.org/john-d/">
    <dc:creator xml:lang="en">Jonathan Doe</dc:creator>
    <foaf:primaryTopic>
      <rdf:Description rdf:about="http://example.org/john-d/#me">
        <foaf:nick xml:lang="en">John D</foaf:nick>
        <foaf:interest rdf:resource="http://www.neubauten.org/"/>
        <foaf:interest>
          <rdf:Description rdf:about="urn:ISBN:0752820907">
            <dc:creator xml:lang="en">Tim Berners-Lee</dc:creator>
            <dc:title xml:lang="en">Weaving the Web</dc:title>
          </rdf:Description>
        </foaf:interest>
      </rdf:Description>
    </foaf:primaryTopic>
  </rdf:Description>
</rdf:RDF>
```

#### HTML5 + RDFa 1.1

The above example can be expressed without [XML namespaces](https://en.wikipedia.org/wiki/XML_namespaces "XML namespaces") in [HTML5](https://en.wikipedia.org/wiki/HTML5 "HTML5"):

```
<html prefix="dc: http://purl.org/dc/elements/1.1/" lang="en">
  <head>
    <title>John's Home Page</title>
    <link rel="profile" href="http://www.w3.org/1999/xhtml/vocab" />
    <base href="http://example.org/john-d/" />
    <meta property="dc:creator" content="Jonathan Doe" />
    <link rel="foaf:primaryTopic" href="http://example.org/john-d/#me" />
  </head>
  <body about="http://example.org/john-d/#me">
    <h1>John's Home Page</h1>
    <p>My name is <span property="foaf:nick">John D</span> and I like
      <a href="http://www.neubauten.org/" rel="foaf:interest"
        lang="de">Einstürzende Neubauten</a>.
    </p>
    <p>
      My <span rel="foaf:interest" resource="urn:ISBN:0752820907">favorite
      book is the inspiring <span about="urn:ISBN:0752820907"><cite
      property="dc:title">Weaving the Web</cite> by
      <span property="dc:creator">Tim Berners-Lee</span></span></span>.
    </p>
  </body>
</html>
```

Note how the prefix foaf is still used without declaration. RDFa 1.1 automatically includes prefixes for popular vocabularies such as FOAF.[^rdfa_initial_context-30]

  
The minimal [^31] document is:

```
<html lang="en">
  <head>
    <title>Example Document</title>
  </head>
  <body vocab="http://schema.org/">
    <p typeof="Blog">
      Welcome to my <a property="url" href="http://example.org/">blog</a>.
    </p>
  </body>
</html>
```

That is, it is recommended that all of these attributes are used: `vocab`, `typeof`, `property`; not only one of them.

**RDFa Structured Data Example**

Person Schema in RDFa.[^32]

```
<div vocab="http://schema.org/" typeof="Person">
  <a property="image" href="http://manu.sporny.org/images/manu.png">
    <span property="name">Manu Sporny</span></a>, 
  <span property="jobTitle">Founder/CEO</span>
  <div>
    Phone: <span property="telephone">(540) 961-4469</span>
  </div>
  <div>
    E-mail: <a property="email" href="mailto:(your emailid)">msporny@digitalbazaar(.)com</a>
  </div>
  <div>
    Links: <a property="url" href="http://manu.sporny.org/">Manu's homepage</a>
  </div>
</div>
```

## See also

- [GRDDL](https://en.wikipedia.org/wiki/GRDDL "GRDDL"), a way to extract (annotated) data out of XHTML and [XML](https://en.wikipedia.org/wiki/XML "XML") documents and transform it into an RDF graph
- [Microdata](https://en.wikipedia.org/wiki/Microdata_\(HTML\) "Microdata (HTML)") - another approach at embedding semantics in HTML using additional attributes
- [Microformats](https://en.wikipedia.org/wiki/Microformat "Microformat"), a simplified approach to semantically annotate data in web pages
- [Open Graph protocol](https://en.wikipedia.org/wiki/Open_Graph_protocol "Open Graph protocol"), a way to use RDFa to integrate web pages into the Facebook social graph
- [Schema.org](https://en.wikipedia.org/wiki/Schema.org "Schema.org"), search-engine supported schemas for structured data markup on web pages that can be expressed as RDFa

## References

[^rdfa-primer-1]: ["RDFa 1.1 Primer"](https://www.w3.org/TR/2015/NOTE-rdfa-primer-20150317/) (3rd ed.). [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 17 March 2015. Retrieved 2016-09-02.

[^rdfa_wiki-2]: ["RDFa / Tools"](http://rdfa.info/).

[^xhtml_and_rdf_note1-3]: ["XHTML and RDF W3C Note 14 February 2004"](http://www.w3.org/MarkUp/2004/02/xhtml-rdf.html). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2004-02-14. Retrieved 2007-12-27.

[^4]: ["W3C Semantic Web Interest Group (SWIG)"](http://www.w3.org/2001/sw/interest/).

[^xhtml_and_rdf_note2-5]: ["Semantic Web Interest Group"](http://www.xml.com/pub/a/2004/03/03/deviant.html). *www.xml.com*. 2004-03-03. Retrieved 2007-12-27.

[^xhtml_2_wd_6-6]: ["XHTML 2.0 W3C Working Draft 22 July 2004, 19. XHTML Metainformation Attributes Module"](http://www.w3.org/TR/2004/WD-xhtml2-20040722/mod-metaAttributes.html#s_metaAttributesmodule). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2004-07-22. Retrieved 2007-10-06.

[^timelinehistory-7]: ["XML and Semantic Web W3C Standards Timeline"](https://web.archive.org/web/20130424125723/http://www.dblab.ntua.gr/~bikakis/XML%20and%20Semantic%20Web%20W3C%20Standards%20Timeline-History.pdf) (PDF). Archived from [the original](http://www.dblab.ntua.gr/~bikakis/XML%20and%20Semantic%20Web%20W3C%20Standards%20Timeline-History.pdf) (PDF) on 2013-04-24. Retrieved 2013-06-28.

[^rdfa_1-8]: ["RDF/A Syntax: A collection of attributes for layering RDF on XML languages"](http://www.w3.org/MarkUp/2004/rdf-a.html). 2004-10-11. Retrieved 2009-05-14.

[^rdfa_modules_ed-9]: ["XHTML RDFa Modules, Modules to support RDF annotation of elements, W3C Editor's Draft 2 April 2007"](http://www.w3.org/MarkUp/2007/ED-xhtml-rdfa-20070402). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2007-04-02. Retrieved 2007-10-06.

[^xhtml_rdfa_1_examples-10]: For examples of this, see: ["CBS: NCIS - Joost Link"](https://web.archive.org/web/20071011062935/http://joost.com/09400ax). Archived from [the original](http://www.joost.com/09400ax) on 2007-10-11. Retrieved 2007-10-06. ["WebOrganics :: HAudio RDFa"](https://web.archive.org/web/20071214081908/http://weborganics.co.uk/files/hAudio-RDFa.xhtml). Archived from [the original](http://weborganics.co.uk/files/hAudio-RDFa.xhtml) on 2007-12-14. Retrieved 2007-10-06.

[^rdfa_syntax_wd1-11]: ["RDFa in XHTML: Syntax and Processing, A collection of attributes and processing rules for extending XHTML to support RDF, W3C Working Draft 18 October 2007"](http://www.w3.org/TR/2007/WD-rdfa-syntax-20071018). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2007-10-18. Retrieved 2007-10-20.

[^rdfa_syntax_cr1-12]: ["RDFa in XHTML: Syntax and Processing, A collection of attributes and processing rules for extending XHTML to support RDF, W3C Recommendation 14 October 2008"](http://www.w3.org/TR/2008/REC-rdfa-syntax-20081014). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2008-10-14. Retrieved 2008-10-15.

[^rdfa1_1_core_rec-13]: ["RDFa Core 1.1 - Syntax and processing rules for embedding RDF through attributes"](http://www.w3.org/TR/2012/REC-rdfa-core-20120607). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2012-06-07. Retrieved 2012-08-25.

[^html_plus_rdfa1_1-14]: ["HTML+RDFa 1.1 - Support for RDFa in HTML4 and HTML5"](http://www.w3.org/TR/2012/WD-rdfa-in-html-20120329). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2012-03-29. Retrieved 2012-08-25.

[^xhtml-rdfa-primer0-15]: ["RDF/A Primer 1.0"](https://www.w3.org/TR/2006/WD-xhtml-rdfa-primer-20060310/). [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 10 March 2006. Retrieved 2016-09-02.

[^rdfa2008-16]: "RDFa in XHTML: Syntax and Processing - A collection of attributes and processing rules for extending XHTML to support RDF", W3C Recommendation 14 October 2008. [http://www.w3.org/TR/2008/REC-rdfa-syntax-20081014/](http://www.w3.org/TR/2008/REC-rdfa-syntax-20081014/)

[^html-rdfa-17]: "HTML+RDFa 1.1 - Support for RDFa in HTML4 and HTML5", W3C Recommendation 22 August 2013. [http://www.w3.org/TR/html-rdfa/](http://www.w3.org/TR/html-rdfa/)

[^rdfa-core-18]: "RDFa Core 1.1 - Third Edition - Syntax and processing rules for embedding RDF through attribute", W3C Recommendation 17 March 2015. [https://www.w3.org/TR/2015/REC-rdfa-core-20150317/](https://www.w3.org/TR/2015/REC-rdfa-core-20150317/)

[^rdfalite1.0-19]: [first draft 1.1](http://www.w3.org/TR/2011/WD-rdfa-lite-20111208/).

[^rdfalite1.1-20]: "RDFa Lite 1.1, W3C Recommendation 07 June 2012. [http://www.w3.org/TR/rdfa-lite/](http://www.w3.org/TR/rdfa-lite/) ([second edition at 2015](http://www.w3.org/TR/2015/REC-rdfa-lite-20150210/))

[^21]: [Final W3C position](http://www.w3.org/html/wg/tracker/issues/76) (ISSUE-76), establishing that Microdata syntax simply duplicates what RDFa Lite already does.

[^22]: ["Mythical Differences: RDFa Lite vs. Microdata - The Beautiful, Tormented Machine"](http://manu.sporny.org/2012/mythical-differences).

[^23]: [Building Interoperable Web Metadata](http://assets.adida.net/presentations/w3c-2006-04-06/w3c-2006-04-06.pdf)

[^24]: ["RDFa – Implications for Accessibility – Standards Schmandards"](http://www.standards-schmandards.com/2007/rdfa-and-accessibility/).

[^webstats2013-25]: ["Web Data Commons – RDFa, Microdata, and Microformat Data Sets"](http://webdatacommons.org/structureddata/index.html#toc2). *section 3.1, "Extraction Results from the November 2013 Common Crawl Corpus"*. 2013. Retrieved 2015-02-21.

[^webstats2017-26]: ["Web Data Commons – RDFa, Microdata, and Microformat Data Sets"](http://webdatacommons.org/structureddata/index.html#toc2). *section 3.1, "Extraction Results from the November 2017 Common Crawl Corpus"*. 2017. Retrieved 2019-01-09.

[^27]: ["RDFaCE — Agile Knowledge Engineering and Semantic Web (AKSW)"](http://aksw.org/Projects/RDFaCE).

[^28]: ["RDFaCE — Agile Knowledge Engineering and Semantic Web (AKSW)"](http://aksw.org/Projects/RDFaCE).

[^29]: ["Google Code Archive - Long-term storage for Google Code Project Hosting"](https://code.google.com/p/autometa/).

[^rdfa_initial_context-30]: ["RDFa Core Initial Context - Vocabulary Prefixes"](http://www.w3.org/2011/rdfa-context/rdfa-1.1). [World Wide Web Consortium](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium"). 2012-05-27. Retrieved 2012-08-25.

[^31]: ["Example of an HTML+RDFa 1.1 document" at www.w3.org](http://www.w3.org/TR/html-rdfa/#document-conformance)

[^32]: Murari, Krishna (19 January 2023). ["Person Schema in RDFa"](https://www.theseotoday.com/2023/01/schema-markup-guide.html). *The Seo Today*. [Archived](https://web.archive.org/web/20230119083602/https://www.theseotoday.com/2023/01/structured-data-guide.html) from the original on 19 January 2023. Retrieved 19 January 2023.

## External links

- [RDFa Primer](http://www.w3.org/TR/rdfa-primer/)
- [hGRDDL](http://www.w3.org/2006/07/SWD/wiki/hGRDDL_Example)
- [RDFa – Implications for Accessibility](http://www.standards-schmandards.com/2007/rdfa-and-accessibility/)
- [Mark Birbeck presenting RDFa at Google in May 2008](https://www.youtube.com/watch?v=mxE3FeOyS-E). Video archived at [ghostarchive.org](https://ghostarchive.org/varchive/mxE3FeOyS-E) on 24 May 2022.

![](https://en.wikipedia.org/wiki/Special:CentralAutoLogin/start?type=1x1&usesul3=1)
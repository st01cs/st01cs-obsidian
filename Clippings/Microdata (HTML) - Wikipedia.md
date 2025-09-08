---
categories:
  - "[[Clippings]]"
title: "Microdata (HTML) - Wikipedia"
source: "https://en.wikipedia.org/wiki/Microdata_(HTML)"
author:
  - "[[Wikipedia]]"
created: 2025-09-08
description:
tags:
  - "clippings"
  - "wikipedia"
---
For other uses, see [Microdata (disambiguation)](https://en.wikipedia.org/wiki/Microdata_\(disambiguation\) "Microdata (disambiguation)").

| [HTML](https://en.wikipedia.org/wiki/HTML "HTML") |
| --- |
| [![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/61/HTML5_logo_and_wordmark.svg/60px-HTML5_logo_and_wordmark.svg.png)](https://en.wikipedia.org/wiki/File:HTML5_logo_and_wordmark.svg) |
| HTML and variants |
| - [Dynamic HTML](https://en.wikipedia.org/wiki/Dynamic_HTML "Dynamic HTML") - [HTML5](https://en.wikipedia.org/wiki/HTML5 "HTML5") - [XHTML](https://en.wikipedia.org/wiki/XHTML "XHTML") - [Basic](https://en.wikipedia.org/wiki/XHTML_Basic "XHTML Basic") - [Mobile Profile](https://en.wikipedia.org/wiki/XHTML_Mobile_Profile "XHTML Mobile Profile") |
| HTML elements and attributes |
| - [HTML element](https://en.wikipedia.org/wiki/HTML_element "HTML element") - [article](https://en.wikipedia.org/wiki/Article_element "Article element") - [audio](https://en.wikipedia.org/wiki/HTML_audio "HTML audio") - [blink](https://en.wikipedia.org/wiki/Blink_element "Blink element") - [canvas](https://en.wikipedia.org/wiki/Canvas_element "Canvas element") - [div and span](https://en.wikipedia.org/wiki/Div_and_span "Div and span") - [marquee](https://en.wikipedia.org/wiki/Marquee_element "Marquee element") - [meta](https://en.wikipedia.org/wiki/Meta_element "Meta element") - [video](https://en.wikipedia.org/wiki/HTML_video "HTML video") - [HTML attribute](https://en.wikipedia.org/wiki/HTML_attribute "HTML attribute") - [alt attribute](https://en.wikipedia.org/wiki/Alt_attribute "Alt attribute") - [HTML frame](https://en.wikipedia.org/wiki/Frame_\(World_Wide_Web\) "Frame (World Wide Web)") |
| Editing |
| - [HTML editor](https://en.wikipedia.org/wiki/HTML_editor "HTML editor") - [Text editor](https://en.wikipedia.org/wiki/Text_editor "Text editor") |
| Character encodings and language |
| - [Character encodings](https://en.wikipedia.org/wiki/Character_encodings_in_HTML "Character encodings in HTML") - [Character entity references (amed characters)](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references "List of XML and HTML character entity references") - [Unicode](https://en.wikipedia.org/wiki/Unicode_and_HTML "Unicode and HTML") - [Language code](https://en.wikipedia.org/wiki/Language_code "Language code") |
| Document and browser models |
| - [Document Object Model](https://en.wikipedia.org/wiki/Document_Object_Model "Document Object Model") - [Browser Object Model](https://en.wikipedia.org/wiki/Browser_Object_Model "Browser Object Model") - [Style sheets](https://en.wikipedia.org/wiki/Style_sheet_\(web_development\) "Style sheet (web development)") - [CSS](https://en.wikipedia.org/wiki/CSS "CSS") - [Font family](https://en.wikipedia.org/wiki/Font_family_\(HTML\) "Font family (HTML)") - [Web colors](https://en.wikipedia.org/wiki/Web_colors "Web colors") |
| Client-side scripting and APIs |
| - [JavaScript](https://en.wikipedia.org/wiki/JavaScript "JavaScript") - [WebCL](https://en.wikipedia.org/wiki/WebCL "WebCL") - [HTMX](https://en.wikipedia.org/wiki/HTMX "HTMX") |
| Graphics and Web3D technology |
| - [Web3D](https://en.wikipedia.org/wiki/Web3D "Web3D") - [WebGL](https://en.wikipedia.org/wiki/WebGL "WebGL") - [WebGPU](https://en.wikipedia.org/wiki/WebGPU "WebGPU") - [WebXR](https://en.wikipedia.org/wiki/WebXR "WebXR") - [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium "World Wide Web Consortium") - [Validator](https://en.wikipedia.org/wiki/W3C_Markup_Validation_Service "W3C Markup Validation Service") - [WHATWG](https://en.wikipedia.org/wiki/WHATWG "WHATWG") - [Quirks mode](https://en.wikipedia.org/wiki/Quirks_mode "Quirks mode") - [Web storage](https://en.wikipedia.org/wiki/Web_storage "Web storage") - [Rendering engine](https://en.wikipedia.org/wiki/Browser_engine "Browser engine") |
| Comparisons |
| - [Document markup languages](https://en.wikipedia.org/wiki/Comparison_of_document_markup_languages "Comparison of document markup languages") - [Comparison of browser engines](https://en.wikipedia.org/wiki/Comparison_of_browser_engines "Comparison of browser engines") |
| - [v](https://en.wikipedia.org/wiki/Template:HTML "Template:HTML") - [t](https://en.wikipedia.org/wiki/Template_talk:HTML "Template talk:HTML") - [e](https://en.wikipedia.org/wiki/Special:EditPage/Template:HTML "Special:EditPage/Template:HTML") |

**Microdata** is a [WHATWG](https://en.wikipedia.org/wiki/WHATWG "WHATWG") [HTML](https://en.wikipedia.org/wiki/HTML "HTML") specification used to nest [metadata](https://en.wikipedia.org/wiki/Metadata "Metadata") within existing content on web pages.[^whatwg-1] [Search engines](https://en.wikipedia.org/wiki/Search_engines "Search engines"), [web crawlers](https://en.wikipedia.org/wiki/Web_crawlers "Web crawlers"), and [browsers](https://en.wikipedia.org/wiki/Web_browser "Web browser") can extract and process Microdata from a web page and use it to provide a richer browsing experience for users. Search engines benefit greatly from direct access to Microdata because it allows them to understand the information on web pages and provide more relevant [results](https://en.wikipedia.org/wiki/Search_engine_results_page "Search engine results page") to users.[^2][^3] Microdata uses a supporting vocabulary to describe an item and name-value pairs to assign values to its properties.[^dive-4] Microdata is an attempt to provide a simpler way of annotating [HTML elements](https://en.wikipedia.org/wiki/HTML_element "HTML element") with machine-readable tags than the similar approaches of using [RDFa](https://en.wikipedia.org/wiki/RDFa "RDFa") and [microformats](https://en.wikipedia.org/wiki/Microformat "Microformat").

In 2013, because the W3C HTML Working Group failed to find someone to serve as an editor for the **Microdata HTML** specification, its development was terminated with a 'Note'.[^5][^6] However, since that time, two new editors were selected, and five newer versions of the working draft have been published,[^7][^8][^9][^:0-10] the most recent being Working Draft 26 April 2018.[^:0-10]

## Vocabularies

Microdata vocabularies do not provide the [semantics](https://en.wikipedia.org/wiki/Semantics "Semantics"), or meaning of an Item.[^11] Web developers can design a custom vocabulary or use vocabularies available on the web. A collection of commonly used markup vocabularies are provided by [Schema.org](https://en.wikipedia.org/wiki/Schema.org "Schema.org") schemas which include: *Person*, "*Place*", *Event*, *Organization*, *Product*, *Review*, *Review-aggregate*, *Breadcrumb*, *Offer*, *Offer-aggregate*. The website schema.org was established by search engine operators like [Google](https://en.wikipedia.org/wiki/Google "Google"), [Microsoft](https://en.wikipedia.org/wiki/Microsoft "Microsoft"), [Yahoo!](https://en.wikipedia.org/wiki/Yahoo! "Yahoo!"), and [Yandex](https://en.wikipedia.org/wiki/Yandex "Yandex"), which use microdata markup to improve search results.[^12] 

For some purposes, an ad-hoc vocabulary is adequate. For others, a vocabulary will need to be designed. Where possible, authors are encouraged to re-use existing vocabularies, as this makes content re-use easier.[^whatwg-1]

## Localization

In some cases, search engines covering specific regions may provide locally-specific extensions of microdata. For example, [Yandex](https://en.wikipedia.org/wiki/Yandex "Yandex"), a major search engine in Russia, supports [microformats](https://en.wikipedia.org/wiki/Microformats "Microformats") such as [hCard](https://en.wikipedia.org/wiki/HCard "HCard") (company contact information), [hRecipe](https://en.wikipedia.org/wiki/HRecipe "HRecipe") (food recipe), [hReview](https://en.wikipedia.org/wiki/HReview "HReview") (market reviews) and [hProduct](https://en.wikipedia.org/wiki/HProduct "HProduct") (product data) and provides its own format for definition of the terms and encyclopedic articles. This extension was made in order to solve [transliteration](https://en.wikipedia.org/wiki/Transliteration "Transliteration") problems between the Cyrillic and Latin alphabets. After the implementation of additional parameters from Schema's vocabulary,[^academicyan-13] indexation of information in Russian-language web-pages became more successful.

## Global attributes

- `itemscope` – Creates the Item and indicates that descendants of this [element](https://en.wikipedia.org/wiki/HTML_element "HTML element") contain information about it.[^whatwg-1]
- `itemtype` – A valid URL of a vocabulary that describes the item and its properties' context.
- `itemid` – Indicates a unique identifier of the item.
- `itemprop` – Indicates that its containing tag holds the value of the specified item property. The property's name and value context are described by the item's vocabulary. Properties values usually consist of string values, but can also use URLs using the `a` element and its `href` attribute, the `img` element and its `src` attribute, or other elements that link to or embed external resources.[^whatwg-1]
- `itemref` – Properties that are not descendants of the element with the `itemscope` attribute can be associated with the item using this attribute. Provides a list of element IDs (not `itemid`s) with additional properties elsewhere in the document.[^whatwg-1]
- `datetime` – Indicates date or duration as specified by [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601 "ISO 8601") standard.

## Example

The following HTML5 markup may be found on a typical “About” page containing information about a person:

```
<div> Hello, my name is John Doe, I am a graduate research assistant at
the University of Dreams.
My friends call me Johnny. 
You can visit my homepage at <a href="http://www.example.com/~JohnnyD">www.example.com/~JohnnyD</a>.
I live at 1234 Peach Drive, Warner Robins, Georgia.</div>
```

Here is the same markup with added [Schema.org](https://en.wikipedia.org/wiki/Schema.org "Schema.org")[^14][^15][^16] Microdata:

```
<div itemscope itemtype="http://schema.org/Person"> 
	Hello, my name is 
	<span itemprop="name">John Doe</span>, 
	I am a 
	<span itemprop="jobTitle">graduate research assistant</span> 
	at the 
	<span itemprop="affiliation">University of Dreams</span>. 
	My friends call me 
	<span itemprop="additionalName">Johnny</span>. 
	You can visit my homepage at 
	<a href="http://www.example.com/~JohnnyD" itemprop="url">www.example.com/~JohnnyD</a>. 
	<div itemprop="address" itemscope itemtype="http://schema.org/PostalAddress">
		I live at 
		<span itemprop="streetAddress">1234 Peach Drive</span>,
		<span itemprop="addressLocality">Warner Robins</span>,
		<span itemprop="addressRegion">Georgia</span>.
	</div>
</div>
```

As the above example shows, Microdata items can be nested. In this case, an item of type [http://schema.org/PostalAddress](http://schema.org/PostalAddress) is nested inside an item of type [http://schema.org/Person](http://schema.org/Person).

The following text shows how Google parses the Microdata from the above example code. Developers can test pages containing Microdata using Google's *Rich Snippet Testing Tool*.[^googlers-17]

```
Item
   Type: http://schema.org/Person
   name = John Doe
   jobTitle = graduate research assistant
   affiliation = University of Dreams
   additionalName = Johnny
   url = http://www.example.com/~JohnnyD
   address = Item(1)
Item 1
   Type: http://schema.org/PostalAddress
   streetAddress = 1234 Peach Drive
   addressLocality = Warner Robins
   addressRegion = Georgia
```

The same machine-readable terms can be used not only in HTML Microdata, but also in other annotations such as [RDFa](https://en.wikipedia.org/wiki/RDFa "RDFa") or [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD "JSON-LD") in the markup, or in an external [RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework "Resource Description Framework") file in a serialization such as [RDF/XML](https://en.wikipedia.org/wiki/RDF/XML "RDF/XML"), [Notation3](https://en.wikipedia.org/wiki/Notation3 "Notation3"), or [Turtle](https://en.wikipedia.org/wiki/Turtle_\(syntax\) "Turtle (syntax)").

## Support

- Servers: [Google](https://en.wikipedia.org/wiki/Google "Google") can[^googlecan-18] use microdata in its [result pages](https://en.wikipedia.org/wiki/Search_engine_results_page "Search engine results page").[^googlers-17] It was the preferred snippet format for the [Google+](https://en.wikipedia.org/wiki/Google%2B "Google+") social network.[^19]
- Browsers: As of July 2021, no major browser supports the Microdata [DOM](https://en.wikipedia.org/wiki/Document_Object_Model "Document Object Model") [API](https://en.wikipedia.org/wiki/API "API").[^20] Opera supported it from 11.60 (released in 2011), but since removed its implementation.[^21] Firefox removed it in version 49.[^22]

## See also

- [Semantic web](https://en.wikipedia.org/wiki/Semantic_web "Semantic web")
- [Microformat](https://en.wikipedia.org/wiki/Microformat "Microformat")
- [RDFa Lite](https://en.wikipedia.org/wiki/RDFa_Lite "RDFa Lite")
- [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD "JSON-LD")
- [CP/LD (Content Profile/Linked Document)](https://en.wikipedia.org/wiki/CP/LD "CP/LD")
- [Semantic HTML](https://en.wikipedia.org/wiki/Semantic_HTML "Semantic HTML")
- [Semantic social network](https://en.wikipedia.org/wiki/Semantic_social_network "Semantic social network")

## References

[^whatwg-1]: ["Microdata — HTML Draft Standard"](https://www.whatwg.org/specs/web-apps/current-work/multipage/microdata.html). Whatwg.org. Retrieved 2016-06-30.

[^2]: ["MicroData - The Future of Search Engine Relevance and Optimization (SEO)"](http://www.lyquix.com/blog-and-news/microdata-the-future-of-search-engine-relevance-and-search-engine-optimization-seo). Lyquix.com. Retrieved 2016-06-30.

[^3]: Schema.org [http://schema.org/](http://schema.org/)

[^dive-4]: [""Distributed," "Extensibility," And Other Fancy Words"](http://diveintohtml5.info/extensibility.html). Diveintohtml5.info. Retrieved 2016-06-30.

[^5]: Cotton, Paul (2 Oct 2013). ["WG Decision to publish HTML Microdata as a WG Note"](https://lists.w3.org/Archives/Public/public-html-admin/2013Oct/0018.html). *public-html-admin@w3.org* (Mailing list). Retrieved 2016-06-30.

[^6]: ["HTML Microdata"](http://www.w3.org/TR/microdata/). W3.org. 23 June 2014. Retrieved 2016-06-30.

[^7]: ["HTML Microdata W3C First Public Working Draft 04 May 2017"](https://www.w3.org/TR/2017/WD-microdata-20170504/). *World Wide Web Consortium (W3C)*. Retrieved 2017-09-06.

[^8]: ["HTML Microdata W3C Working Draft 26 June 2017"](https://www.w3.org/TR/2017/WD-microdata-20170626/). *World Wide Web Consortium (W3C)*. Retrieved 2017-09-06.

[^9]: ["HTML Microdata W3C Working Draft 09 October 2017"](https://www.w3.org/TR/2017/WD-microdata-20171009/). *World Wide Web Consortium (W3C)*. 9 October 2017. Retrieved 16 March 2018.

[^:0-10]: ["HTML Microdata W3C Working Draft 10 October 2017"](https://www.w3.org/TR/2017/WD-microdata-20171010/). *World Wide Web Consortium (W3C)*. 10 October 2017. Retrieved 16 March 2018.

[^11]: ["HTML Standard"](https://html.spec.whatwg.org/multipage/microdata.html). *Web Hypertext Application Technology Working Group*. Retrieved 30 December 2016.

[^12]: MacDonald, Matthew (2014). *HTML5: The missing manual* (2nd ed.). [O'Reilly and Associates](https://en.wikipedia.org/wiki/O%27Reilly_and_Associates "O'Reilly and Associates"). [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-1-4493-6326-0](https://en.wikipedia.org/wiki/Special:BookSources/978-1-4493-6326-0 "Special:BookSources/978-1-4493-6326-0").

[^academicyan-13]: ["Semantic markup deployment in Russia"](https://www.academia.edu/6732371). Academia.edu. Retrieved 2016-06-30.

[^14]: ["Documentation"](http://schema.org/docs/documents.html). Schema.org. Retrieved 2016-06-30.

[^15]: ["Type Hierarchy"](http://schema.org/docs/full.html). Schema.org. Retrieved 2016-06-30.

[^16]: ["Schema.org Turtle RDFS Schema"](https://web.archive.org/web/20140921103224/http://schema.rdfs.org/all.ttl). Archived from [the original](http://schema.rdfs.org/all.ttl) on 2014-09-21. Retrieved 2013-05-29.

[^googlers-17]: ["Rich snippets (microdata, microformats, RDFa)"](https://developers.google.com/structured-data/testing). Google Inc. 2016-05-17. Retrieved 2016-06-30.

[^googlecan-18]: ["Rich Snippet display clarification"](https://www.google.com/support/webmasters/bin/answer.py?answer=99170). 2016-06-22. Retrieved 2016-06-30.

[^19]: Google Webmasters Channel (2011-12-06). [*Types of Rich Snippets*](https://www.youtube.com/watch?v=4W8Ah394bH8) (Video). [Archived](https://ghostarchive.org/varchive/youtube/20211215/4W8Ah394bH8) from the original on 2021-12-15. Retrieved 2016-06-30. `{{[cite AV media](https://en.wikipedia.org/wiki/Template:Cite_AV_media "Template:Cite AV media")}}`: `|author=` has generic name ([help](https://en.wikipedia.org/wiki/Help:CS1_errors#generic_name "Help:CS1 errors"))

[^20]: ["Microdata DOM API - Web APIs | MDN"](https://developer.mozilla.org/en-US/docs/Web/API/Microdata_DOM_API). *developer.mozilla.org*. Retrieved 2021-07-05.

[^21]: Opera Software Documentation Team (2011-12-06). ["Opera 11.60 for Windows changelog"](https://web.archive.org/web/20141023082043/http://www.opera.com/docs/changelogs/windows/1160/). Opera.com. Archived from [the original](http://www.opera.com/docs/changelogs/windows/1160/) on 2014-10-23. Retrieved 2016-06-30.

[^22]: ["909633 - Remove HTML Microdata API"](https://bugzilla.mozilla.org/show_bug.cgi?id=909633). *bugzilla.mozilla.org*. Retrieved 2021-07-05.

## External links

- [*Microdata — HTML Draft Standard*](https://html.spec.whatwg.org/multipage/microdata.html), [WHATWG](https://en.wikipedia.org/wiki/Web_Hypertext_Application_Technology_Working_Group "Web Hypertext Application Technology Working Group")
- [*W3C HTML Microdata Working Group Note*](https://www.w3.org/TR/microdata/), [W3C](https://en.wikipedia.org/wiki/W3C "W3C")
- Almaer, Dion (2009-05-11), [*Hixie discusses the addition of HTML5 "microdata"*](https://web.archive.org/web/20091212053447/http://ajaxian.com/archives/hixie-discusses-the-addition-of-html5-microdata), Ajaxian, archived from [the original](http://ajaxian.com/archives/hixie-discusses-the-addition-of-html5-microdata) on 2009-12-12
- [*HTML5 Microdata Specs*](http://www.data-vocabulary.org/), Data-Vocabulary.org

![](https://en.wikipedia.org/wiki/Special:CentralAutoLogin/start?type=1x1&usesul3=1)
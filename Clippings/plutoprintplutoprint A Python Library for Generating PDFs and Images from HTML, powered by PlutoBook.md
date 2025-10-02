---
title: "plutoprint/plutoprint: A Python Library for Generating PDFs and Images from HTML, powered by PlutoBook"
source: "https://github.com/plutoprint/plutoprint"
author:
  - "[[sammycage]]"
published:
created: 2025-10-01
description: "A Python Library for Generating PDFs and Images from HTML, powered by PlutoBook - plutoprint/plutoprint"
tags:
  - "clippings"
---
**[plutoprint](https://github.com/plutoprint/plutoprint)** Public

A Python Library for Generating PDFs and Images from HTML, powered by PlutoBook

[plutoprint.readthedocs.io](https://plutoprint.readthedocs.io/ "https://plutoprint.readthedocs.io")

[MIT license](https://github.com/plutoprint/plutoprint/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/plutoprint/plutoprint?resume=1)

## PlutoPrint

PlutoPrint is a lightweight and easy-to-use Python library for generating high-quality PDFs and images directly from HTML or XML content. It is based on [PlutoBook’s](https://github.com/plutoprint/plutobook) robust rendering engine and provides a simple API to convert your HTML into crisp PDF documents or vibrant image files. This makes it ideal for reports, invoices, or visual snapshots.

| Invoices | Tickets |
| --- | --- |
| [![Invoices](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoices.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoices.png) | [![Tickets](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/tickets.jpg)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/tickets.jpg) |

### Installation

```
pip install plutoprint
```

PlutoPrint requires [PlutoBook](https://github.com/plutoprint/plutobook). On Windows (`win_amd64`), Linux (`manylinux_2_28_x86_64`) and macOS (`macosx_14_0_arm64`), prebuilt binaries are bundled with the package and no further steps are necessary. On other architectures or when building from source, see the [Getting Started guide](https://plutoprint.readthedocs.io/en/latest/getting_started.html) for dependency setup and build instructions.

On **macOS** and **Linux**, you can also install PlutoPrint using [Homebrew](https://formulae.brew.sh/formula/plutoprint):

```
brew update
brew install plutoprint
```

### Quick Usage

Generate a PDF from the command line with the installed `plutoprint` script:

```
plutoprint input.html output.pdf --size=A4
```
```
import plutoprint

book = plutoprint.Book(plutoprint.PAGE_SIZE_A4)
book.load_url("hello.html")

# Export the entire document to PDF
book.write_to_pdf("hello.pdf")

# Export pages 2 to 15 (inclusive) in order
book.write_to_pdf("hello-range.pdf", 2, 15, 1)

# Export pages 15 to 2 (inclusive) in reverse order
book.write_to_pdf("hello-reverse.pdf", 15, 2, -1)

# Render pages manually with PDFCanvas (in reverse order)
with plutoprint.PDFCanvas("hello-canvas.pdf", book.get_page_size()) as canvas:
   canvas.scale(plutoprint.UNITS_PX, plutoprint.UNITS_PX)
   for page_index in range(book.get_page_count() - 1, -1, -1):
      canvas.set_size(book.get_page_size_at(page_index))
      book.render_page(canvas, page_index)
      canvas.show_page()
```
```
import plutoprint
import math

book = plutoprint.Book(media=plutoprint.MEDIA_TYPE_SCREEN)
book.load_html("<b>Hello World</b>", user_style="body { text-align: center }")

# Outputs an image at the document’s natural size
book.write_to_png("hello.png")

# Outputs a 320px wide image with auto-scaled height
book.write_to_png("hello-width.png", width=320)

# Outputs a 240px tall image with auto-scaled width
book.write_to_png("hello-height.png", height=240)

# Outputs an 800×200 pixels image (may stretch/squish content)
book.write_to_png("hello-fixed.png", 800, 200)

# Get the natural document size
width = math.ceil(book.get_document_width())
height = math.ceil(book.get_document_height())

# Outputs a high-resolution 5x scaled image
book.write_to_png("hello-scaled.png", width * 5, height * 5)

# Render manually on a canvas with white background
with plutoprint.ImageCanvas(width, height) as canvas:
   canvas.clear_surface(1, 1, 1)
   book.render_document(canvas)
   canvas.write_to_png("hello-canvas.png")
```

Quick example of using `-pluto-qrcode(<string>[, <color>])` to create QR codes with optional colors.

```
import plutoprint

HTML_CONTENT = """
<table>
  <tr>
    <th class="email">Email</th>
    <th class="tel">Tel</th>
  </tr>
  <tr>
    <th class="website">Website</th>
    <th class="github">GitHub</th>
  </tr>
</table>
"""

USER_STYLE = """
body {
  margin: 0;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f7f7f7;
  font: 16px Arial;
}

table {
  border-spacing: 2rem;
  background: #fff;
  padding: 2rem;
  border: 1px solid #ccc;
  border-radius: 16px;
}

th::before {
  display: block;
  width: 130px;
  height: 130px;
  margin: 0 auto 0.8rem;
}

.email::before   { content: -pluto-qrcode('mailto:contact@example.com', #16a34a); }
.tel::before     { content: -pluto-qrcode('tel:+1234567890', #2563eb); }
.website::before { content: -pluto-qrcode('https://example.com', #ef4444); }
.github::before  { content: -pluto-qrcode('https://github.com/plutoprint', #f59e0b); }
"""

book = plutoprint.Book(plutoprint.PAGE_SIZE_LETTER.landscape())
book.load_html(HTML_CONTENT, USER_STYLE)
book.write_to_png("qrcard.png")
book.write_to_pdf("qrcard.pdf")
```

Expected output:

[![QR card](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/qrcard.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/qrcard.png)

```
import plutoprint

import matplotlib.pyplot as plt
import urllib.parse
import io

class CustomResourceFetcher(plutoprint.ResourceFetcher):
   def fetch_url(self, url):
      if not url.startswith('chart:'):
         return super().fetch_url(url)
      values = [float(v) for v in urllib.parse.unquote(url[6:]).split(',')]
      labels = [chr(65 + i) for i in range(len(values))]

      plt.bar(labels, values)
      plt.title('Bar Chart')
      plt.xlabel('Labels')
      plt.ylabel('Values')

      buffer = io.BytesIO()
      plt.savefig(buffer, format='svg', transparent=True)

      return plutoprint.ResourceData(buffer.getvalue(), "image/svg+xml", "utf-8")

book = plutoprint.Book(plutoprint.PAGE_SIZE_A4.landscape(), plutoprint.PAGE_MARGINS_NONE)

book.custom_resource_fetcher = CustomResourceFetcher()

HTML_CONTENT = """
<body>
  <img src='chart:23,45,12,36,28,50'>
  <img src='chart:5,15,25,35,45'>
  <img src='chart:50,40,30,20,10'>
  <img src='chart:10,20,30,40,50,60,70'>
</body>
"""

USER_STYLE = """
body {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  background: #f7f7f7;
  height: 100vh;
  margin: 0;
}

img {
  background: #fff;
  border: 1px solid #ccc;
  margin: auto;
  max-height: 45vh;
}
"""

book.load_html(HTML_CONTENT, USER_STYLE)
book.write_to_png("charts.png")
book.write_to_pdf("charts.pdf")
```

Expected output:

[![Charts](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/charts.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/charts.png)

## Samples

Invoices

| [![Invoice 1](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoice-1.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoice-1.png) | [![Invoice 2](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoice-2.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoice-2.png) | [![Invoice 3](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoice-3.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/invoice-3.png) |
| --- | --- | --- |

Tickets

| [![Ticket 1](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-1.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-1.png) | [![Ticket 2](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-2.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-2.png) |
| --- | --- |
| [![Ticket 3](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-3.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-3.png) | [![Ticket 4](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-4.png)](https://raw.githubusercontent.com/plutoprint/plutoprint-samples/main/images/ticket-4.png) |

- Documentation: [https://plutoprint.readthedocs.io](https://plutoprint.readthedocs.io/)
- Samples: [https://github.com/plutoprint/plutoprint-samples](https://github.com/plutoprint/plutoprint-samples)
- Code: [https://github.com/plutoprint/plutoprint](https://github.com/plutoprint/plutoprint)
- Issues: [https://github.com/plutoprint/plutoprint/issues](https://github.com/plutoprint/plutoprint/issues)
- Donation: [https://github.com/sponsors/plutoprint](https://github.com/sponsors/plutoprint)

## License

PlutoPrint is licensed under the [MIT License](https://github.com/plutoprint/plutoprint/blob/main/LICENSE), allowing for both personal and commercial use.

## Releases 12

[\+ 11 releases](https://github.com/plutoprint/plutoprint/releases)

## Sponsor this project

[**plutoprint** PlutoPrint](https://github.com/plutoprint)

[Sponsor](https://github.com/sponsors/plutoprint)

[Learn more about GitHub Sponsors](https://github.com/sponsors)

## Packages

No packages published  

## Languages

- [Python 51.4%](https://github.com/plutoprint/plutoprint/search?l=python)
- [C 47.3%](https://github.com/plutoprint/plutoprint/search?l=c)
- [Meson 1.3%](https://github.com/plutoprint/plutoprint/search?l=meson)
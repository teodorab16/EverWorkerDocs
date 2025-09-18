---
title: ● PDF to Images
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

# Overview

Convert PDF files to images with configurable resolution and format settings.

# When to Use

Use this node when you need to convert PDF documents into images for visual processing, OCR, or analysis by AI vision models.

# Parameters

* pdfFile (required) - PDF file to convert to images
  * Type: file
  * Accept: .pdf
  * Placeholder: "Upload PDF file to convert to images"
* dpi (optional) - DPI resolution (72-600)
  * Type: number
  * Default: 200
  * Range: 72-600
* format (optional) - Output image format
  * Default: "png"

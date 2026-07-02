# Moodle XML → QTI Converter

A lightweight, browser-based converter for turning **Moodle XML question bank exports** into **IMS QTI format** for use in Canvas and other LMS environments.

The tool runs entirely in the browser. Users upload a Moodle XML file, review detected questions, select an export format, and download a QTI-compatible file.

---

## Features

* Drag-and-drop Moodle XML upload
* Parses Moodle question bank exports directly in the browser
* Displays question statistics before export
* Shows question name, type, points, and readiness status
* Supports multiple Moodle question types
* Converts questions to IMS QTI
* Exports as:

  * Single QTI 1.2 XML file
  * Canvas-ready ZIP package with `imsmanifest.xml`
* Handles embedded images for ZIP exports
* Attempts to import remote images when browser permissions allow
* Sanitizes question and answer HTML for safer LMS import
* Provides warnings for unsupported or incomplete questions

---

## Supported Question Types

The converter detects and processes the following Moodle question types:

| Moodle Type     | Export Handling                        |
| --------------- | -------------------------------------- |
| Multiple choice | QTI multiple choice / multiple answers |
| True/False      | QTI true/false                         |
| Short answer    | QTI short answer                       |
| Essay           | QTI essay                              |
| Matching        | QTI matching in QTI 2.1 ZIP export     |
| Numerical       | QTI numerical in QTI 2.1 ZIP export    |

Unsupported question types are still included where possible but may be exported as essay-style questions depending on the selected output format.

---

## Export Options

### QTI Version

The interface includes two QTI version options:

* **QTI 1.2**
  Recommended for Canvas and general compatibility.

* **QTI 2.1**
  Experimental option for item-level ZIP exports.

### Package Type

The converter can export in two formats:

#### Single XML File

Exports a standalone QTI 1.2 XML file.

Best for simple question banks without embedded media.

Generated filename:

```text
canvas_qti_1.2_export.xml
```

#### Canvas ZIP with Manifest

Exports a ZIP package containing:

* Individual question XML files
* Embedded image assets when available
* `imsmanifest.xml`

Best for Canvas imports, especially when questions include images.

Generated filename pattern:

```text
canvas_qti_1.2.zip
canvas_qti_2.1.zip
```

---

## How to Use

1. Export a question bank from Moodle as a Moodle XML file.
2. Open the converter in a browser.
3. Click the upload area or drag the `.xml` file into the drop zone.
4. Review the detected questions and warnings.
5. Choose:

   * QTI version
   * Package type
6. Click **Convert & download**.
7. Import the exported file into Canvas or another LMS that supports QTI.

---

## Running Locally

Because this is a standalone HTML file, no build process is required.

Clone the repository:

```bash
git clone https://github.com/your-username/moodle-xml-qti-converter.git
cd moodle-xml-qti-converter
```

Open the file in a browser:

```bash
open index.html
```

Or simply double-click `index.html`.

---

## Dependencies

The app uses:

* HTML
* CSS
* Vanilla JavaScript
* [JSZip](https://stuk.github.io/jszip/) for ZIP packaging
* Google Fonts:

  * IBM Plex Sans
  * IBM Plex Mono

JSZip is loaded from a CDN:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
```

No server-side runtime is required.

---

## Browser Requirements

Use a modern browser with support for:

* `FileReader`
* `DOMParser`
* `Blob`
* `URL.createObjectURL`
* `fetch`
* ES6 JavaScript syntax

Recommended browsers:

* Chrome
* Edge
* Firefox
* Safari

---

## Image Handling

The converter includes special handling for images in Moodle XML exports.

### Embedded Moodle Images

Images embedded in Moodle XML as base64 files can be packaged into the Canvas ZIP export.

### Remote Images

Remote images are detected and may be imported into the ZIP package if the browser is allowed to fetch them.

Remote image import may fail if the source:

* Requires authentication
* Blocks cross-origin browser requests
* Returns a non-image response
* Is unavailable

### Single XML Export

For single XML export, embedded image files may be omitted to keep Canvas import behavior stable. Use the ZIP option when preserving images is important.

---

## HTML Sanitization

The converter sanitizes question and answer content before export.

Allowed elements include common instructional content tags such as:

* Paragraphs
* Lists
* Tables
* Links
* Images
* Bold and italic text
* Code/preformatted text
* Subscript and superscript

Blocked or stripped elements include:

* Scripts
* Iframes
* Forms
* Inputs
* Embedded objects
* SVG
* Canvas
* External styles and metadata

This helps reduce import issues and removes unsafe or unsupported HTML.

---

## Known Limitations

* QTI 1.2 support is the safest option for Canvas.
* QTI 2.1 export is experimental.
* Some Moodle question types may not translate cleanly to Canvas.
* Matching and numerical questions have stronger support in the QTI 2.1 item export path than in the single QTI 1.2 XML path.
* Remote images may not import because of browser security restrictions.
* Cloze questions are detected but not fully converted as native cloze items.
* Complex Moodle question behavior, feedback, penalties, hints, and advanced grading logic may not be preserved.
* Canvas import behavior may vary between Classic Quizzes and New Quizzes.

---

## Recommended Workflow

For Canvas migration work:

1. Export the Moodle question bank as Moodle XML.
2. Run the XML through this converter.
3. Use **QTI 1.2** and **Canvas ZIP with manifest** for the first import test.
4. Import into a Canvas sandbox course.
5. Review question formatting, images, point values, and correct answers.
6. Fix warnings in Moodle or the XML source if needed.
7. Re-export and re-import after cleanup.

---

## File Structure

A simple repository structure may look like this:

```text
moodle-xml-qti-converter/
├── index.html
├── README.md
└── LICENSE
```

---

## Development Notes

The converter is intentionally written as a single-page app with no build step. Core functionality is organized into JavaScript functions for:

* File upload handling
* Moodle XML parsing
* Question type detection
* HTML sanitization
* Image extraction and packaging
* QTI 1.2 generation
* QTI 2.1 generation
* IMS manifest generation
* ZIP creation and download

This makes the project easy to host on GitHub Pages or run locally without additional tooling.

---

## GitHub Pages Deployment

This project can be hosted directly with GitHub Pages.

1. Push `index.html` and `README.md` to a GitHub repository.
2. Go to **Settings → Pages**.
3. Set the source branch to `main`.
4. Save the Pages settings.
5. Open the generated GitHub Pages URL.

---

## Privacy

All conversion work happens in the user’s browser. The uploaded Moodle XML file is not sent to a server by this app.

Remote image import may request external image URLs if the source XML references remote images and the user chooses an export path that attempts image packaging.

---

## License

Choose a license that matches your intended use.

Common options:

* MIT License for open reuse
* GPL if derivative work should remain open
* Internal/private license if used only within an institution

---

## Disclaimer

This tool is intended to assist with Moodle-to-Canvas question bank migration. Always review imported quizzes in Canvas before using them in a live course.

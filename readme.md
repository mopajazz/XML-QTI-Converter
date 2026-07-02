# Moodle XML → QTI Converter

A lightweight browser-based tool for converting **Moodle XML question bank exports** into **IMS QTI format** for Canvas and other LMS platforms.

The converter runs entirely in the browser. Upload a Moodle XML file, review the detected questions, choose an export format, and download a Canvas-ready QTI file or ZIP package.

---

## Features

- Drag-and-drop Moodle XML upload
- Browser-based conversion with no server required
- Question summary dashboard
- Question preview table with type, points, and status
- QTI 1.2 export for Canvas compatibility
- Experimental QTI 2.1 ZIP export
- Canvas ZIP packaging with `imsmanifest.xml`
- Embedded image handling for ZIP exports
- Remote image import when browser permissions allow
- HTML cleanup and sanitization before export
- Warnings for unsupported or incomplete questions

---

## Supported Question Types

| Moodle question type | Export support |
|---|---|
| Multiple choice | Supported |
| True/False | Supported |
| Short answer | Supported |
| Essay | Supported |
| Matching | Supported in QTI 2.1 ZIP export |
| Numerical | Supported in QTI 2.1 ZIP export |
| Other types | Exported where possible, often as essay-style questions |

---

## Export Options

### QTI Version

| Option | Notes |
|---|---|
| QTI 1.2 | Recommended for Canvas and general LMS compatibility |
| QTI 2.1 | Experimental item-level export |

### Package Format

| Format | Best for |
|---|---|
| Single XML file | Simple question banks without embedded media |
| Canvas ZIP with manifest | Canvas imports, especially when images are included |

Generated files may include:

```text
canvas_qti_1.2_export.xml
canvas_qti_1.2.zip
canvas_qti_2.1.zip
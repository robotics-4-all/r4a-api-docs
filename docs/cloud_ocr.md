# OCR API
---

## *CloudAPI*.**performOcr**

Performs OCR from camera

#### Input parameters

An `InputMessage`, containing in `data`:

- `lang`: Language in ISO639-1 standard
- `file`: The file path of the image

#### Output

The TekVariables affected are:

- `TekVariables.OCR_DETECTION`: The string result of OCR

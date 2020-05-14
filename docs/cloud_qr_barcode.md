# QR/Barcode detection API
---

## *CloudAPI*.**detectQr** / *CloudAPI*.**detectBarcode**

Detects QR codes / Barcodes from camera.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the image

#### Output

The TekVariables affected are:

- `TekVariables.QR_DETECTION_DETECTED`: Bool value denoting the detection success
- `TekVariables.QR_DETECTION`: The QR data
- `TekVariables.BARCODE_DETECTION_DETECTED`: The number of faces detected
- `TekVariables.BARCODE_DETECTION`: The Barcode data

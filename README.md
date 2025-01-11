SynPDF
======

Synopse PDF engine is a fully featured *Open Source* PDF document creation library for Delphi, embedded in one unit.

Original repository https://github.com/synopse/SynPDF

Extentions
==========

TPdfDocument.AddEmbeddedStream
------------------------------

Allows you to add a file stream to a PDF.

Parameter Stream is a stream containing the file data.

Parameter StreamName is the filename inside the PDF.

Parameter Description describes the content of the file in plain text.

Parameter DataType defines the MIME type of the file (text/xml).

Parameter CreationDate and ModDate contains date/time of creation and modification.

Parameter AFRelationship defines the relationship (afrUnspecified, afrSource, afrData, afrAlternative, afrSupplement)


Example:

To embedd a xrechnung.xml stream in a Factur-X/ZUGFeRD PDF:

```
AddEmbeddedStream(<streamobject>, 'xrechnung.xml', 'XRechnung Rechnung', 'text/xml', <creation date/time>, <modification date/time>, afrAlternative);
```

AFRelationship = afrAlternative see Factur-X specification 1.07.2 page 68

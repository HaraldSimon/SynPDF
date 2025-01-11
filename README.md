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

TPdfDocument.PDFMetaDataExtention
---------------------------------

Allows you to specifying additional metadata for PDF/A.

Example:

To add Factur-X/ZUGFeRD metadata:

```
  type
    PDFMetaDataExtentionZugferd : PDFString =
    '<rdf:Description xmlns:fx="urn:factur-x:pdfa:CrossIndustryDocument:invoice:1p0#" rdf:about="">' + // Factur-X specification 1.07.2  page 69f
    '<fx:DocumentType>INVOICE</fx:DocumentType>' +
    '<fx:DocumentFileName>xrechnung.xml</fx:DocumentFileName>' +
    '<fx:Version>2.3</fx:Version>' +                                                                   // specification wants 2p3 but validators rejects
    '<fx:ConformanceLevel>XRECHNUNG</fx:ConformanceLevel>' +
    '</rdf:Description>' +
    '<rdf:Description xmlns:pdfaExtension="http://www.aiim.org/pdfa/ns/extension/" xmlns:pdfaField="http://www.aiim.org/pdfa/ns/field#" xmlns:pdfaProperty="http://www.aiim.org/pdfa/ns/property#" xmlns:pdfaSchema="http://www.aiim.org/pdfa/ns/schema#" xmlns:pdfaType="http://www.aiim.org/pdfa/ns/type#" rdf:about="">' +
    '<pdfaExtension:schemas>' +
    '<rdf:Bag>' +
    '<rdf:li rdf:parseType="Resource">' +
    '<pdfaSchema:schema>Factur-X PDFA Extension Schema</pdfaSchema:schema>' +
    '<pdfaSchema:namespaceURI>urn:factur-x:pdfa:CrossIndustryDocument:invoice:1p0#</pdfaSchema:namespaceURI>' +   // Factur-X specification 1.07.2  page 69
    '<pdfaSchema:prefix>fx</pdfaSchema:prefix>' +
    '<pdfaSchema:property>' +
    '<rdf:Seq>' +
    '<rdf:li rdf:parseType="Resource">' +
    '<pdfaProperty:name>DocumentFileName</pdfaProperty:name>' +
    '<pdfaProperty:valueType>Text</pdfaProperty:valueType>' +
    '<pdfaProperty:category>external</pdfaProperty:category>' +
    '<pdfaProperty:description>name of the embedded XML invoice file</pdfaProperty:description>' +
    '</rdf:li>' +
    '<rdf:li rdf:parseType="Resource">' +
    '<pdfaProperty:name>DocumentType</pdfaProperty:name>' +
    '<pdfaProperty:valueType>Text</pdfaProperty:valueType>' +
    '<pdfaProperty:category>external</pdfaProperty:category>' +
    '<pdfaProperty:description>INVOICE</pdfaProperty:description>' +
    '</rdf:li>' +
    '<rdf:li rdf:parseType="Resource">' +
    '<pdfaProperty:name>Version</pdfaProperty:name>' +
    '<pdfaProperty:valueType>Text</pdfaProperty:valueType>' +
    '<pdfaProperty:category>external</pdfaProperty:category>' +
    '<pdfaProperty:description>The actual version of the ZUGFeRD data</pdfaProperty:description>' +
    '</rdf:li>' +
    '<rdf:li rdf:parseType="Resource">' +
    '<pdfaProperty:name>ConformanceLevel</pdfaProperty:name>' +
    '<pdfaProperty:valueType>Text</pdfaProperty:valueType>' +
    '<pdfaProperty:category>external</pdfaProperty:category>' +
    '<pdfaProperty:description>The conformance level of the ZUGFeRD data</pdfaProperty:description>' +
    '</rdf:li>' +
    '</rdf:Seq>' +
    '</pdfaSchema:property>' +
    '</rdf:li>' +
    '</rdf:Bag>' +
    '</pdfaExtension:schemas>' +
    '</rdf:Description>';

    ...

    obPDF:=TPdfDocument.Create(false, 0, pdfa3B);                  // define USE_PDFALEVEL enabled
    obPDF.PDFMetaDataExtention:=PDFMetaDataExtentionZugferd;
```
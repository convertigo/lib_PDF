# lib_PDF #

A Convertigo library for handling PDF forms.

## Intro ##
In many projects you have to handle PDF generation. This can be done with Convertigo with XSL-FO technology but writing XSL-FO style sheets is sometimes not so easy. This is why this library was developed to use the PDF Form technology instead.

## Installation   
lib_PDF is based on the Apache PDFBox API and needs the PDFBox Jar fil to be present in Convertigo class path. This is automatically the case for Convertigo Version > 7.5. For 7.5 and lower versions you will have to install ther JAR file manually.

1. Downnload PDF Box Jar File [http://wwwftp.ciril.fr/pub/apache/pdfbox/2.0.11/pdfbox-app-2.0.11.jar](http://wwwftp.ciril.fr/pub/apache/pdfbox/2.0.11/pdfbox-app-2.0.11.jar "PDFBox")
1. For Convertigo Studio: UNZIP the jar file in <ConvertigoStudio Directory>/plugins/com.twinsoft.convertigo.studio_X.Y.z.vvvvvvvv/tomcat/webapps/convertigo/WEB-INF/classes
2. For Convertigo Server: copy the jar file in the <Convertigo Server>/tomcat/webapps/convertigo/lib directory

Then you import it in your Studio or deploy the lib_PDF.CAR project directly in the server.

## API
The project exposes 2 sequences

- getFieldsNames (Lists all the fields found in a PDF file)
	- input => tplPDF : the full path to a PDF form file
	- output => a list of all PDF form fields found in this PDF file
- fillFORM (Fills a form in a PDF file )
	- input => tplPDF : the full path to a PDF form file used a template
	- input => tgtPDF : the target PDF full path. A PDF file will be generated using the tplPDF template and the form data and placed in this path.
	- input => replacements : a JSON string containing an Array of {key: "key", value: "value", type: "type"} objects. Each key must be the name of a PDF form field and will be filled with the corresponding value. Types are ignored in this version.
	- output => none

The library will automatically find the field type in the form and set text or check the check boxes according to this type. 

The lib can also set images in the PDF. Images can be full paths to PNG or JPG files or be base64 strings.

## sample JSON string with images files.
  
	[{"key": "client_1", "value": "CLIENT1", "type": "text"}, {"key": "num_rapport", "value": "12345", "type": "text"}, {"key": "num_ot", "value": "00004", "type": "text"}, {"key": "contrat", "value": "1234567890", "type": "text"}, {"key": "check_lieu_chantier", "value": "true", "type": "checkbox"}, {"key": "num_info_1", "value": "1", "type": "text"}, {"key": "num_info_2", "value": "1", "type": "text"}, {"key": "num_info_3", "value": "1", "type": "text"}, {"key": "num_info_4", "value": "1", "type": "text"}, {"key": "num_info_5", "value": "1", "type": "text"}, {"key": "num_info_6", "value": "1", "type": "text"}, {"key": "num_info_7", "value": "1", "type": "text"}, {"key": "num_info_8", "value": "1", "type": "text"}, {"key": "compteur_depart", "value": "999999", "type": "text"},{"key": "sig_agence","value": "C:/Users/opic.TWINSOFT2K/wks7.6/pdf_Templates/sig_agence.png","type": "image"},{"key": "sig_client","value": "C:/Users/opic.TWINSOFT2K/wks7.6/pdf_Templates/sig_client.png","type": "image"}] 

## sample JSON string with base64 images

	[
    {
        "key": "client_1",
        "value": "CLIENT1",
        "type": "text"
    },
    {
        "key": "num_rapport",
        "value": "12345",
        "type": "text"
    },
    {
        "key": "num_ot",
        "value": "00004",
        "type": "text"
    },
    {
        "key": "contrat",
        "value": "1234567890",
        "type": "text"
    },
    {
        "key": "check_lieu_chantier",
        "value": "true",
        "type": "checkbox"
    },
    {
        "key": "num_info_1",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_2",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_3",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_4",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_5",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_6",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_7",
        "value": "1",
        "type": "text"
    },
    {
        "key": "num_info_8",
        "value": "1",
        "type": "text"
    },
    {
        "key": "compteur_depart",
        "value": "999999",
        "type": "text"
    },
    {
        "key": "sig_agence",
        "value": "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",
        "type": "image"
    },
    {
        "key": "sig_client",
        "value": "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",
        "type": "image"
    }
	]

## Preparing PDF templates

You can use any tool to create your PDF form templates but we found this Online Tool very useful [https://www.pdfescape.com/open/](https://www.pdfescape.com/open/ "PDF escape") Use the tool to create fields on any existing PDF file.

## Preparing for Images
If you want to insert images in the form, you will have to create images placeholders using fake PDF form submit buttons. Place the button anywhere on the page with the size and layout you want and give it a field name. The library will use this layout to insert and image at this exact location.

## sample PDF template
You can find a sample template in the projects data/mypdf.pdf file.


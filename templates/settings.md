# Settings

Open the template setting by clicking this ![](../.gitbook/assets/image11.png) icon when editing the template.

![](../.gitbook/assets/screenshot-localhost-8000-2019.08.27-04-48-55.png)

## Name 

The name and description are returned when fetching a list of all templates. The name is also shown in the template overview.

## Resource Identifier

The template may be specified by its id, which automatically generated, or by the reference which is specified in the `Resource Identifier` field. Each template must have a unique reference. You can swap the reference from one template to another \(unlike an id\).

## Locale

The locale specifies the number and date formatting and typically should match the document language. Currently only Dutch and English are supported.

You can transform a date or number to the locale by using:  
`x.localeDateFormat()` and `x.localeNumberFormat()`

## Font

A single font is used throughout the document. Any font that's available through [Google fonts](https://fonts.google.com/) may be selected.

## Header / Footer

Use one of the header / footers you as described in\#FillTheDoc UI. \(when generating the PDF\)

Note that the header and footer are not displayed when filling out the form or when getting the document as HTML.

## 




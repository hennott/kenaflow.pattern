# kenaflow can create an PDF
Nearly every digital process needs at the end an PDF/A which is stored mostly in an archive system. This is why kenaflow has a build in mechanism to create an PDF-file. Use the power of this solution combined with the TemplateEngine. You don´t need to install any dependencies.

## How To create an PDF
> `New-KFPDF -HTML <html> -AsStream`

example how to use this in the best way:
> `$document = (Invoke-KFTemplate -Template $config["tpl.Doc.Archive"])`
> `$pdfstream = New-KFPDF -HTML $document -AsStream`
> `Add-PnPFile -Folder "/archive_documents" -FileName "Protocol_$($item.ID).pdf" -Stream $pdfstream`
In this example we create an PDF based on a template and upload the file to a library.
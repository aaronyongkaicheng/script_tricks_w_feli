# script_tricks_w_feli

*Automate PDF printing*

Today, we are going to look into automating print files in PowerShell or Cygwin:

**Configuration printer selection**

1) To check default printer setup on your laptop:

```
$DefPrinter=Get-WmiObject -Query " SELECT * FROM Win32_Printer WHERE Default=$true"
Write-Output $DefPrinter
```

2) To check all the available printers:

```
$xgetPrinters=Get-WmiObject -Query " SELECT * FROM Win32_Printer" | Select Name
Write-Output $xgetPrinters
```

Therefore you could choose a particular printer name and set as your default:

```
$Printer_net = New-Object -COM WScript.Network
$Printer_net.SetDefaultPrinter("Printer_name_here")
```
**Get Printing**

1) Set your path to your folder directory that contains the PDFs:

```
$xpath="c:\path\here\"
```

Then run:

```
$folders=get-childitem $xpath | select Name
```

2) Run Printing:

```
foreach($pdf_files in $folders)
{
$PDF_file_name = $pdf_files.Name;

Start-Process $xpath$PDF_file_name -Verb Print
}
```



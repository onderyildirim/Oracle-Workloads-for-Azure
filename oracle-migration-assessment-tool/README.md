# Oracle Migration Assistant Tool

Oracle Migration Assistant (OMA) tool helps to understand resource usage on Oracle installations (on premise or in any cloud) and recommend the most suitable virtual machine that can run the same on Azure.

It works by processing Advanced Workload Repository (AWR) reports collected from the source system. Necessary information is extracted from AWR files and placed into an Excel workbook. For more information on different sections of workbook and the algorithm behind calculations see [AWR sizing document](/az-oracle-sizing/AWR%20Sizing%20Instructions.pdf).

OMA tool essentially automates steps defined in the [AWR sizing document](/az-oracle-sizing/AWR%20Sizing%20Instructions.pdf) to speed up the process and to relieve user from complexities of interpreting the AWR report. Below are description of each step it executes and output

* AWR files are processed from a single directory
* Data is extracted into an Excel file
* Most suitable VM size(s) is calculated and fetched for the Azure region given.
* The resulting Excel file is ready to use for further analysis and updates for fine tuning. For example, you can manually add another database by extracting data from its AWR file manually, change **calculation factors** or add/delete/modify recommended Azure VM sizes. See [AWR sizing document](/az-oracle-sizing/AWR%20Sizing%20Instructions.pdf) for more information on how to use the Excel file.

## Prerequisites and Limitations

Please review prerequisites and limitations of OMA tool before using it for your scenario

* PowerShell 5.1 or above is required
* Excel 2019 or above is required
* PowerShell core is not supported (due to COM dependencies)
* Only AWR Global (RAC) reports (created by running **awrgrpt.sql**) supported. In other words, regular AWR reports (created by running **awrrpt.sql**) are not supported.

## Usage

Usage: oma-tool.ps1 [OPTIONS]

OPTIONS:

   -h, Help          : Display this screen.
   
   -SourceFolder     : Source folder that contains AWR reports in HTML format. Default is '.' (current directory).
   
   -OutputFile       : Full path of the Excel file that will be created as output. Default is same name as SourceFolder directory name with XLSX extension under SourceFolder directory.
   
   -AzureRegion      : Name of the Azure region to be used when generating Azure resource recommendations. Default is 'westus'.
   
   -Debug            : Generates debug output.
   
SAMPLE:   
   oma-tool.ps1 -SourceFolder "C:\Reports" -AzureRegion westus

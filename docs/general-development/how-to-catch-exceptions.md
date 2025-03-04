---
title: Catch exceptions
description: You place the sections of code that might throw exceptions in a try block and place code that handles exceptions in a catch block. The order of catch statements is important. When an exception occurs, it is passed up the stack and each catch block is given the opportunity to handle it.
ms.date: 09/25/2017
keywords: errors,how to,howdoi,howto
f1_keywords:
- errors,how to,howdoi,howto
ms.prod: sharepoint
ms.assetid: de5fdb67-201b-4d7a-90a8-99ab7e51ea4e
ms.localizationpriority: medium
---


# Catch exceptions

You place the sections of code that might throw exceptions in a try block and place code that handles exceptions in a catch block. The order of catch statements is important. When an exception occurs, it is passed up the stack and each catch block is given the opportunity to handle it. The catch block that should handle the exception is determined by matching the type of the exception to the name of the exception specified in the catch block. For example, the following catch block catches Simple Object Access Protocol (SOAP) exceptions:
  
    
    


```csharp

catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Error Code: {0}", 
        e.SubCode.Code.Name);
    Console.WriteLine("SOAP Exception Message is: {0}", 
        e.Message);
}
```


```VB.net

Catch e As SoapException
    Console.WriteLine("SOAP Exception Error Code: {0}", e.SubCode.Code.Name)
    Console.WriteLine("SOAP Exception Message is: {0}", e.Message)
End Try
```

If no type-specific catch block exists, the exception is caught by a general catch block, if one exists. For example, you can catch general exceptions by adding the following code:


```csharp

catch (Exception e)
{
    Console.WriteLine("Exception Message: {0}", e.Message);
}
```




```VB.net

Catch e As Exception
    Console.WriteLine("Exception Message: {0}", e.Message)
End Try
```

You place catch blocks targeted to specific types of exceptions before a general exception. The common language runtime catches exceptions that are not caught by a catch block. Depending on how the runtime is configured, either a debug dialog box appears, or the program stops executing and a dialog box with exception information appears. For information about debugging, see  [Debugging and Profiling Applications](https://go.microsoft.com/fwlink/?LinkId=64641) (https://msdn.microsoft.com/library/default.asp?url=/library/cpguide/html/cpcondebuggingprofiling.asp).For more information about how to handle exceptions, see  [Best Practices for Handling Exceptions](https://go.microsoft.com/fwlink/?LinkId=64480) (https://msdn.microsoft.com/library/default.asp?url=/library/cpguide/html/cpconbestpracticesforhandlingexceptions.asp).
## Example


```csharp

using System;
using System.Text;
using System.Web.Services.Protocols;
using ExcelWebService.myserver02;
namespace ExcelWebService
{
    class WebService
    {
        [STAThread]
        static void Main(string[] args)
        {
            // Instantiate the Web service and make a status array object
            ExcelService xlservice = new ExcelService();
            Status[] outStatus;
            RangeCoordinates rangeCoordinates = new RangeCoordinates();
            string sheetName = "Sheet1";

            // Set the path to the workbook to open.
            // TODO: Change the path to the workbook
            // to point to a workbook you have access to.
            // The workbook must be in a trusted location.
            // If workbookPath is a UNC path, the application 
            // must be on the same computer as the server.
            // string targetWorkbookPath = 
            // @"\\\\MyServer\\myxlfiles\\Formulas.xlsx";
            string targetWorkbookPath = 
            "http://myserver02/DocLib/Shared%20Documents/Basic1.xlsx";
            // Set credentials for requests
            xlservice.Credentials = 
               System.Net.CredentialCache.DefaultCredentials;

            try
            {
                // Call the OpenWorkbook method and point to the 
                // trusted location of the workbook to open.
                string sessionId = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", out outStatus);
                Console.WriteLine("sessionID : {0}", sessionId);
                // Prepare object to define range coordinates, 
                // and call the GetRange method.
                rangeCoordinates.Column = 0;
                rangeCoordinates.Row = 0;
                rangeCoordinates.Height = 18;
                rangeCoordinates.Width = 10;

                object[] rangeResult1 = xlservice.GetRange(sessionId, sheetName, rangeCoordinates, false, out outStatus);
                Console.WriteLine("Total rows in range: " + rangeResult1.Length);

                Console.WriteLine("Sum in last column is: " + ((object[])rangeResult1[2])[3]);

               // Close the workbook. This also closes the session.
                xlservice.CloseWorkbook(sessionId);
            }
            catch (SoapException e)
            {
                Console.WriteLine("SOAP Exception Error Code: {0}", 
                    e.SubCode.Code.Name);
                Console.WriteLine("SOAP Exception Message is: {0}", 
                    e.Message);
            }

            catch (Exception e)
            {
                Console.WriteLine("Exception Message: {0}", e.Message);
            }
            Console.ReadLine();
        }
    }
}
```


```VB.net

Imports System
Imports System.Text
Imports System.Web.Services.Protocols
Imports ExcelWebService.myserver02
Namespace ExcelWebService
    Friend Class WebService
        <STAThread> _
        Shared Sub Main(ByVal args() As String)
            ' Instantiate the Web service and make a status array object
            Dim xlservice As New ExcelService()
            Dim outStatus() As Status
            Dim rangeCoordinates As New RangeCoordinates()
            Dim sheetName As String = "Sheet1"

            ' Set the path to the workbook to open.
            ' TODO: Change the path to the workbook
            ' to point to a workbook you have access to.
            ' The workbook must be in a trusted location.
            ' If workbookPath is a UNC path, the application 
            ' must be on the same computer as the server.
            ' string targetWorkbookPath = 
            ' @"\\\\MyServer\\myxlfiles\\Formulas.xlsx";
            Dim targetWorkbookPath As String = "http://myserver02/DocLib/Shared%20Documents/Basic1.xlsx"
            ' Set credentials for requests
            xlservice.Credentials = System.Net.CredentialCache.DefaultCredentials

            Try
                ' Call the OpenWorkbook method and point to the 
                ' trusted location of the workbook to open.
                Dim sessionId As String = xlservice.OpenWorkbook(targetWorkbookPath, "en-US", "en-US", outStatus)
                Console.WriteLine("sessionID : {0}", sessionId)
                ' Prepare object to define range coordinates, 
                ' and call the GetRange method.
                rangeCoordinates.Column = 0
                rangeCoordinates.Row = 0
                rangeCoordinates.Height = 18
                rangeCoordinates.Width = 10

                Dim rangeResult1() As Object = xlservice.GetRange(sessionId, sheetName, rangeCoordinates, False, outStatus)
                Console.WriteLine("Total rows in range: " &amp; rangeResult1.Length)

                Console.WriteLine("Sum in last column is: " &amp; (CType(rangeResult1(2), Object()))(3))

               ' Close the workbook. This also closes the session.
                xlservice.CloseWorkbook(sessionId)
            Catch e As SoapException
                Console.WriteLine("SOAP Exception Error Code: {0}", e.SubCode.Code.Name)
                Console.WriteLine("SOAP Exception Message is: {0}", e.Message)

            Catch e As Exception
                Console.WriteLine("Exception Message: {0}", e.Message)
            End Try
            Console.ReadLine()
        End Sub
    End Class
End Namespace
```


## See also


#### Tasks


  
    
    
 [How to: Trust a Location](how-to-trust-a-location.md)
  
    
    
 [How to: Save from Excel Client to the Server](how-to-save-from-excel-client-to-the-server.md)
  
    
    
 [How to: Use the SubCode Property to Capture Error Codes](how-to-use-the-subcode-property-to-capture-error-codes.md)
#### Concepts


  
    
    
 [Accessing the SOAP API](accessing-the-soap-api.md)
  
    
    
 [Excel Services Alerts](excel-services-alerts.md)
  
    
    
 [Excel Services Known Issues and Tips](excel-services-known-issues-and-tips.md)
  
    
    
 [Loop-Back SOAP Calls and Direct Linking](loop-back-soap-calls-and-direct-linking.md)
#### Other resources


  
    
    
 [Walkthrough: Developing a Custom Application Using Excel Web Services](walkthrough-developing-a-custom-application-using-excel-web-services.md)

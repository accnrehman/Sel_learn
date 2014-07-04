

--------------------------------------------------------------------------
Macro Running Part : Module 1 code...
---------------------------------------------------------------------------
Sub FileSize()

Dim oFS, oFolder
Dim objexcel, r, lnameArray, lname, nameLength
Set oFS = CreateObject("Scripting.FileSystemObject")
'Path = "" & ThisWorkbook.Worksheets("Instructions").Cells(1, 2) & ""

Dim fldr As FileDialog
Dim sItem As String
Dim path As String

Set fldr = Application.FileDialog(msoFileDialogFolderPicker)

With fldr
    .Title = "Select a Folder"
    .AllowMultiSelect = False
    '.InitialFileName = strPath
    If .Show <> -1 Then GoTo NextCode
    sItem = .SelectedItems(1)
End With



NextCode:
path = sItem
Set fldr = Nothing

On Error GoTo Finally

Set oFolder = oFS.GetFolder(path)

Application.Visible = True


r = 2

Call ShowFolderDetails(oFolder)


MsgBox "Done"

Finally:


End Sub

 

'Public Function ShowFolderDetails(oF, r, ExtTypes, Flag)
Public Function ShowFolderDetails(oF)
Dim F
Dim filename
Dim SheetFlag As Boolean
'ThisWorkbook.Worksheets("FileSize").Cells(r, 1).Value = oF.Name

If oF.Files.Count <> 0 Then
             
        
        Set filename = oF.Files
            For Each folderIdx In filename
            
                If LCase(GetType(folderIdx.Name)) = "xlsx" Or _
                    LCase(GetType(folderIdx.Name)) = "xlsm" Or _
                    LCase(GetType(folderIdx.Name)) = "xls" Or _
                    LCase(GetType(folderIdx.Name)) = "xlsb" Then
                    
                    SheetFlag = False
                    Workbooks.Open folderIdx.path
                    Workbooks(folderIdx.Name).Activate
                    
                    For i = 1 To Workbooks(folderIdx.Name).Worksheets.Count
                    
                        If Workbooks(folderIdx.Name).Worksheets(i).Name = "Confidential" Then
                        
                            SheetFlag = True
                            Exit For
                        
                        Else
                        
                            SheetFlag = False
                        
                        End If
                                    
                    Next
                    
                    
                    If SheetFlag = False Then
                        
                         Application.DisplayAlerts = False
                         Workbooks(folderIdx.Name).Worksheets.Add().Name = "Confidential"
                         Workbooks(folderIdx.Name).Sheets("Confidential").Range("D10") = "Confidential"
                         Workbooks(folderIdx.Name).Sheets("Confidential").Range("D10").Font.Size = 20
                         Workbooks(folderIdx.Name).Sheets("Confidential").Range("D10").Font.Bold = True
                         Workbooks(folderIdx.Name).Sheets("Confidential").Activate
                         Workbooks(folderIdx.Name).Save
                         Workbooks(folderIdx.Name).Close
                         Application.DisplayAlerts = True
                    
                    Else
                        Application.DisplayAlerts = False
                        LRandomNumber = Int((300 - 200 + 1) * Rnd + 200)
                        Workbooks(folderIdx.Name).Worksheets.Add().Name = "Confidential_" & LRandomNumber
                        Workbooks(folderIdx.Name).Sheets("Confidential_" & LRandomNumber).Range("D10") = "Confidential"
                        Workbooks(folderIdx.Name).Sheets("Confidential_" & LRandomNumber).Range("D10").Font.Size = 20
                        Workbooks(folderIdx.Name).Sheets("Confidential_" & LRandomNumber).Range("D10").Font.Bold = True
                        Workbooks(folderIdx.Name).Sheets("Confidential_" & LRandomNumber).Activate
                        Workbooks(folderIdx.Name).Save
                        Workbooks(folderIdx.Name).Close
                        Application.DisplayAlerts = True
                        
                    
                    End If
                
                End If
            Next
            
 
   
End If


For Each F In oF.Subfolders
' Call ShowFolderDetails(F, r, ExtTypes, Flag)
    Call ShowFolderDetails(F)
Next
End Function

Public Function GetType(FileNm)

    FileType = Split(FileNm, ".", -1, 1)
    GetType = FileType(UBound(FileType))

End Function


Public Function RowsCount(ShName, ColIndex)

    r = 0
    
    For i = 1 To Rows.Count
    
        If Worksheets(ShName).Cells(i, ColIndex) <> "" Then
        
            r = r + 1
            
            
        Else
        
            Exit For
        
        End If
        
    Next
    
    RowsCount = r
        
End Function





----------------------------------------------------------------------------------
package testNGRuchita;
import java.io.IOException;

import org.apache.poi.openxml4j.exceptions.InvalidFormatException;
import org.testng.annotations.Test;

import frameworkpractice.Mettl;

public class MettlTest {
 Mettl mt = new Mettl();
  @Test
  public void TC_01() throws InvalidFormatException, IOException 
  {
	
	 mt.navigatetoURL();
	 
  }
  @Test
  public void TC_02() throws InvalidFormatException, IOException
  {
	 
	  mt.registermettl();
	  
  }
  @Test
  public void TC_03() throws InvalidFormatException, IOException
  {
	 
	  mt.Login();
	  
  }
  
}
---------------------------------
package frameworkpractice;

import java.io.IOException;

import org.apache.poi.openxml4j.exceptions.InvalidFormatException;
import org.openqa.selenium.By;
import org.openqa.selenium.support.ui.Select;

import GenericLibrary.CommomUtill;
import GenericLibrary.Driver;
import GenericLibrary.ExcelLib;

public class Mettl 
{
	
	ExcelLib lib =new ExcelLib();
	

	CommomUtill cutil= new CommomUtill();
	 public void navigatetoURL() throws InvalidFormatException, IOException
	 {
		 
		 String url= lib.getExcelData("Sheet2", 1, 2); 
		 Driver.driver.get(url);
				 
	 }
	 public void registermettl() throws InvalidFormatException, IOException
	 {
		
		 Driver.driver.findElement(By.id("free-trail")).click();
		    cutil.waitForPageLoad();
		    
		 String email= lib.getExcelData("Sheet2", 2, 5);
		 String password= lib.getExcelData("Sheet2", 2, 4);
		 String name= lib.getExcelData("Sheet2", 2, 3);
		 String mobile= lib.getExcelData("Sheet2", 2,6);
		 String organisation= lib.getExcelData("Sheet2", 2, 7);
		 
		 
		  Driver.driver.findElement(By.id("signup-email")).sendKeys(email); 
		 Driver.driver.findElement(By.id("signup-password")).sendKeys(password); 
		 Driver.driver.findElement(By.id("signup-firstName")).sendKeys(name); 
		 Driver.driver.findElement(By.id("signup-phoneNumber")).sendKeys(mobile); 
		 Driver.driver.findElement(By.id("signup-organisation")).sendKeys(organisation); 
		 
		 
		 Select st=new Select(Driver.driver.findElement(By.id("signup-purpose")));
		 st.selectByIndex(1);
		 
		 Driver.driver.findElement(By.id("signup")).click();
		 
	 }

}
------------------------------------------
package com.GenericLibrary;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

public class CommomUtill 
{
	public void waitForPageLoad()
	{
		Driver.driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
	}
	public void waitForElementPresent(String xpath)
	{
		WebDriverWait wait=new WebDriverWait(Driver.driver,10);
		wait.until(ExpectedConditions.elementToBeClickable(By.xpath(xpath)));	
	}
	public void waitForLinkPresent(String linkText)
	{
		WebDriverWait wait=new WebDriverWait(Driver.driver,10);
		wait.until(ExpectedConditions.elementToBeClickable(By.xpath(linkText)));	
	}
	public Boolean verifyTextPresent(String expectedText)
	{
		boolean b= true;
		String entirePageSource= Driver.driver.getPageSource();
		if(entirePageSource.contains(expectedText))
		{
			b=true;
			System.out.println("found");
		}
		else
		{
			b= false;
			System.out.println(" not found");
		}
		return b;
	}
	public boolean verifyTextofTheElemt(String xpath,String expText)
	{
		boolean b =false;
		 String  actText=Driver.driver.findElement(By.xpath(xpath)).getText();
		if(actText.equals(expText))
		{
			b= true;
		}
		else
		{
			b=false;
		}
		return b;	
	}
	public void verifyElementprsent(String xpath) throws InterruptedException
	{
		int i=0;
		boolean flag=false;
		while(i<10)
		{
			try{
			Driver.driver.findElement(By.xpath(xpath));
		   flag=true;
		   break;
			}
			catch(Throwable e)
			{
				Thread.sleep(2000);
				i= i+1;
			}
		}
	}
	

}
-------------------------------------------

package GenericLibrary;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;

public static class Driver 
{
	public static WebDriver driver= new FirefoxDriver();


}

-------------------------------------------------

package com.GenericLibrary;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

import org.apache.poi.openxml4j.exceptions.InvalidFormatException;
import org.apache.poi.ss.usermodel.Cell;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Workbook;
import org.apache.poi.ss.usermodel.WorkbookFactory;

public class ExcelLib 
{
	public String excelFilePath="C:\\Users\\Ruchita\\Desktop\\Book1.xlsx";
	public String getExcelData(String sheetName,int rowNo,int colNo) throws InvalidFormatException, IOException
	{
	FileInputStream file= new FileInputStream(excelFilePath);
	Workbook wb= WorkbookFactory.create(file);
	Sheet sh= wb.getSheet(sheetName);
	Row rw =sh.getRow(rowNo);
	Cell cel=rw.getCell(colNo);
	
	return cel.getStringCellValue(); 
	}
	public void setExcelData(String sheetName,int rowNo,int colNo,String message) throws InvalidFormatException, IOException
	{
		FileInputStream file= new FileInputStream(excelFilePath);
		Workbook wb= WorkbookFactory.create(file);
		Sheet sh= wb.getSheet(sheetName);
		Row rw =sh.getRow(rowNo);
		Cell cel=rw.getCell(colNo);
		cel.setCellType(cel.CELL_TYPE_STRING);
		cel.setCellValue(message);
		FileOutputStream fos= new FileOutputStream(excelFilePath);
		wb.write(fos);
	}
	public int  getRowExcel(String sheetName ) throws InvalidFormatException, IOException 
	{
		FileInputStream file= new FileInputStream(excelFilePath);
		Workbook wb= WorkbookFactory.create(file);
		Sheet sh= wb.getSheet(sheetName);
		return sh.getLastRowNum();
		
		
	}

}

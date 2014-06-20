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

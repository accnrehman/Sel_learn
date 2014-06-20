
package com.qspider.frameworkpractice;

import java.io.IOException;

import org.apache.poi.openxml4j.exceptions.InvalidFormatException;
import org.openqa.selenium.By;

import com.qspider.GenericLibrary.CommomUtill;
import com.qspider.GenericLibrary.Driver;
import com.qspider.GenericLibrary.ExcelLib;

public class LoginActiTime {

	
	public static void main(String[] args) throws InvalidFormatException, IOException 
	{
	  Driver.driver.get("http://127.0.0.1/login.do");
	   String title= Driver.driver.getTitle();
	   ExcelLib elib = new ExcelLib();
	   CommomUtill cutil= new CommomUtill();
	   cutil.verifyTextPresent("Username:" );
	   elib.setExcelData("Sheet1", 1, 4, title);  
	   String uname =elib.getExcelData("Sheet1", 1, 2);
	   String pwd =elib.getExcelData("Sheet1", 1, 3);
	   
	   Driver.driver.findElement(By.xpath("//input[@type='text']")).sendKeys(uname);
	   Driver.driver.findElement(By.xpath("//input[@type='password']")).sendKeys(pwd);
	   Driver.driver.findElement(By.xpath("//input[@type='submit']")).click();
       Boolean b=cutil.verifyTextofTheElemt("//td[text()='AABB1']", "AABB1");
	   System.out.println(b);
	}
}

package com.qspider.frameworkpractice;

import java.io.IOException;

import org.apache.poi.openxml4j.exceptions.InvalidFormatException;
import org.openqa.selenium.By;
import org.openqa.selenium.support.ui.Select;

import com.qspider.GenericLibrary.CommomUtill;
import com.qspider.GenericLibrary.Driver;
import com.qspider.GenericLibrary.ExcelLib;

public class Mettle 
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
package com.qspider.GenericLibrary;

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
package com.qspider.GenericLibrary;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;

public class Driver 
{
	public static WebDriver driver= new FirefoxDriver();
	

}
package com.qspider.GenericLibrary;

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
	public String excelFilePath="C:\\Users\\Sahir\\Desktop\\Book1.xlsx";
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
package com.qspider.testNGabdur;

import java.io.IOException;

import org.apache.poi.openxml4j.exceptions.InvalidFormatException;
import org.testng.annotations.Test;

import com.qspider.frameworkpractice.Mettle;

public class MettlTest {
 Mettle mt = new Mettle();
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
  
}




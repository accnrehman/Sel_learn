


import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.FileWriter;
import java.io.IOException;
import java.util.NoSuchElementException;
import java.util.concurrent.TimeUnit;

import jxl.Cell;
import jxl.Sheet;
import jxl.Workbook;

import org.apache.commons.io.FileUtils;
import org.apache.poi.hssf.usermodel.HSSFCell;
import org.apache.poi.hssf.usermodel.HSSFRow;
import org.apache.poi.hssf.usermodel.HSSFSheet;
import org.apache.poi.hssf.usermodel.HSSFWorkbook;
import org.junit.Assert;
import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.Point;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.ie.InternetExplorerDriver;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.support.ui.Select;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

public class AchE2EFlow

{
	private static WebDriver driver;
	static int i = 1;
	static int j = 2;
	static int k = 15;

		static String FilePath = "C:\\Users\\s.nageswararao\\Desktop\\File System\\Cpo_Data_Adv.xls";
		static String Sheet = "Ach";
		static String Flag = "Pass";
	
	
	   @Test(description="Navigation to different browsers according to input data")
	   public static void OpenBrowser(String Xpath,String Url) throws Exception
	   {
		  
		   switch(Xpath)
		   	{
		   		case "Firefox":
			   					driver = new FirefoxDriver();
			   					//String baseUrl = "https://cashproonline-preprod.bankofamerica.com";
			   					driver.manage().window().maximize();
			   					driver.get(Url);
			   					qspCreateLogFile();
			   					break;
		   		case "ie":   
				   				DesiredCapabilities capabilities = DesiredCapabilities.internetExplorer();
				   				//capabilities.setCapability(CapabilityType.UNEXPECTED_ALERT_BEHAVIOUR,"Ignore");
				   				capabilities.setCapability(InternetExplorerDriver.INTRODUCE_FLAKINESS_BY_IGNORING_SECURITY_DOMAINS, true);
				            
				   				File file = new File("C:\\Users\\s.nageswararao\\Desktop\\IEDriverServer.exe");
				   				System.setProperty("webdriver.ie.driver", file.getAbsolutePath());
				   				driver = new InternetExplorerDriver(capabilities);
				   				driver.get(Url);
				   				Thread.sleep(15000);
				   				driver.manage().window().maximize();  
				   				qspCreateLogFile();
				   				break;
			   			
			   			
		   		case "chrome":
		   						file = new File("C:\\Users\\s.nageswararao\\Desktop\\chromedriver_win_26.0.1383.0\\chromedriver.exe");
		   						System.setProperty("webdriver.chrome.driver", file.getAbsolutePath());
		   						driver=new ChromeDriver();
		   						//Thread.sleep(15000);
		   						driver.manage().window().maximize();  
		   						driver.get(Url);
		   						qspCreateLogFile();
		   						break;
			   			
		   		default:
			   					System.out.println("Browser Not found");
		   }
	   }
	
	// To read the Values from Excel sheet and stores in dataprovider	
	   @DataProvider(name = "dataProvider")
	   	public static Object[][] CreatTable() throws Exception
	   	{
		   Object[][] retObjArr=getTableArray("C:\\Users\\s.nageswararao\\Desktop\\File System\\Cpo_Data_Adv.xls","Ach","RegressionTestData");
				return(retObjArr);
	     
	   	}
	
	

	@SuppressWarnings("deprecation")
	@Test (dataProvider = "dataProvider")
	   
	   public void testCpo(String ScreenName, String Keywords, String Url, String ObjProperty,String Xpath,String Xpath1,String Value,String Window, String Applicable, String DefaultFrame,String Frame1,String Frame2,String Frame3,String Frame4,String Result,String PageValidation) throws Exception
	   {
		   		
			if(Keywords.equals("OpenBrowser"))
			{
					OpenBrowser(Xpath,Url);
			}
					
		   	if(Keywords.equals("EnterText"))
			{
		   		EnterText(ScreenName,Keywords,Url,ObjProperty,Xpath,Xpath1,Value,Window,Applicable,DefaultFrame,Frame1,Frame2,Frame3,Frame4,Result,PageValidation);			
		   				   		
			}
			
			
			if(Keywords.equals("ClickButton"))
			{
		   		ClickButton(ScreenName,Keywords,Url,ObjProperty,Xpath,Xpath1,Value,Window,Applicable,DefaultFrame,Frame1,Frame2,Frame3,Frame4,Result,PageValidation);
		   				
		   		
			}
			if(Keywords.equals("ClickMenu"))
			{
				
				ClickMenu(ScreenName,Keywords,Url,ObjProperty,Xpath,Xpath1,Value,Window,Applicable,DefaultFrame,Frame1,Frame2,Frame3,Frame4,Result,PageValidation);
			}
			
			if(Keywords.equals("SelectCheckbox"))
			{
				
				SelectCheckbox(ScreenName,Keywords,Url,ObjProperty,Xpath,Xpath1,Value,Window,Applicable,DefaultFrame,Frame1,Frame2,Frame3,Frame4,Result,PageValidation);
			}
			if(Keywords.equals("ClickLink"))
			{
				
				ClickLink(ScreenName,Keywords,Url,ObjProperty,Xpath,Xpath1,Value,Window,Applicable,DefaultFrame,Frame1,Frame2,Frame3,Frame4,Result,PageValidation);
			}
			if(Keywords.equals("AnswerChallegeQ"))
			{
				
				AnswerChallegeQ();
			}
			
			
		/*
			if(ObjectID.equals(""))
			System.out.println("Object Not found");
			if(ObjectID.equals("id"))
			xyposid(Xpath);
			if(ObjectID.equals("css"))
			xyposcss(Xpath);*/
			
				
		/* Code for Drop down objects
			if(Type.equals("Dropdown"))
			{
				driver.switchTo().window(Window);
				WebElement drop; 
				drop=driver.findElement(By.id(Xpath));
			    driver.manage().timeouts().implicitlyWait(4, TimeUnit.SECONDS);
			    drop.click();
			    Select dropchat = new Select(drop);
			    driver.manage().timeouts().implicitlyWait(4, TimeUnit.SECONDS);
			    dropchat.selectByVisibleText(Xpath1);
			    Thread.sleep(5000);
			    screenCaptureFF(); 

			}
			*/
			
			// Code for Login to Cpo Application till Home page
				
			
		     
//Close of Testcpo method
 }
		   	
		 	  
	 @Test(description="Enter data into text boxes and validates textbox UI validation")
	   public static void EnterText(String ScreenName, String Keywords, String Url,String ObjProperty,String Xpath,String Xpath1,String Value,String Window, String Applicable,String DefaultFrame, String Frame1,String Frame2,String Frame3,String Frame4,String Result,String PageValidation) throws Exception
	   {
		   try
	   		{
	   			
	   		if(Applicable.equals("Yes"))
	   			
	   			
	   		//qspWriteDesignStep("Text Box Verification is applicable");
	   				if(driver.findElement(By.id(Xpath)).isEnabled()==true)
	   				{
			   			writeToExcel(FilePath, Sheet, Flag);
			   			String page1="page is displayed successfully";
			   			String page=ScreenName+" "+page1;
			   			writeToExcelpage(FilePath, Sheet, page);
						WebElement element = driver.findElement(By.id(Xpath));
						//driver.manage().timeouts().implicitlyWait(05, TimeUnit.SECONDS);
						element.sendKeys(Value);
						screenCaptureFF();
								
	   			}
	   		else
	   			
	   			{
			   			Flag="Fail";
			   			String page2="page is not displayed successfully";
			   			String pagefail=ScreenName+" "+page2;
		   				//qspWriteFailLog("The textbox \""+Name+"\" is disabled");
		   				writeToExcel(FilePath, Sheet, Flag);
		   				writeToExcelpage(FilePath, Sheet, pagefail);
		   				
	   				//qspWriteFailLog("The textbox \""+Name+"\" is disabled");
	   			}
				
	   		}catch(NoSuchElementException nsee)
	   			{
	   					System.out.println(nsee.toString()); 

	   			}
	   }
	   
	   @Test(description="click each button and validates button UI validation")
	   public static void ClickButton(String ScreenName, String Keywords, String Url, String ObjProperty,String Xpath,String Xpath1,String Value,String Window, String Applicable,String DefaultFrame, String Frame1,String Frame2,String Frame3,String Frame4,String Result,String PageValidation) throws Exception
	   {
		   try
	   		{
	   			
	   		if(Applicable.equals("Yes"))
	   		{
	   			
	   			if((!Frame1.isEmpty())&&(!Frame2.isEmpty())&(!Frame3.isEmpty()))
	   			{
	   		//qspWriteDesignStep("Text Box Verification is applicable");
	   				if(driver.findElement(By.id(Xpath)).isEnabled()==true)
	   				{
	   					driver.switchTo().frame(Frame1);
	   					driver.switchTo().frame(Frame2);
			   			writeToExcel(FilePath, Sheet, Flag);
			   			String page1="page is displayed successfully";
			   			String page=ScreenName+" "+page1;
			   			writeToExcelpage(FilePath, Sheet, page);
			   			
						WebElement element = driver.findElement(By.id(Xpath));
						//driver.manage().timeouts().implicitlyWait(05, TimeUnit.SECONDS);
						element.click();
						screenCaptureFF();
		   											
	   				}
	   				else
	   				{
	   					Flag="Fail";
			   			String page2="page is not displayed successfully";
			   			String pagefail=ScreenName+" "+page2;
		   				//qspWriteFailLog("The textbox \""+Name+"\" is disabled");
		   				writeToExcel(FilePath, Sheet, Flag);
		   				writeToExcelpage(FilePath, Sheet, pagefail);
	   				}
	   			}
	   			else
	   				{
		   				writeToExcel(FilePath, Sheet, Flag);
			   			String page1="page is displayed successfully";
			   			String page=ScreenName+" "+page1;
			   			writeToExcelpage(FilePath, Sheet, page);
			   			
						WebElement element = driver.findElement(By.id(Xpath));
						//driver.manage().timeouts().implicitlyWait(05, TimeUnit.SECONDS);
						element.click();
						screenCaptureFF();
	   				}
	   			
	   		}
	   		
	   		}catch(NoSuchElementException nsee)
	   			{
	   				System.out.println(nsee.toString()); 

	   			}
		   
	   	}
	   @Test(description="Clicks each Main menus ans sub menu items")
	   public static void ClickMenu(String ScreenName, String Keywords, String Url,String ObjProperty, String Xpath,String Xpath1,String Value,String Window, String Applicable,String DefaultFrame, String Frame1,String Frame2,String Frame3,String Frame4,String Result,String PageValidation) throws Exception
	   {
		   try{	
			   
			  if((Frame1.isEmpty())&&(Frame2.isEmpty()))
			    
			  	 {  
				  	Thread.sleep(15000);
			  		WebElement element = driver.findElement(By.cssSelector(Xpath));
			  		element.click();
			  		//Thread.sleep(10000);
			  		element = driver.findElement(By.cssSelector(Xpath1));
					screenCaptureFF();
					element.click();
					}
			  
			  else if((!Frame1.isEmpty())&&(Frame2.isEmpty()))
				  
			  	{
				  if(DefaultFrame.equals("Yes"))
					  
				   {
					  	Thread.sleep(15000);
					  	driver.manage().timeouts().implicitlyWait(4, TimeUnit.SECONDS);
						driver.switchTo().defaultContent();
						driver.switchTo().frame(Frame1);
					  	WebElement element = driver.findElement(By.cssSelector(Xpath));
				  		element.click();
				  		//Thread.sleep(10000);
				  		element = driver.findElement(By.cssSelector(Xpath1));
						screenCaptureFF();
						element.click();
				   }
				  else
					  
				  	{
					  	Thread.sleep(15000);
					  	driver.switchTo().frame(Frame1);
				  		WebElement element = driver.findElement(By.cssSelector(Xpath));
				  		element.click();
				  		//Thread.sleep(10000);
				  		element = driver.findElement(By.cssSelector(Xpath1));
				  		screenCaptureFF();
				  		element.click();
				  	}
			  	}
			  else if((Frame1.isEmpty())&&(!Frame2.isEmpty()))
			  {
					  	Thread.sleep(15000);
					  	driver.switchTo().frame(Frame2);
					  	WebElement element = driver.findElement(By.cssSelector(Xpath));
				  		element.click();
				  		//Thread.sleep(10000);
				  		element = driver.findElement(By.cssSelector(Xpath1));
						screenCaptureFF();
						element.click();
			  }
			  else
			  {
				  if(ObjProperty.equals("Id"))
				  {
						Thread.sleep(15000); 	
						driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
					  	driver.switchTo().frame(Frame1);
					  	driver.switchTo().frame(Frame2);
					  	WebElement element = driver.findElement(By.id(Xpath));
				  		element.click();
				  		//Thread.sleep(10000);
			  		
				  }
				  else
				  {
					  	Thread.sleep(15000);
					  	driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
					  	driver.switchTo().frame(Frame1);
					  	driver.switchTo().frame(Frame2);
					  	WebElement element = driver.findElement(By.cssSelector(Xpath));
				  		element.click();
				  		//Thread.sleep(10000);
				  		element = driver.findElement(By.cssSelector(Xpath1));
						screenCaptureFF();
						element.click();
						element.click();
					  
				  }
			  }
		   	}catch(NoSuchElementException nsee)
			   		{
			   			System.out.println(nsee.toString()); 

			   		}
				
					
	   }

		@Test
		 public static void SelectCheckbox(String ScreenName, String Keywords, String Url,String ObjProperty, String Xpath,String Xpath1,String Value,String Window, String Applicable,String DefaultFrame, String Frame1,String Frame2,String Frame3,String Frame4,String Result,String PageValidation) throws Exception
		   {
			try{	
				   
				  if((Frame1.isEmpty())&&(Frame2.isEmpty())&&(Frame3.isEmpty()))
				    
				  	 {  
				  		if(ObjProperty.equals("Name"))
				  		{
				  			WebElement element = driver.findElement(By.name(Xpath));
				  			element.click();
				  			screenCaptureFF();
				  		//Thread.sleep(10000);
				  		
						}
				  		else
				  		{
				  			WebElement element = driver.findElement(By.id(Xpath));
				  			element.click();
				  			screenCaptureFF();
				  		//Thread.sleep(10000);
				  		}
				  		
				  	 }  else if((Frame3.isEmpty())&&(!Frame1.isEmpty())&&(!Frame2.isEmpty()))
				  		 
				  	{
				  		if(ObjProperty.equals("name"))
				  			
					  	{
				  			driver.switchTo().frame(Frame1);
						  	driver.switchTo().frame(Frame2);
						  	WebElement element = driver.findElement(By.name(Xpath));
						  	element.click();
						  	screenCaptureFF();
					  	}
				  		else
				  			{
				  				driver.switchTo().frame(Frame1);
				  				driver.switchTo().frame(Frame2);
				  				WebElement element = driver.findElement(By.id(Xpath));
				  				element.click();
				  				screenCaptureFF();
						  	//Thread.sleep(10000);
				  			}
				  		
				  	}
				  	 else 
				  	 {	
					  
				  		 if(ObjProperty.equals("name"))
				  			
					  	{
						  	driver.switchTo().defaultContent();
						  	driver.switchTo().frame(Frame1);
						  	driver.switchTo().frame(Frame2);
						  	driver.switchTo().frame(Frame3);
						  	WebElement element = driver.findElement(By.name(Xpath));
						  	element.click();
						  	screenCaptureFF();
					  	}
				  		else
				  			{
				  				driver.switchTo().defaultContent();
				  				driver.switchTo().frame(Frame1);
				  				driver.switchTo().frame(Frame2);
				  				driver.switchTo().frame(Frame3);
				  				WebElement element = driver.findElement(By.id(Xpath));
				  				element.click();
				  				screenCaptureFF();
						  	//Thread.sleep(10000);
				  			}
				  		
				  }
				  
			   	}
						catch(NoSuchElementException nsee)
				   		{
				   			System.out.println(nsee.toString()); 

				   		}
					
						
		   }
		@Test
		 public static void ClickLink(String ScreenName, String Keywords, String Url,String ObjProperty, String Xpath,String Xpath1,String Value,String Window, String Applicable,String DefaultFrame, String Frame1,String Frame2,String Frame3,String Frame4,String Result,String PageValidation) throws Exception
		   {
			   try{	
				   
				   if((Frame1.isEmpty())&&(Frame2.isEmpty())&&(Frame3.isEmpty()))
				    
				  	 {  
				  		WebElement element = driver.findElement(By.linkText(Xpath));
				  		element.click();
				  		screenCaptureFF();
				  		//Thread.sleep(10000);
				  		
					}
				   else 
					 {
					   if(DefaultFrame.equals("Yes"))
					   	{
						   	driver.switchTo().defaultContent();
						   	driver.switchTo().frame(Frame1);
						   	driver.switchTo().frame(Frame2);
						   	driver.switchTo().frame(Frame3);
						  	WebElement element = driver.findElement(By.linkText(Xpath));
					  		element.click();
					  		screenCaptureFF();
					   }
					   	else
					   	{
					   		driver.switchTo().frame(Frame1);
						   	driver.switchTo().frame(Frame2);
						   	driver.switchTo().frame(Frame3);
						  	WebElement element = driver.findElement(By.linkText(Xpath));
					  		element.click();
					  		screenCaptureFF();
				  		
					   }
					 }
				   
				   
			   }catch(NoSuchElementException nsee)
				   		{
				   			System.out.println(nsee.toString()); 

				   		}
					
						
		   }
	@Test		
	 private static void exit() {
		// TODO Auto-generated method stub
		
	}

	
	@Test 
	public static void AnswerChallegeQ()
	{
			Point x;
			Dimension y;
			int j;
		     String s= "?";
		     String m = null;
		     String q1,q2,q3;
		     WebElement element = driver.findElement(By.id("answerChallengeQuestions:challengeQuestionsText1"));
		     q1=element.getText();
		     element = driver.findElement(By.id("answerChallengeQuestions:challengeQuestionsText2"));
		     q2=element.getText();
		     element = driver.findElement(By.id("answerChallengeQuestions:challengeQuestionsText3"));
		     q3=element.getText();
		     //System.out.println(q1);
		    // System.out.println(q2);
		    // System.out.println(q3);
		     String[] q7 = q1.split(" ");
		     for(j=0;j<q7.length;j++)
		     {
		    	 String[] a = q7[j].split("");
		    	 		 
		    	 for(int b=0;b<a.length;b++) 		 
		    	 	{
		    		  if(a[b].compareTo(s)==0)
		    			 {
		    				 m=q7[j];
		    			     exit();
		    			 }
		    		}
		    	if(m!=null)
				System.out.println(m);
		     }
		     String q8 = q7[q7.length - 1];
		     //System.out.println(q8); 
		     String str=removeLastChar(q8);
		     //System.out.println(str); 
		     String[] q9 = q2.split(" ");
		     String q10 = q9[q9.length - 1];
		     //System.out.println(q8); 
		     String q11=removeLastChar(q10);
		    // System.out.println(q11); 
		     String[] q12 = q3.split(" ");
		     String q13 = q12[q12.length - 1];
		     //System.out.println(q8); 
		     String q14=removeLastChar(q13);
		     //System.out.println(q14); 
		     driver.manage().timeouts().implicitlyWait(20, TimeUnit.SECONDS);
		     screenCaptureFF();
		     element = driver.findElement(By.id("answerChallengeQuestions:answerPasswordBox1"));
		     x= element.getLocation();
			 System.out.println("Location of the Object" +"answerChallengeQuestions:answerPasswordBox1"+ " "+ x);
			 y=element.getSize();
			 System.out.println("Size of the Object" +"answerChallengeQuestions:answerPasswordBox1"+" "+ y);
		     element.sendKeys(str);
		     element = driver.findElement(By.id("answerChallengeQuestions:answerPasswordBox2"));
		     x= element.getLocation();
			 System.out.println("Location of the Object" +"answerChallengeQuestions:answerPasswordBox2"+" "+ x);
			 y=element.getSize();
			 System.out.println("Size of the Object" +"answerChallengeQuestions:answerPasswordBox2" + " "+y);
		     element.sendKeys(q11);
		     element = driver.findElement(By.id("answerChallengeQuestions:answerPasswordBox3"));
		     x= element.getLocation();
			 System.out.println("Location of the Object" +"answerChallengeQuestions:answerPasswordBox3"+ " "+ x);
			 y=element.getSize();
			 System.out.println("Size of the Object" +"answerChallengeQuestions:answerPasswordBox3"+ " "+y);
		     element.sendKeys(q14);
     
		}

	@Test
	public static String[][] getTableArray(String xlFilePath, String sheetName, String tableName){
		    String[][] tabArray=null;
		    try{
		        
		    	Workbook workbook = Workbook.getWorkbook(new File(xlFilePath));
		        Sheet sheet = workbook.getSheet(sheetName);
		        int startRow,startCol, endRow, endCol,ci,cj;
		        Cell tableStart=sheet.findCell(tableName);
		        startRow=tableStart.getRow();
		        startCol=tableStart.getColumn();

		        Cell tableEnd= sheet.findCell(tableName, startCol+1,startRow+1, 100, 64000,  false);
		  

		        endRow=tableEnd.getRow();
		        endCol=tableEnd.getColumn();
		        Cell a=sheet.findCell(tableName,3,4,100,64000,true);
		        System.out.println(a);
		        System.out.println("startRow="+startRow+", endRow="+endRow+", " +"startCol="+startCol+", endCol="+endCol);
		        tabArray=new String[endRow-startRow-1][endCol-startCol-1];
		        ci=0;

		        for (int i=startRow+1;i<endRow;i++,ci++){
		            cj=0;
		            for (int j=startCol+1;j<endCol;j++,cj++){
		                tabArray[ci][cj]=sheet.getCell(j,i).getContents();
		            }
		        }
		    }
		    catch (Exception e)    {
		        System.out.println("error in getTableArray()");
		    }

		    return(tabArray);
		}
	  

	/*@Test
		public void xyposid(String Xpath) throws Exception
	{
		WebElement element;
		Point x;
		Dimension y;
		element = driver.findElement(By.id(Xpath));
    	x= element.getLocation();
    	System.out.println("Location of the Object" + x);
    	y=element.getSize();
    	System.out.println("Size of the Object" + y);
    			
	}
	@Test
	public void xyposcss(String Xpath) throws Exception
{
	WebElement element;
	Point x;
	Dimension y;
	element = driver.findElement(By.cssSelector(Xpath));
	x= element.getLocation();
	System.out.println("Location of the Object" + x);
	y=element.getSize();
	System.out.println("Size of the Object" + y);
			
}*/
	   @Test
		//Method to remove last character of a word
	   private static String removeLastChar(String str) 
	   {
	   			return str.substring(0,str.length()-1);
	   	}
	   
	   
	   // Method to take screenshots
	   @Test
	   public static void screenCaptureFF()
	   {

	   File screenshot	=	((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
	   try
	   {
	   	FileUtils.copyFile(screenshot, new File("C:\\Users\\s.nageswararao\\Desktop\\CPO_Screenshot\\LiveChat"+i+".png"));
	   	
	   }
	   catch(IOException e){
	   	e.printStackTrace();
	   }
	   i++;
	   }
	
	  @Test
	  
	  public static void writeToExcel(String FilePath, String Sheet, String result) throws Exception
		
		
		{
			
					try{
						FileInputStream testdatastream = new FileInputStream(FilePath);  
						HSSFWorkbook wb = new HSSFWorkbook();
						wb = new HSSFWorkbook(testdatastream);  
					
						//HSSFSheet ws = wb.createSheet(Sheet); 
						HSSFSheet ws = wb.getSheet(Sheet);

					
						HSSFRow row = ws.getRow(j);
						HSSFCell cell = row.createCell(k);
						cell.setCellValue(result);
						testdatastream.close();
						FileOutputStream fileOut = new FileOutputStream(FilePath); 

						wb.write(fileOut);  
						fileOut.close();
						k++;
						//j++;
						
					}
	
					catch(Exception e)
					{
						e.printStackTrace();
					}
		}
	  
	  public static void writeToExcelpage(String FilePath, String Sheet, String result) throws Exception
		
		
		{
			
					try{
						FileInputStream testdatastream = new FileInputStream(FilePath);  
						HSSFWorkbook wb = new HSSFWorkbook();
						wb = new HSSFWorkbook(testdatastream);  
					
						//HSSFSheet ws = wb.createSheet(Sheet); 
						HSSFSheet ws = wb.getSheet(Sheet);

					
						HSSFRow row = ws.getRow(j);
						HSSFCell cell = row.createCell(k);
						cell.setCellValue(result);
						testdatastream.close();
						FileOutputStream fileOut = new FileOutputStream(FilePath); 

						wb.write(fileOut);  
						fileOut.close();
						k--;
						j++;
						//k++;
					}
	
					catch(Exception e)
					{
						e.printStackTrace();
					}		}
	   @AfterClass
	    public void tearDown() throws Exception{
	    	//qspCompleteLogFile();
	    	
	       // driver.close();
	       
	    } 
	   
	   //Function definition to create the result file
	    public static void qspCreateLogFile() throws Exception{        

	    	BufferedWriter b = new BufferedWriter(new FileWriter("C:\\Users\\s.nageswararao\\Desktop\\test-output\\"+"CPO_Report"+".htm"));
	    	b.write("<html><head><title>"+"CPO Application Report"+"</title></head>");   
	    	b.write("<body><table border='1'><tr bgcolor='#A2B5CD'><td>Currently Executing:</td><td>"+"CPO UI Status Report"+"</td></tr></table>");      
	    	b.write("<table border='1'><tr bgcolor='#A2B5CD'><td><b>Description</b></td><td><b>Result</b></td></tr>");
	    	b.close();

	    }
	       
		
	    
	    //Function definition to write the heading in the result file
	    public static void qspWriteHeading(String desc, String PageTitle) throws Exception{

	    	BufferedWriter b = new BufferedWriter(new FileWriter("C:\\Users\\s.nageswararao\\Desktop\\test-output\\"+"CPO_Report"+".htm",true));
	    	b.write("<tr bgcolor='#AFEEEE'><td><b>Page:"+PageTitle+": "+desc+"</b></td></tr>");
	    	b.close();
	    }
	    
	
	    
	    //Function definition to write the design steps in the result file
	    public static void qspWriteDesignStep(String desc) throws Exception{

	    	BufferedWriter b = new BufferedWriter(new FileWriter("C:\\Users\\s.nageswararao\\Desktop\\test-output\\"+"CPO_Report"+".htm",true));
	    	b.write("<tr bgcolor='#E0EEEE'><td><b>"+desc+"</b></td></tr>");
	    	b.close();
	    }

	    //Function definition to write the pass results in the result file
	    public static void qspWritePassLog(String desc) throws Exception{

	    	BufferedWriter b = new BufferedWriter(new FileWriter("C:\\Users\\s.nageswararao\\Desktop\\test-output\\"+"CPO_Report"+".htm",true));
	    	b.write("<tr><td>"+desc+"</td><td bgcolor='#00FF00'>PASS</td></tr>");
	    	b.close();
	    }

	    //Function definition to write the fail results in the result file
	    public static void qspWriteFailLog(String desc) throws Exception{
	    	BufferedWriter b = new BufferedWriter(new FileWriter("C:\\Users\\s.nageswararao\\Desktop\\test-output\\"+"CPO_Report"+".htm",true));
	    	b.write("<tr><td>"+desc+"</td><td bgcolor='#FF0000'>Fail</td></tr>");
	    	b.close();
	    }   
	    
	  
	    //Function definition to complete the result file
	    public void qspCompleteLogFile() throws Exception{
	    	BufferedWriter b = new BufferedWriter(new FileWriter("C:\\Users\\s.nageswararao\\Desktop\\test-output\\"+"CPO_Report"+".htm",true));
	    	b.write("</html>");
	    	b.close();
	    }
	   }

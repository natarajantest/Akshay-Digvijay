# Akshay Babu Gawali(Q5387)
#Digvijay Sawant(Q5388)
#HospitalApp
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
package package2;

import java.time.Duration;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;

import javafx.scene.control.Alert;

public class HospitalApp {

	public static void main(String[] args) throws InterruptedException {
		WebDriver driver = new ChromeDriver();
		WebDriverWait wait = new WebDriverWait(driver,300);
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
		driver.get("http://demo.openemr.io/d/openemr/interface/login/login.php?site=default");
		//Username
		driver.findElement(By.id("authUser")).sendKeys("admin");
		//password
		driver.findElement(By.id("clearPass")).sendKeys("pass");
		//Login Button
		driver.findElement(By.xpath("//button[@class='btn btn-default btn-lg']")).click();
		//patient/client
		driver.findElement(By.xpath("//div[@class='menuSection']")).click();
		//New/search
		Actions act  = new Actions(driver);
		act.moveToElement(driver.findElement(By.xpath("//div[text()='Patient/Client']"))).build().perform();
		act
		.keyDown(Keys.CONTROL)
		.pause(Duration.ofSeconds(1))
		.build()
		.perform();
		driver.findElement(By.xpath("//div[text()='New/Search']")).click();
		driver.switchTo().frame(driver.findElement(By.name("pat")));
		//FirstName
		driver.findElement(By.xpath("//input[@class='form-control']")).sendKeys("Akshay");
		//LastName
		driver.findElement(By.name("form_lname")).sendKeys("Gawali");

		//Date
		driver.findElement(By.id("form_DOB")).sendKeys("2019-04-17");
		//Sex
		Select sex=new Select(driver.findElement(By.name("form_sex")));
		sex.selectByIndex(2);
		//FirstName
		driver.findElement(By.xpath("//input[@class='form-control']")).sendKeys("Akshay");
		//Click on Create new patient
		driver.findElement(By.id("create")).click();

		//confirm new patient
		driver.switchTo().defaultContent();
		driver.switchTo().frame(driver.findElement(By.id("modalframe")));
		driver.findElement(By.xpath("//input[@value='Confirm Create New Patient']")).click();
		//Alert
		Thread.sleep(5000);
		driver.switchTo().alert().accept();

		//Happy birthday
		driver.findElement(By.xpath("//div[@class='closeDlgIframe']")).click();
		Thread.sleep(5000);
		//Billy smith
		driver.findElement(By.id("username")).click();
		//logout
		act.moveToElement(driver.findElement(By.xpath("//div[@class='menuSection userSection']"))).build().perform();
		driver.findElement(By.xpath("//ul//li[text()='Logout']")).click();

	}

}


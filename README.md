

import java.io.File;
import java.io.FileNotFoundException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Scanner;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.support.ui.ExpectedCondition;
import org.openqa.selenium.support.ui.WebDriverWait;

/**
 *
 * @author S530945
 */
public class SeleniumPHP {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) throws FileNotFoundException, InterruptedException {

        Scanner sc = new Scanner(new File("Input.txt"));
        PrintWriter pout = new PrintWriter(new File("output.txt"));
        String inputNameField = "";
        String inputNumber1 = "";
        String incidentName = "";
        String incidentLocation = "";
        String incidentDescription = "";
        String searchName = "";
        String searchNameInReport = "";
        while (sc.hasNext()) {
            inputNameField = sc.nextLine();
            inputNumber1 = sc.nextLine();
            incidentName = sc.nextLine();
            incidentLocation = sc.nextLine();
            incidentDescription = sc.nextLine();
            searchName = sc.nextLine();
            searchNameInReport = sc.nextLine();
            System.out.println(inputNameField + " " + inputNumber1 + " " + incidentName + "" + incidentLocation + " " + incidentDescription + " " + searchName);
            pout.println(inputNameField + " " + inputNumber1 + " " + incidentName + "" + incidentLocation + " " + incidentDescription + " " + searchName);
            System.setProperty("webdriver.chrome.driver", "C:\\Software\\chromedriver.exe");
//Initialize variable for chrome driver
            WebDriver driver = new ChromeDriver();
            // to maximize the Chrome Browser 
            driver.manage().window().maximize();
            driver.get("https://drrs.herokuapp.com/#/login ");
            driver.findElement(By.xpath("//*[@id=\"mat-input-0\"]")).sendKeys(inputNameField);
            Thread.sleep(2000);
            driver.findElement(By.xpath("//*[@id=\"mat-input-1\"]")).sendKeys(inputNumber1);

            driver.findElement(By.xpath("/html/body/app-root/div/app-login/div[3]/mat-card/mat-card-content/form/button/span")).click();
            Thread.sleep(2000);

            // clicking ok on the notification when login is successfull
            driver.findElement(By.xpath("//*[@id=\"mat-dialog-0\"]/app-logindialog/mat-card/mat-card-content/button")).click();
            Thread.sleep(2000);
            String previousURL = driver.getCurrentUrl();
//        Login Page Validation //System.out.println(previousURL);
            if (previousURL.equalsIgnoreCase("https://drrs.herokuapp.com/#/dashboard")) {
                System.out.println("Login user  ==  Pass");
                pout.println("Login user  ==  Pass");
            } else {
                System.out.println("Login user  ==  Fail");
                pout.println("Login user  ==  Fail");
            }
            //driver.navigate().to("https://drrs.herokuapp.com/#/dashboard");
            Thread.sleep(2000);
            driver.findElement(By.xpath("/html/body/app-root/div/app-dashboard/div/div[1]/div[1]/button/span")).click();;
            Thread.sleep(2000);

            String previousURL2 = driver.getCurrentUrl();
//        System.out.println(previousURL);
            if (previousURL2.equalsIgnoreCase("https://drrs.herokuapp.com/#/createIncident")) {
                System.out.println("Created Incident  ==  Pass");
                pout.println("Created Incident  ==  Pass");
            } else {
                System.out.println("Created Incident  ==  Fail");
                pout.println("Created Incident  ==  Fail");
            }
            //driver.navigate().to("https://drrs.herokuapp.com/#/createIncident");
            Thread.sleep(2000);

            driver.findElement(By.xpath("//*[@id=\"inputincidentName\"]")).sendKeys(incidentName);
            Thread.sleep(2000);
            driver.findElement(By.xpath("//*[@id=\"inputlocation\"]")).sendKeys(incidentLocation);
            Thread.sleep(2000);
            driver.findElement(By.xpath("//*[@id=\"inputdescription\"]")).sendKeys(incidentDescription);
            Thread.sleep(2000);
            driver.findElement(By.xpath("/html/body/app-root/div/app-create-incident/div[2]/form/div[2]/button[1]/span")).click();
            Thread.sleep(2000);
            driver.findElement(By.xpath("//*[@id=\"mat-dialog-1\"]/app-incidentsuccessful/mat-card/mat-card-content/button")).click();
            Thread.sleep(2000);
            //clicking on review application
            driver.findElement(By.xpath("/html/body/app-root/div/app-dashboard/mat-toolbar/a[2]")).click();
            Thread.sleep(2000);

            //Test case for navigating to archived list
            String previousURL4 = driver.getCurrentUrl();
            if (previousURL2.equalsIgnoreCase("https://drrs.herokuapp.com/#/createIncident")) {
                System.out.println("Navigated to the archived list  ==  Pass");
                pout.println("Navigated to the archived list  ==  Pass");
            } else {
                System.out.println("Navigated to the archived list  ==  Fail");
                pout.println("Navigated to the archived list  ==  Fail");
            }

            // Searching the name of the person 
            driver.findElement(By.xpath("//*[@id=\"mat-input-2\"]")).sendKeys(searchName);
            Thread.sleep(2000);

            String previousURL5 = driver.getCurrentUrl();

            if (previousURL2.equalsIgnoreCase("https://drrs.herokuapp.com/#/createIncident")) {
                System.out.println("Entered the name to be searched  ==  Pass");
                pout.println("Entered the name to be searched  ==  Pass");
            } else {
                System.out.println("Entered the name to be searched  ==  Fail");
                pout.println("Entered the name to be searched  ==  Fail");
            }

            // Navigating to the Common operating pictute and checking weather it has navigated to the proper page or not
            driver.findElement(By.xpath("/html/body/app-root/div/app-review-application/mat-toolbar/a[3]")).click();
            Thread.sleep(2000);

            String previousURL6 = driver.getCurrentUrl();
            if (previousURL2.equalsIgnoreCase("https://drrs.herokuapp.com/#/createIncident")) {
                System.out.println("Navigating to Common Operating Picture  ==  Pass");
                pout.println("Navigating to Common Operating Picture  ==  Pass");
            } else {
                System.out.println("Navigating to Common Operating Picture  ==  Fail");
                pout.println("Navigating to Common Operating Picture  ==  Fail");
            }

            //Navigating back to the dashboard and validating it wheather it has moved to particular page or not
            driver.findElement(By.xpath("/html/body/app-root/div/app-cop/mat-toolbar/a[1]")).click();
            Thread.sleep(2000);

            String previousURL7 = driver.getCurrentUrl();

            if (previousURL2.equalsIgnoreCase("https://drrs.herokuapp.com/#/cop")) {
                System.out.println("Navigating to Dashboard  ==  Pass");
                pout.println("Navigating to Dashboard  ==  Pass");
            } else {
                System.out.println("Navigating to Dashboard  ==  Fail");
                pout.println("Navigating to Dashboard  ==  Fail");
            }

            //Navigating to the report page
            driver.findElement(By.xpath("/html/body/app-root/div/app-dashboard/div/div[2]/div[1]/div/mat-card/mat-card-actions/button[1]")).click();
            Thread.sleep(2000);
            //Searching the reports by report submitted person name
            driver.findElement(By.xpath("//*[@id=\"mat-input-3\"]")).sendKeys(searchNameInReport);
            Thread.sleep(2000);

            //Navigating back to the dashboard
            driver.findElement(By.xpath("/html/body/app-root/div/app-report/mat-toolbar/a[1]")).click();
            Thread.sleep(2000);

            //navigating to archived incidents
            driver.findElement(By.xpath("//html/body/app-root/div/app-dashboard/div/div[1]/div[2]/button")).click();
            Thread.sleep(2000);
            // Clicking on the download option in the archived incidents page to download the list of archived incidents
            driver.findElement(By.xpath("/html/body/app-root/div/app-archived-incidents/div/div[3]/div/a")).click();
            Thread.sleep(2000);
            driver.navigate().to("https://drrs.herokuapp.com/#/dashboard");
            Thread.sleep(2000);

            // Clicking on logoff button and checking weather it is logging of successfully or not       
            driver.findElement(By.xpath("/html/body/app-root/div/app-dashboard/mat-toolbar/a[4]")).click();;
            Thread.sleep(2000);
            String previousURL9 = driver.getCurrentUrl();
            if (previousURL2.equalsIgnoreCase("https://drrs.herokuapp.com/#/dashboard")) {
                System.out.println("Logging out of application  ==  Pass");
                pout.println("Logging out of application  ==  Pass");
            } else {
                System.out.println("Logging out of application  ==  Fail");
                pout.println("Logging out of application  ==  Fail");
            }

            pout.close();
        }
    }
} 

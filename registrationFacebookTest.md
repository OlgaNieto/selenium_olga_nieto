import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.Select;
import org.testng.annotations.Test;

import java.util.List;

import static java.lang.Thread.sleep;

public class registrationFacebookTest {
    @Test
    public void fullRegistrationTest() throws InterruptedException {
        System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe");
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.facebook.com/");

        // Crear una nueva cuenta. Hacer clic en  crear cuenta nueva
        driver.findElement(By.linkText("Crear cuenta nueva")).click();
        // Espera mientras la pantalla se carga
        sleep(2000);

        // Diligencia la información
        registrarDatos("firstname", "John", driver);
        registrarDatos("lastname", "Smith", driver);
        registrarDatos("reg_email__", "5555555", driver);
        registrarDatos("reg_passwd__", "123456789", driver);

        // Registra la fecha de nacimiento
        // Para ingresar el día
        WebElement elementoDias = driver.findElement(By.name("birthday_day"));
        Select dias = new Select(elementoDias);
        dias.selectByValue("26");
        // Para ingresar el mes
        WebElement elementoMeses = driver.findElement(By.name("birthday_month"));
        Select meses = new Select(elementoMeses);
        meses.selectByVisibleText("jun");
        // Para ingresar el año
        WebElement elementoAnios = driver.findElement(By.name("birthday_year"));
        Select anios = new Select(elementoAnios);
        anios.selectByIndex(41);

        // Seleccionar el sexo Hombre, de acuerdo con lo encontrado es Mujer (0), Hombre (1), P (3)
        seleccionarGenero(1, driver);

        // Espero un tiempo para visualizar la información
        sleep(2000);
        // Cierra el explorador
        driver.close();
    }
    //Este es el método para ingresar los datos
    public static void registrarDatos(String campoRellenar, String valorCampo, WebDriver driver) {
        driver.findElement(By.name(campoRellenar)).sendKeys(valorCampo);
    }

    public static void seleccionarGenero(int pos, WebDriver driver) {
        List<WebElement> listaGenero = driver.findElements(By.name("sex"));
        WebElement generoRadiobutton = listaGenero.get(pos);
        generoRadiobutton.click();
    }

}

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.Select;
import org.testng.annotations.Test;

import java.util.List;

import static java.lang.Thread.sleep;

public class SpotifyWithCssSelectorTest {

    @Test
    public void spotifyByPlaceHolderTest() throws InterruptedException {
        System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe");
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.spotify.com/uy/signup/");

        // Llamo el método para cargar cada uno los datos
        rellenarCampo("input[placeholder='Introduce tu correo electrónico.']","prueba@prueba.com", driver);
        rellenarCampo("input[placeholder='Vuelve a introducir tu correo electrónico.']","prueba@prueba.com", driver);
        rellenarCampo("input[placeholder='Crea una contraseña.']","123456", driver);
        rellenarCampo("input[placeholder='Introduce un nombre de perfil.']","Olga", driver);
        rellenarCampo("input[placeholder='DD']","12", driver);
        rellenarCampo("input[placeholder='AAAA']","1997", driver);

        //Tomo la lista de meses
        WebElement listaMeses = driver.findElement(By.cssSelector("select[name='month']"));
        Select mesSelect = new Select(listaMeses);
        //Cargo el mes de nacimiento
        mesSelect.selectByValue("09");

        // Selecciona el género femenino
        driver.findElement(By.xpath("//div[@class='Radio-tr5kfi-0 dYEnUC'][2]")).click();

        // Selecciono la opción de Prefiero no recibir publicidad de Spotify.
        // Al hacerlo con click genera un error, por eso la quite
        //driver.findElement(By.cssSelector("input[name='marketing']")).click();
        sleep(2000);
        driver.close();

    }

    // Método para rellenar un campo de un formulario
    public static void rellenarCampo(String detalleCampo, String valorCampo, WebDriver driver) {
        // Creo la lista de acuerdo con el tipo de elemento
        driver.findElement(By.cssSelector(detalleCampo)).sendKeys(valorCampo);
    }

}

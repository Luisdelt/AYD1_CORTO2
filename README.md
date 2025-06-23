# Nombre: Luis Carlos de León Torón
# Carnet: 202212535

Imagen corriendo en el puerto 3000

![image](https://github.com/user-attachments/assets/55fcf494-0003-4a41-97b9-b1f4da58afcd)

![image](https://github.com/user-attachments/assets/da92e7a3-620c-469e-9b43-0e3b22b138e2)


Pruebas E2E

![image](https://github.com/user-attachments/assets/291b48cb-7814-4f39-a94f-d702bb2aa80c)

![image](https://github.com/user-attachments/assets/20d070bc-59d6-4d50-a61a-84ce9b95f9a5)

![image](https://github.com/user-attachments/assets/8eb3331b-a64a-47e8-8859-e9ddb1f16400)


```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service as ChromeService
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from webdriver_manager.chrome import ChromeDriverManager
import os
import time

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
wait = WebDriverWait(driver, 10)

try:
    driver.get("http://localhost:3000") 
    print("[INFO]: Página cargada.")

    wait.until(EC.visibility_of_element_located((By.XPATH, "//h2[contains(text(),'Datos del Conductor')]")))

    driver.find_element(By.NAME, "nombre").send_keys("Análisis")
    driver.find_element(By.NAME, "apellido").send_keys("Diseño")
    driver.find_element(By.NAME, "email").send_keys("ayd1@usac.edu.gt")
    driver.find_element(By.NAME, "pass").send_keys("LuisAYD1")

    genero_select = driver.find_element(By.NAME, "genero")
    for option in genero_select.find_elements(By.TAG_NAME, "option"):
        if option.text.strip().lower() == "Masculino":
            option.click()
            break

    driver.find_element(By.NAME, "fecha_nacimiento").send_keys("01-08-2001")

    driver.find_element(By.NAME, "direccion").send_keys("Ciudad universitaria zona 12, Ciudad de Guatemala")

    print("[INFO]: Formulario completado.")

    boton_registro = driver.find_element(By.XPATH, "//button[contains(text(),'Registrarse')]")
    boton_registro.click()
    print("[INFO]: Formulario enviado.")

    time.sleep(2)

except Exception as e:
    print(f"[ERROR]: {e}")
finally:
    time.sleep(3) 
    driver.quit()
```

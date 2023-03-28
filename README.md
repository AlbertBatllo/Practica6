# Practica6: Busos de comunicació II (SPI)

L'objectiu de la pràctica és comprendre el funcionament del bus spi

## Codi

```
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>

File myFile;

void setup()
{
  Serial.begin(115200);
  Serial.print("Iniciando SD ...");
  if (!SD.begin(5)) {
    Serial.println("No se pudo inicializar");
    return;
  }
  Serial.println("inicializacion exitosa");
 
  myFile = SD.open("/archivo.txt");//abrimos  el archivo 
  if (myFile) {
    Serial.println("archivo.txt:");
    while (myFile.available()) {
    	Serial.write(myFile.read());
    }
    myFile.close(); //cerramos el archivo
  } else {
    Serial.println("Error al abrir el archivo");
  }
}

void loop()
{
  
}
```
## Explicació del codi

Per aquesta pràctcia són necessaries dues llibreries: 'SPI.h' per gestionar el bus SPI, i 'SD.h' per el lector lector de targetes:

```
#include <SPI.h>
#include <SD.h>
```

Declararem un objecte "File" que serà l'arxiu on es carregarà el fitxer de la SD amb el que treballarem:

```
File myFile;
```
**Set Up:**

Primer s'inicialitzarà la SD, mentres es mostrarà per pantalla "Iniciando SD ...", en cas de que no es pugui inicialitzar correctament es mostararà per pantalla "No se pudo inicializar" i es finalitzarà el procés. Per altra banda, si es pot inicialitzar correctament es mostrarà per pantalla "inicializacion exitosa" i es continuarà amb el procés:

```
void setup()
{
  Serial.begin(115200);
  Serial.print("Iniciando SD ...");
  if (!SD.begin(5)) {
    Serial.println("No se pudo inicializar");
    return;
  }
  Serial.println("inicializacion exitosa");
```
Un cop establerta la conexió, carreguem el fitxer de text "parchivo.txt" al objecte "myFile" creat anteriorment. A continuació s'executarà una funció if que revisarà si s'ha pogut carregar el fitxer correctament. En cas afirmatiu es mostrarà el contingut a traves de la terminal i, un cop acabat, tancarà el fitxer. En càs negatiu es mostrarà per pantalla "Error al abrir el archivo":

 ```
  myFile = SD.open("/archivo.txt");//abrimos  el archivo 
  if (myFile) {
    Serial.println("archivo.txt:");
    while (myFile.available()) {
    	Serial.write(myFile.read());
    }
    myFile.close(); //cerramos el archivo
  } else {
    Serial.println("Error al abrir el archivo");
  }
}
```

**Loop:**
```
void loop()
{
  
}



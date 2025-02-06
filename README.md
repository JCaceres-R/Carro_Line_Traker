# Carro Seguidor de Línea con Raspberry Pi Pico W

Este proyecto implementa un carro seguidor de línea utilizando una Raspberry Pi Pico W y una cámara OV7670. El sistema captura imágenes, las procesa para detectar una línea en la pista y utiliza un algoritmo de ponderación en tres renglones para calcular el centro relativo de la línea, lo que permite ajustar la dirección del carro.

## Descripción

El proyecto se basa en el siguiente funcionamiento:
- **Captura de Imagen:** La cámara OV7670 captura una imagen en una resolución reducida (dividida por 16) y en formato YUV para facilitar el procesamiento.
- **Procesamiento y Umbralización:** Se convierte la imagen a un formato binario aplicando un umbral de luminancia. Los píxeles con luminancia menor o igual a un valor predefinido se consideran negros y los que están por encima, blancos.
- **Selección de Renglones y Ponderación:** Se seleccionan tres renglones específicos (fila central, una fila arriba y una fila abajo) para analizar la posición de la línea. Cada píxel en estas filas se pondera según su posición horizontal respecto al centro de la imagen. El algoritmo calcula un valor promedio que indica el desplazamiento de la línea.
- **Control de Motores:** Con base en la posición detectada, el algoritmo ajusta la velocidad de los motores para corregir la dirección del carro, permitiendo que siga la línea de forma continua.

## Integrantes del Proyecto

- **Edwin Arbey Valbuena Gamboa** - 20211005129
- **Paula Andrea Chaparro Sánchez** – 20211005008
- **Johan Sebastian Caceres Rodriguez** - 20212005111

## Requisitos

- **Hardware:**
  - Raspberry Pi Pico W
  - Cámara OV7670
  - LEDs y motores conectados a los pines GPIO según el diseño del circuito
- **Software:**
  - CircuitPython (o MicroPython) instalado en la Raspberry Pi Pico W
  - Biblioteca `adafruit_ov7670` y otras dependencias (como `digitalio`, `busio`, `pwmio` y `board`)

## Instalación y Configuración

1. **Configurar la Raspberry Pi Pico W:**  
   Instala CircuitPython en la placa siguiendo la documentación oficial.

2. **Conectar el Hardware:**  
   - Conecta la cámara OV7670 a los pines especificados en el código.
   - Asegura que los LEDs y los motores estén correctamente conectados a los pines indicados.

3. **Instalar las Bibliotecas Necesarias:**  
   Descarga e instala la biblioteca `adafruit_ov7670` y verifica que estén disponibles las dependencias requeridas.

4. **Cargar el Código:**  
   Copia el script principal en la memoria de la Raspberry Pi Pico W.

## Uso

1. **Alimentación:** Conecta la Raspberry Pi Pico W a una fuente de alimentación adecuada.
2. **Ejecución:** Inicia el script. El sistema comenzará a capturar imágenes, procesarlas y ajustar los motores en función del algoritmo de ponderación.
3. **Observación:** Podrás monitorear la salida a través del puerto serial, donde se mostrarán mensajes indicando la dirección (izquierda, derecha o derecho) según la posición detectada de la línea.

## Estructura del Código

El código se organiza en las siguientes secciones:

- **Configuración de Hardware:**  
  Inicialización de LEDs, motores y la cámara (con definición de pines y parámetros de configuración).

- **Captura y Procesamiento de Imagen:**  
  La cámara captura la imagen y se extraen tres renglones específicos para analizar la línea.

- **Algoritmo de Ponderación:**  
  Se realiza una suma ponderada de los píxeles de cada renglón para calcular el centro relativo de la línea. La fórmula es:
  \[
  \text{centro} = \frac{\sum (\text{peso} \times \text{valor del píxel})}{\sum (\text{valor del píxel})}
  \]
  donde el peso es la distancia del píxel al centro de la imagen.

- **Control de Motores:**  
  Dependiendo del valor promedio obtenido, se ajustan los motores para girar hacia la dirección correcta (izquierda o derecha) o para continuar en línea recta.

## Contribución

Este proyecto es fruto del trabajo colaborativo de los integrantes mencionados. Cada miembro aportó en diferentes áreas: diseño del algoritmo, implementación del hardware, programación del software y pruebas del sistema.

## Licencia

Este proyecto es de código abierto y se distribuye bajo la [MIT License](LICENSE).

## Contacto

Para dudas, sugerencias o colaboraciones, por favor, contacta a alguno de los integrantes del equipo.


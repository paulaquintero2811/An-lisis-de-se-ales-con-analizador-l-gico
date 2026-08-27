# Análisis de señales con analizador lógico

## Descripción

En este laboratorio se analizó una comunicación serial UART generada mediante una Raspberry Pi Pico 2W, utilizando un analizador lógico y el software Logic 2.

Se realizaron mediciones del tiempo de bit para diferentes tasas de transmisión y frecuencias de muestreo, comparando los resultados experimentales con los valores teóricos obtenidos a partir de la tasa de baudios.

También se analizó el efecto de la frecuencia de muestreo sobre la resolución temporal de la señal y sobre la correcta decodificación de los datos transmitidos.

## Objetivos

- Comprobar la relación entre el tiempo de bit y la tasa de transmisión.
- Analizar las características de una comunicación serial UART.
- Identificar los diferentes elementos de una trama UART.
- Comprender el funcionamiento de un analizador lógico.
- Evaluar el efecto de la frecuencia de muestreo sobre la medición del tiempo de bit.
- Comparar los valores teóricos y experimentales obtenidos durante las mediciones.

## Hardware utilizado

- Raspberry Pi Pico 2W
- Analizador lógico
- Computador

## Software utilizado

- MicroPython
- Logic 2
- Thonny

## Configuración inicial

La Raspberry Pi Pico 2W fue configurada para transmitir datos mediante UART utilizando:

- Baudrate: 9600 baudios
- Bits de datos: 8
- Paridad: Ninguna
- Bits de parada: 1

El canal 0 del analizador lógico se conectó al pin TX de la Raspberry Pi Pico 2W y la referencia GND del analizador al GND del microcontrolador. :contentReference[oaicite:1]{index=1}

## Análisis de la señal UART

Inicialmente se transmitió periódicamente el carácter `U`. Mediante Logic 2 se capturó la señal y se analizaron sus diferentes representaciones en formato:

- Binario
- Decimal
- Hexadecimal
- ASCII

Para una transmisión de 9600 baudios, el tiempo teórico de un bit es aproximadamente **104,16 µs**. Experimentalmente se obtuvo un valor cercano a **104 µs**, mostrando una buena correspondencia entre ambos valores. :contentReference[oaicite:2]{index=2}

También se analizó la duración de una trama UART. Con 8 bits de datos, 1 bit de inicio y 1 bit de parada, cada carácter está compuesto por 10 bits, obteniéndose un tiempo teórico aproximado de **1,041 ms**. :contentReference[oaicite:3]{index=3}

## Transmisión de mensajes

Se transmitió el mensaje:

`UMNG_2026_LIDER_EN_TELECOMUNICACIONES`

El mensaje contiene 37 caracteres. Con una configuración de 10 bits por carácter y una velocidad de 9600 baudios, el tiempo teórico de transmisión fue aproximadamente **38,54 ms**. :contentReference[oaicite:4]{index=4}

Posteriormente se agregó un bit de paridad impar, aumentando la cantidad de bits por carácter a 11. Esto incrementó el tiempo teórico de transmisión del mensaje a aproximadamente **42,39 ms**. :contentReference[oaicite:5]{index=5}

## Análisis de la frecuencia de muestreo

Se evaluaron diferentes tasas de transmisión:

- 1200 baudios
- 9600 baudios
- 57600 baudios
- 115200 baudios

También se utilizaron diferentes frecuencias de muestreo, desde **25 kS/s hasta 24 MS/s**.

Se calculó el número de muestras por bit mediante:

`N = fs / fB`

Como criterio práctico se utilizó un mínimo de **10 muestras por bit** para obtener una representación adecuada de la señal. :contentReference[oaicite:6]{index=6}

Los resultados mostraron que, a medida que aumenta la tasa de baudios, disminuye el tiempo de bit y se necesita una mayor frecuencia de muestreo para obtener suficientes muestras por bit. :contentReference[oaicite:7]{index=7}

## Casos de error

Se analizaron casos en los que la frecuencia de muestreo no fue suficiente para realizar una correcta decodificación.

Por ejemplo:

- **57600 baudios a 25 kS/s:** se obtuvieron aproximadamente 0,434 muestras por bit y el carácter `M` no fue decodificado correctamente.
- **115200 baudios a 50 kS/s:** también se obtuvieron aproximadamente 0,434 muestras por bit y se presentó un error de paridad durante la decodificación. :contentReference[oaicite:8]{index=8}

Estos resultados demostraron que una frecuencia de muestreo demasiado baja puede dificultar la identificación de las transiciones de la señal y producir errores en la información recibida.

## Resultados principales

El laboratorio permitió comprobar experimentalmente que:

- El tiempo de bit disminuye cuando aumenta la tasa de baudios.
- Una mayor frecuencia de muestreo proporciona una mejor resolución temporal.
- El número de muestras por bit influye en la precisión de las mediciones.
- Una cantidad insuficiente de muestras por bit puede provocar errores de decodificación.
- La configuración de la trama UART influye directamente en el tiempo total de transmisión.
- Un mínimo aproximado de 10 muestras por bit permitió obtener mediciones más confiables. :contentReference[oaicite:9]{index=9}

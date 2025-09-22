# Laboratorio 2 - Convolucion y transformada de fourier

**Universidad Militar Nueva Granada**

**Asignatura:** Procesamiento Digital de Señales

**Estudiantes:** Dubrasca Martinez, Mariana Leyton, Maria Fernanda Castellanos

**Fecha:** 21 de septiembre de 2025

**Título de la práctica:** Convolucion, transformada y estadisticos descriptivos de la señal EOG.

# **Objetivos**
- Comprender la convolución como una operación que permite obtener la respuesta de un sistema discreto ante una entrada determinada.
- Analizar la correlación como medida de similitud entre dos señales.
- Aplicar la Transformada de Fourier como herramienta de análisis en el dominio de la frecuencia.
- Caracterizar estadísticamente señales biológicas en el dominio del tiempo y de la frecuencia, mediante parámetros descriptivos y análisis espectral.

# **Procedimiento, método o actividades**
Para el desarrollo de la práctica se plantearon tres fases principales. En la primera fase, se definió el sistema discreto h[n] a partir de los dígitos del código del estudiante y la señal de entrada x[n] con los dígitos de la cédula, realizando la convolución de manera manual mediante sumatorias, representándola gráficamente y posteriormente implementándola en Python para obtener y graficar el resultado de forma secuencial. En la segunda fase, se trabajó con dos señales discretas 
x1[n]=cos(2π100nTs) y x2[n]=sin(2π100nTs), definidas para un periodo de muestreo de Ts=1.25ms, calculando su correlación cruzada, graficando la secuencia resultante y analizando las situaciones en las que esta herramienta resulta útil en el procesamiento digital de señales. Finalmente, en la tercera fase, se generó una señal biológica utilizando el generador de señales, se determinó la frecuencia de Nyquist y se digitalizó aplicando una frecuencia de muestreo cuatro veces superior. Posteriormente, se caracterizó la señal en el dominio del tiempo calculando parámetros estadísticos (media, mediana, desviación estándar, máximo y mínimo) y clasificándola según su naturaleza (determinística/aleatoria, periódica/aparádica, analógica/digital). Por último, se aplicó la Transformada de Fourier a la señal, obteniendo su representación en el dominio de la frecuencia, la densidad espectral de potencia, así como el análisis de sus parámetros estadísticos (frecuencia media, mediana, desviación estándar e histograma de frecuencias).

# **Parte A**
  ## **Convolución a mano Maria Castellanos**
<img width="1418" height="887" alt="image" src="https://github.com/user-attachments/assets/141c2903-40df-45e6-b512-a8bc9fd26951" />

## **Gráfica de convolución**
<img width="1190" height="1600" alt="image" src="https://github.com/user-attachments/assets/7407e121-7240-492e-914a-3706c9652c24" />


  ## **Convolución a mano Dubrasca Martínez**
<img width="1305" height="831" alt="image" src="https://github.com/user-attachments/assets/2a42648d-17c6-4ad4-a63c-d04911c23275" />

## **Gráfica de convolución**
<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/e64c6361-a4f4-4da9-b450-6aac96954547" />



  ## **Convolución a mano Mariana Leyton**
<img width="1370" height="950" alt="image" src="https://github.com/user-attachments/assets/efa31e59-37e9-408f-847c-0b21d2f67be8" />

## **Gráfica de convolución**
 <img width="1128" height="1600" alt="image" src="https://github.com/user-attachments/assets/011be737-f350-41aa-8471-d7c0db20de17" />


## **Código en Python (Google colab)**
<pre> ```
# Importación de las librerias a utilizar
!pip install wfdb                                                    # Instalación de la liberia wfdb
import wfdb                                                          # Liberia para analizar señales fisiologicas
import matplotlib.pyplot as plt                                      # Liberia para permitir visualizar las graficas de las señales
import os                                                            # Liberia para interactuar con el sistema operativo
from google.colab import files                                       # Liberia en Google colab para subir archivos desde el computador
import numpy as np

  ```
</pre>
## **Convolución Maria Fernanda Castellanos**

<pre> ```
h = np.array([5,6,0,0,8,6,6])                                        # Sistema (código)
x = np.array([1,0,5,3,3,2,5,6,7,3])                                  # Señal (cédula)
y = np.convolve(x, h)                                                # Se realiza la convolucion y se obtiene "y" como señal de salida 

# Graficar
plt.stem(y, basefmt=" ")                                             # Función para graficar la señal de salida (plt.stem para señales discretas)
plt.title("Convolución y[n] = x[n] * h[n]")
plt.xlabel("n")
plt.ylabel("Amplitud")
plt.show()                                                           # Mostrar el gráfico en pantalla

print("y[n] =", y)                                                   # Imprimir los resultados de la convolucion de la señal de salida
  ```
</pre>

## **Gráfica de convolución**
<img width="712" height="565" alt="image" src="https://github.com/user-attachments/assets/1b88052e-5a85-44aa-ab9c-e8afe59830b5" />

y[n] = [ 5 6 25 45 41 34 83 114 143 109 88 90 122 102 60 18 ]

## **Convolución Dubrasca Martínez**

<pre> ```
h = ([5, 6, 0, 0, 7, 6, 0])                                         
x = ([5, 0, 5, 2, 2, 2, 7])                                         
y = np.convolve(x, h)

# Graficar
plt.stem(y, basefmt=" ")
plt.title("Convolución y[n] = x[n] * h[n]")
plt.xlabel("n")
plt.ylabel("Amplitud")
plt.show()

print("y[n] =", y)
  ```
</pre>

## **Gráfica de convolución**
<img width="702" height="566" alt="image" src="https://github.com/user-attachments/assets/67aab448-fbe3-44a2-be97-d1b4dd17cc66" />

y[n] = [ 25 30 25 40 57 52 82 86 26 26 61 42 0 ]

## **Convolución Mariana Leyton Palencia**

<pre> ```
h = np.array([5,6,0,0,7,5,2])
x = np.array([1,0,3,1,8,0,5,3,7,1])
y = np.convolve(x, h)

# Graficar
plt.stem(y, basefmt=" ")
plt.title("Convolución y[n] = x[n] * h[n]")
plt.xlabel("n")
plt.ylabel("Amplitud")
plt.show()

print("y[n] =", y)
  ```
</pre>

## **Gráfica de convolución**
<img width="710" height="569" alt="image" src="https://github.com/user-attachments/assets/76e19389-52e2-42e2-a121-d7740bf7803b" />

y[n] = [ 5 6 15 23 53 53 48 67 120 89 57 46 74 48 19 2 ]

## **Análisis de los resultados de la parte A**

Al analizar la señal de salida en los tres casos, se puede observar que su longitud es igual a la suma de la longitud de la señal x y la longitud del sistema h, menos uno. Este resultado es lo que se espera al realizar una convolución discreta. Además, se observa que las primeras muestras de la señal de salida aumentan a medida que se incrementa el solapamiento entre h y x. Luego, se alcanzan valores máximos en los puntos donde la superposición de los elementos más significativos de ambas señales es más pronunciada. Por ejemplo, en la segunda convolución, se obtiene un valor máximo de 86, lo que indica el momento de mayor coincidencia entre los valores más altos de h y x. En términos generales, la convolución en señales discretas describe cómo responde el sistema h ante la entrada x. En este caso, los picos en la señal de salida y representan los momentos en los que la entrada tiene componentes que coinciden de manera más clara con la estructura del sistema h.

# **Parte B**
## **Código en Python (Google colab)**

<pre> ```
#Parametros
Ts = 0.00125                                                         # Periodo de muestreo en s
fs = 1/Ts                                                            # Frecuencia de muestreo                                             
f = 100                                                              # Frecuencia de la señal
muestras = np.arange(0,9)                                            # Rango de n de 0 a 9
t = muestras * Ts                                                    # Vector de tiempo

# Señales
x1 = np.cos(2*np.pi*f*t)                                             
x2 = np.sin(2*np.pi*f*t)

# Señal x1[n]
plt.figure(figsize=(10,6))                                           
plt.subplot(2, 1, 1)                                                 # Divide la figura en dos filas y una columna y se selecciona la gráfica de la fila uno
plt.stem(muestras, x1, 'b', basefmt=' ')
plt.title('Señal x1[n] = cos(2π×100×nTs)')
plt.xlabel('muestras (n)')
plt.ylabel('Amplitud')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)                         # Linea horizontal en y = 0 para referencia

# Señal x2[n]
plt.figure(figsize=(10,6))
plt.subplot(2, 1, 1)
plt.stem(muestras, x2, 'r', basefmt=' ')
plt.title('Señal x2[n] = sin(2π×100×nTs)')
plt.xlabel('muestras (n)')
plt.ylabel('Amplitud')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)

# Correlacion
correlacion = np.correlate(x1, x2, mode= 'full')                     # Calcula la correlación cruzada entre x1 y x2
lags = np.arange(-len(x1)+1, len(x1))                                # Vector de desplazamiento k para cada punto de la correlación
plt.figure(figsize=(10,6))
plt.subplot(2, 1, 1)
plt.stem(lags, correlacion, 'g', basefmt=' ')                        # Función para graficar la señal de salida (plt.stem para señales discretas)
plt.title('Correlación Cruzada')
plt.xlabel('k (desplazamiento)')
plt.ylabel('Correlación')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.tight_layout()
plt.show()

# Imprimir resultados numéricos
print("x1[n]:", np.round(x1, 4))
print("x2[n]:", np.round(x2, 4))
print("Correlación cruzada:", np.round(correlacion, 4))
  ```
</pre>

## **Gráfica de la señal x1**

<img width="1072" height="367" alt="image" src="https://github.com/user-attachments/assets/93e573f1-0066-4ad3-852b-fe8aebd67f13" />

## **Gráfica de la señal x2**

<img width="1071" height="363" alt="image" src="https://github.com/user-attachments/assets/84d1782d-f8e3-4c96-b5eb-ae7f744609a1" />

## **Gráfica de la correlación cruzada**

<img width="1235" height="408" alt="image" src="https://github.com/user-attachments/assets/2a4b0e97-f8d1-4dbf-ab2f-ac6fa6a567bb" />

***Resultados:***

x1[n] = [ 1 0.7071 0 -0.7071 -1 -0.7071 0 0.7071 1 ]

x2[n] = [ 0 0.7071 1 0.7071 0 -0.7071 -1 -0.7071 0 ]

Correlación cruzada = [ 0 -0.7071 -1.5 -1.4142 0 2.1213 3.5 2.8284 0 -2.8284 -3.5 -2.1213 0 1.4142 1.5 0.7071 0 ]

***Descripción de la secuencia resultante:***

La secuencia de la correlación cruzada muestra una simetría casi perfecta alrededor de k=0, alternando entre valores positivos y negativos. En k=0, se observa un valor cercano a cero, lo que sugiere que no hay una correlación directa entre las señales sin desfase. Esto se debe a que x1 es un coseno y x2 es un seno de la misma frecuencia, lo que significa que están desfasados 90 grados y son prácticamente ortogonales en un ciclo completo, haciendo que su producto promedio tienda a cancelarse. Los picos más altos se presentan en retardos positivos y negativos cercanos a un cuarto de periodo, donde las señales coinciden más, lo que refuerza la idea de que la similitud entre ambas depende del desfase.

***¿En qué situaciones resulta útil aplicar la correlación cruzada en el procesamiento digital de señales?***

La correlación cruzada es una herramienta fundamental en el procesamiento digital de señales, ya que permite identificar similitudes entre señales aun cuando estén desplazadas en el tiempo. Su aplicación es útil en la detección de señales en ambientes con ruido, en la estimación de retardos temporales (como en radares y sistemas de localización GPS) y en el reconocimiento de patrones (voz, imágenes o huellas digitales).

## **Análisis de los resultados de la parte B**
En la parte B se definieron las señales x1[n]=cos(2π100nTs) y x2[n]=sin(2π100nTs) con 𝑇𝑠=1.25 ms para 0≤n<9, obteniendo vectores de 9 muestras que, al aplicar la correlación cruzada, generaron una secuencia oscilatoria y antisimétrica con máximos de aproximadamente ±3.5 en los desplazamientos k=±2. Este resultado confirma que la senoide es la cosenoide retrasada un cuarto de periodo (2 muestras, equivalentes a 2.5 ms a 100 Hz), lo cual se refleja en el corrimiento donde se alcanza la mayor similitud entre ambas señales. La representación gráfica muestra la secuencia de correlación centrada en k=0, con picos positivos y negativos que evidencian la relación de cuadratura entre el coseno y el seno.

# **Parte C**

## **Frecuencia de Nyquist para la señal**

Según la Revista Cubana de Investigaciones Biomédicas el EOG tiene un ragon de frecuencias que varia entre los 0 y 100 Hz, puesto que la frecuencia de Nyquist propone que debe ser 2 veces la frecuencia máxima, la Frecuencia para esta señal es FN=200Hz.

## **Código en Python (Google colab)**

<pre> ```
from google.colab import files
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import periodogram
from scipy.signal import correlate, convolve, periodogram
uploaded = files.upload()                                         # Subir el archivo .txt de la señal de electrooculografía adquirida del DAQ

voltaje = np.loadtxt("EOG_señal1.txt")                            # Cargar los datos de voltaje de la señal
fs = 800                                                          # Frecuencia de muestreo de 4 veces la frecuencia de Nyquist
N = len(voltaje)
t = np.arange(N) / fs                                             # eje de tiempo

# Graficar
plt.figure(figsize=(10,4))
plt.plot(t, voltaje, label="Señal EOG")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
plt.title("Señal EOG")
plt.grid(True)
plt.show()  
  ```
</pre>

## **Gráfica de la señal EOG**

<img width="1051" height="488" alt="image" src="https://github.com/user-attachments/assets/dd20318a-ab2c-4c5c-a7d1-a918d0fc1549" />

## **Caracterización de la señal**

<pre> ```
media = np.mean(voltaje)
mediana = np.median(voltaje)
desv_std = np.std(voltaje)
vmax = np.max(voltaje)
vmin = np.min(voltaje)
 ```
</pre>

Media: -0.0912,
Mediana: -0.0905,
Desviación estándar: 0.7289,
Máximo: 2.4918,
Mínimo: -2.3107,

## **Convolución, Correlación y Transformada de Fourier**

<pre> ```
# Convolución y correlación
convolucion = np.convolve(voltaje, voltaje, mode="full")
correlacion = np.correlate(voltaje, voltaje, mode="full")
lags = np.arange(-N+1, N)

# Transformada de Fourier
fft_vals = np.fft.fft(voltaje)
fft_freqs = np.fft.fftfreq(N, d=1/fs)
fft_magnitude = np.abs(fft_vals)/N

# Gráficas

# 1. Convolución 
kernel = np.ones(5) / 5   # ventana promedio
conv_result = convolve(voltaje, kernel, mode='same')

plt.figure(figsize=(10,4))
plt.plot(t, conv_result, label="Convolución (ventana 5)")
plt.xlabel("Tiempo [s]")
plt.ylabel("Amplitud")
plt.title("Convolución de la señal")
plt.grid(True)
plt.legend()
plt.show()

# 2. Correlación
corr_result = correlate(voltaje, voltaje, mode='full')
lags = np.arange(-N+1, N)

plt.figure(figsize=(10,4))
plt.stem(lags, corr_result)
plt.xlabel("Desplazamiento (lags)")
plt.ylabel("Correlación")
plt.title("Correlación de la señal")
plt.grid(True)
plt.show()
plt.figure(figsize=(10,4))
plt.plot(freqs_pos, mags_pos)
plt.title("Transformada de Fourier (Espectro de magnitud)")
plt.xlabel("Frecuencia [Hz]")
plt.ylabel("Magnitud")
plt.grid(True)
plt.show()

  
  ```
</pre>
<img width="841" height="382" alt="image" src="https://github.com/user-attachments/assets/42fd4fe3-7f95-468c-ba81-79af45d42fa3" />

<img width="867" height="379" alt="image" src="https://github.com/user-attachments/assets/30bfecfe-3362-4889-99e6-1058f07f743c" />

<img width="852" height="383" alt="image" src="https://github.com/user-attachments/assets/4917d993-85b4-4873-b9cb-b7f6e4f8ebc2" />




## **Clasificación de la señal**

<pre> ```

# Clasificación de la señal
if np.allclose(np.std(voltaje), 0):
    tipo = "Determinística constante"
elif np.max(mags_pos) / np.mean(mags_pos) > 5:
    tipo = "Predominantemente determinística, periódica"
else:
    tipo = "Aparentemente aleatoria / aperiódica"

print("\n=== Clasificación de la señal ===")
print(f"- {tipo}")
print("- Digital (está discretizada en el tiempo por el muestreo)")


  
  ```
</pre>
- Predominantemente determinística, periódica
- Digital (está discretizada en el tiempo por el muestreo)

## **Densidad espectral**

<pre> ```

# Densidad espectral de potencia (PSD)
freqs_psd, psd = periodogram(voltaje, fs)
plt.figure(figsize=(10,4))
plt.semilogy(freqs_psd, psd)
plt.title("Densidad espectral de potencia (PSD)")
plt.xlabel("Frecuencia [Hz]")
plt.ylabel("PSD")
plt.grid(True)
plt.show()

  
  ```
</pre>

<img width="861" height="388" alt="image" src="https://github.com/user-attachments/assets/8539b3ff-647c-4201-bd16-bc54d0a3b1a7" />

## **Datos estadisticos**

<pre> ```


mask = fft_freqs >= 0
freqs_pos = fft_freqs[mask]
mags_pos = fft_magnitude[mask]

energia = mags_pos**2
energia_total = np.sum(energia)

# Frecuencia media (centroide espectral)
freq_media = np.sum(freqs_pos * energia) / energia_total

# Frecuencia mediana
energia_acum = np.cumsum(energia)
freq_mediana = freqs_pos[np.where(energia_acum >= energia_total/2)[0][0]]

# Desviación estándar en frecuencia
freq_std = np.sqrt(np.sum(((freqs_pos - freq_media)**2) * energia) / energia_total)

print("\n=== Estadísticos en frecuencia ===")
print(f"Frecuencia media: {freq_media:.2f} Hz")
print(f"Frecuencia mediana: {freq_mediana:.2f} Hz")
print(f"Desviación estándar: {freq_std:.2f} Hz")


plt.figure(figsize=(8,4))
plt.hist(freqs_pos, weights=energia, bins=40, color="c", edgecolor="k")
plt.title("Histograma de energía por frecuencia")
plt.xlabel("Frecuencia [Hz]")
plt.ylabel("Energía acumulada")
plt.grid(True)
plt.show()

  
  ```
</pre>

Frecuencia media: 17.21 Hz,
Frecuencia mediana: 10.00 Hz,
Desviación estándar: 41.09 Hz
<img width="697" height="386" alt="image" src="https://github.com/user-attachments/assets/bbbdbc0d-31b5-434d-80e7-252e0ebf614f" />



## **Análisis de los resultados de la parte C**
La señal biológica generada mediante el generador de señales corresponde a un EOG, la cual fue muestreada con una frecuencia de fs = 800 Hz, lo que implica una frecuencia de Nyquist de 400 Hz, suficiente para garantizar un análisis espectral libre de aliasing; aunque la condición pedida en el laboratorio establecía muestrear a 4 veces la frecuencia de Nyquist (1600 Hz), en este caso los 800 Hz siguen siendo adecuados dado que la mayor parte de la energía de la señal se concentra por debajo de los 50 Hz. En el dominio del tiempo, la señal presentó una media de -0.0912 V, mediana de -0.0905 V, desviación estándar de 0.7289 V, valor máximo de 2.4918 V y mínimo de -2.3107 V, evidenciando oscilaciones alrededor de cero, propias de este tipo de registros biológicos. En el procesamiento temporal, la convolución con una ventana de 5 puntos permitió suavizar la señal y destacar su envolvente, mientras que la autocorrelación mostró simetría y picos periódicos, confirmando la naturaleza periódica de la señal. En el dominio de la frecuencia, la Transformada de Fourier y la Densidad Espectral de Potencia (PSD) indicaron que la mayor parte de la energía se concentra en bajas frecuencias, destacándose componentes principales por debajo de los 50 Hz, lo cual es característico de señales EOG. Los estadísticos espectrales obtenidos fueron: frecuencia media de 17.21 Hz, mediana de 10 Hz y desviación estándar de 41.09 Hz, valores que concuerdan con el histograma de energía, el cual mostró la mayor concentración energética en frecuencias bajas. De esta manera, la señal puede clasificarse como predominantemente determinística, periódica y digital, lo que concuerda tanto con su comportamiento temporal como espectral. En conclusión, la señal procesada cumple con las características de una señal biológica de baja frecuencia, siendo representativa de un registro EOG y validando correctamente los pasos del laboratorio en cuanto a adquisición, digitalización, caracterización estadística y análisis espectral.

# **Diagramas de flujo**

## **Parte A**
<img width="1436" height="2093" alt="_Diagrama de flujo" src="https://github.com/user-attachments/assets/62389d6d-7d36-4f7b-a2a1-f6e4732c6a68" />

## **Parte B**
<img width="2171" height="4800" alt="_Diagrama de flujo (1)" src="https://github.com/user-attachments/assets/7062cc88-b80e-4354-a5c7-dee116b51923" />

## **Parte c**
<img width="1760" height="1360" alt="_Diagrama de flujo" src="https://github.com/user-attachments/assets/aa261245-2a6b-4730-af29-f5af757f14de" />





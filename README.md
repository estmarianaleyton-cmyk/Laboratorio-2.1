# Laboratorio 2 - Convolucion y transformada de fourier

**Universidad Militar Nueva Granada**

**Asignatura:** Procesamiento Digital de Señales

**Estudiantes:** Dubrasca Martinez, Mariana Leyton, Maria Fernanda Castellanos

**Fecha:** 19 de septiembre de 2025

**Título de la práctica:** Convolucion, transformada y estadisticos descriptivos de la señal EOG.

# **Objetivos**
- Comprender la convolución como una operación que permite obtener la respuesta de un sistema discreto ante una entrada determinada.
- Analizar la correlación como medida de similitud entre dos señales.
- Aplicar la Transformada de Fourier como herramienta de análisis en el dominio de la frecuencia.
- Caracterizar estadísticamente señales biológicas en el dominio del tiempo y de la frecuencia, mediante parámetros descriptivos y análisis espectral.
# **Procedimiento**
Para el desarrollo de la práctica se plantearon tres fases principales. En la primera fase, se definió el sistema discreto h[n] a partir de los dígitos del código del estudiante y la señal de entrada x[n] con los dígitos de la cédula, realizando la convolución de manera manual mediante sumatorias, representándola gráficamente y posteriormente implementándola en Python para obtener y graficar el resultado de forma secuencial. En la segunda fase, se trabajó con dos señales discretas 
𝑥[𝑛]=cos(2𝜋100𝑛𝑇𝑠) y x2[n]=cos(2π100nTs) y 𝑥2[𝑛]=sin⁡(2𝜋100𝑛𝑇𝑠)x2	[n]=sin(2π100nTs), definidas para un periodo de muestreo 𝑇𝑠=1.25𝑚𝑠 Ts=1.25ms, calculando su correlación cruzada, graficando la secuencia resultante y analizando las situaciones en las que esta herramienta resulta útil en el procesamiento digital de señales. Finalmente, en la tercera fase, se generó una señal biológica utilizando el generador de señales, se determinó la frecuencia de Nyquist y se digitalizó aplicando una frecuencia de muestreo cuatro veces superior. Posteriormente, se caracterizó la señal en el dominio del tiempo calculando parámetros estadísticos (media, mediana, desviación estándar, máximo y mínimo) y clasificándola según su naturaleza (determinística/aleatoria, periódica/aparádica, analógica/digital). Por último, se aplicó la Transformada de Fourier a la señal, obteniendo su representación en el dominio de la frecuencia, la densidad espectral de potencia, así como el análisis de sus parámetros estadísticos (frecuencia media, mediana, desviación estándar e histograma de frecuencias).

# **Parte A**
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

Resultados:

x1[n] = [ 1 0.7071 0 -0.7071 -1 -0.7071 0 0.7071 1 ]

x2[n] = [ 0 0.7071 1 0.7071 0 -0.7071 -1 -0.7071 0 ]

Correlación cruzada = [ 0 -0.7071 -1.5 -1.4142 0 2.1213 3.5 2.8284 0 -2.8284 -3.5 -2.1213 0 1.4142 1.5 0.7071 0 ]

## **Análisis de los resultados de la parte B**


# **Parte C**
## **Código en Python (Google colab)**



#**Diagramas de flujo**
** Parte A **
<img width="1436" height="2093" alt="_Diagrama de flujo" src="https://github.com/user-attachments/assets/62389d6d-7d36-4f7b-a2a1-f6e4732c6a68" />


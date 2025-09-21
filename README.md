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

import numpy as np
!pip install wfdb
import wfdb
import matplotlib.pyplot as plt
from google.colab import files

**Maria Fernanda Castellanos Piza**
h = np.array([5,6,0,0,8,6,6])
x = np.array([1,0,5,3,3,2,5,6,7,3])
y = np.convolve(x, h)

# Graficar
plt.stem(y, basefmt=" ")
plt.title("Convolución y[n] = x[n] * h[n]")
plt.xlabel("n")
plt.ylabel("Amplitud")
plt.show()

print("y[n] =", y)
<img width="571" height="455" alt="download" src="https://github.com/user-attachments/assets/2293d9e2-409d-4edf-a32b-34dea67da8e8" />
**Dubrasca Martinez**
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
<img width="562" height="455" alt="download" src="https://github.com/user-attachments/assets/51f36e2f-3a3b-431b-a470-5a12329f370e" />

**Mariana Leyton**
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
<img width="571" height="455" alt="download" src="https://github.com/user-attachments/assets/4aae3e43-0524-49e0-973e-454d6eaf1ec5" />
# **Parte B**
## **Código en Python (Google colab)**
import numpy as np
import matplotlib.pyplot as plt

# Parametros
Ts = 0.00125                                           # Tiempo de muestreo en s
f = 100                                                # Frecuencia en Hz
muestras = np.arange(0,9)                              # Rango de n de 0 a 8
t = muestras * Ts                                      # Vector de tiempo

# Señales
x1 = np.cos(2*np.pi*f*t)
x2 = np.sin(2*np.pi*f*t)

# Gráficas
# Señal x1[n]
plt.figure(figsize=(10,6))
plt.subplot(2, 1, 2)
plt.stem(muestras, x1, 'b', basefmt=' ')
plt.title('Señal x1[n] = cos(2π×100×nTs)')
plt.xlabel('muestras (n)')
plt.ylabel('Amplitud')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)

# Señal x2[n]
plt.figure(figsize=(10,6))
plt.subplot(2, 1, 2)
plt.stem(muestras, x2, 'r', basefmt=' ')
plt.title('Señal x2[n] = sin(2π×100×nTs)')
plt.xlabel('muestras (n)')
plt.ylabel('Amplitud')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)


# Correlación cruzada
correlacion = np.correlate(x1, x2, mode='full')
lags = np.arange(-len(x1)+1, len(x1))               # Ejes de desplazamiento (k)
plt.figure(figsize=(10,6))
plt.subplot(2, 1, 2)
plt.stem(lags, correlacion, 'g', basefmt=' ')
plt.title('Correlación Cruzada Rₓ₁ₓ₂[k]')
plt.xlabel('k (desplazamiento)')
plt.ylabel('Correlación')
plt.grid(True, alpha=0.3)
plt.axhline(0, color='black', linewidth=0.5)
plt.tight_layout()
plt.show()

# Mostrar valores numéricos
print("\n=== x1[n] ===")
for i, val in enumerate(x1):
    print(f"x1[{i}] = {val:.4f}")

print("\n=== x2[n] ===")
for i, val in enumerate(x2):
    print(f"x2[{i}] = {val:.4f}")

print("\n=== Correlación cruzada R_x1x2[k] ===")
for k, val in zip(lags, correlacion):
    print(f"k = {k:>2d} -> R[k] = {val:.4f}")

# Descripción de la secuencia
print("Descripción:")
print("La correlación cruzada es cercana a cero para casi todos los desplazamientos,")
print("lo que indica que x1[n] y x2[n] son casi ortogonales (desfasadas 90°).")
print("Los valores positivos y negativos muestran la relación senoidal entre ambas.")
<img width="857" height="295" alt="download" src="https://github.com/user-attachments/assets/39c27c3f-c1f3-4be0-b6e5-b4289bfcd3bb" />
<img width="857" height="295" alt="download" src="https://github.com/user-attachments/assets/eb2b1656-4e03-46ce-93dc-c4b4351a05df" />
<img width="990" height="330" alt="download" src="https://github.com/user-attachments/assets/05c0cc92-1c09-4230-b91e-15e2d176616e" />
=== x1[n] ===
x1[0] = 1.0000
x1[1] = 0.7071
x1[2] = 0.0000
x1[3] = -0.7071
x1[4] = -1.0000
x1[5] = -0.7071
x1[6] = -0.0000
x1[7] = 0.7071
x1[8] = 1.0000

=== x2[n] ===
x2[0] = 0.0000
x2[1] = 0.7071
x2[2] = 1.0000
x2[3] = 0.7071
x2[4] = 0.0000
x2[5] = -0.7071
x2[6] = -1.0000
x2[7] = -0.7071
x2[8] = -0.0000

=== Correlación cruzada R_x1x2[k] ===
k = -8 -> R[k] = -0.0000
k = -7 -> R[k] = -0.7071
k = -6 -> R[k] = -1.5000
k = -5 -> R[k] = -1.4142
k = -4 -> R[k] = -0.0000
k = -3 -> R[k] = 2.1213
k = -2 -> R[k] = 3.5000
k = -1 -> R[k] = 2.8284
k =  0 -> R[k] = -0.0000
k =  1 -> R[k] = -2.8284
k =  2 -> R[k] = -3.5000
k =  3 -> R[k] = -2.1213
k =  4 -> R[k] = 0.0000
k =  5 -> R[k] = 1.4142
k =  6 -> R[k] = 1.5000
k =  7 -> R[k] = 0.7071
k =  8 -> R[k] = 0.0000
Descripción:
La correlación cruzada es cercana a cero para casi todos los desplazamientos,
lo que indica que x1[n] y x2[n] son casi ortogonales (desfasadas 90°).
Los valores positivos y negativos muestran la relación senoidal entre ambas.

**¿En qué situaciones resulta útil aplicar la correlación cruzada en
el procesamiento digital de señales?**
La correlación cruzada es una herramienta fundamental en el procesamiento digital de señales, ya que permite identificar similitudes entre señales aun cuando estén desplazadas en el tiempo. Su aplicación es útil en la detección de señales en ambientes con ruido, en la estimación de retardos temporales (como en radares, sonar y sistemas de localización GPS) y en el reconocimiento de patrones (voz, imágenes o huellas digitales).
# **Parte C**
## **Código en Python (Google colab)**
from google.colab import files
import numpy as np
import matplotlib.pyplot as plt
uploaded = files.upload()
# Cargar los datos
voltaje = np.loadtxt("EOG_señal1.txt")

# Definir parámetros de muestreo
fs = 800  # Hz (ajústalo al valor que usaste)
N = len(voltaje)
t = np.arange(N) / fs  # eje de tiempo

# Graficar
plt.figure(figsize=(10,4))
plt.plot(t, voltaje, label="Señal EOG")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
plt.title("Señal EOG")
plt.legend()
plt.grid(True)
plt.show()
<img width="844" height="393" alt="download" src="https://github.com/user-attachments/assets/53fcbbaa-b4c5-4994-bb45-faea5796cb29" />

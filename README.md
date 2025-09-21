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




# Variabilidad-de-la-FC-usando-la-Transformada-Wavelet

## Tabla de Contenidos 
1.[Introducción](#introducción)
2.[Requisitos](#requisitos)
3.[Fundamento teorico](#fundamento-teorico)
4.[Explicación del Código](#explicación-del-código)
5.[Resultados y Gráficas](#resultados-y-gráficas)
6.[Conclusión](#conclusión)

## Introducción 
## Fundamento teorico
**Actividad simpática y parasimpática del sistema nervioso autónoma**

El sistema nervioso autónomo (SNA) regula funciones involuntarias del cuerpo como la frecuencia cardíaca, la respiración y la digestión. Se divide en dos:

**Simpática**: Prepara al cuerpo para situaciones de “lucha o huida”. Aumenta la frecuencia cardíaca, la presión arterial y dilata las vías respiratorias.
Estimulación simpática: Incrementa la frecuencia cardíaca (taquicardia) al liberar noradrenalina, que actúa sobre los receptores beta del corazón.

**Parasimpática**: Promueve un estado de “descanso y digestión”. Disminuye la frecuencia cardíaca, aumenta la actividad digestiva y favorece la relajación.
Estimulación parasimpática: Reduce la frecuencia cardíaca (bradicardia) a través del nervio vago, que libera acetilcolina, disminuyendo la velocidad de despolarización del nodo sinoauricular.

La variabilidad de la frecuencia cardiaca (HRV) se refiere a las variaciones en el tiempo entre latidos consecutivos del corazón, específicamente en los intervalos R-R del ECG.

Se considera un indicador del equilibrio entre el sistema simpático y parasimpático, porque la HRV refleja cómo el cuerpo ajusta la frecuencia cardíaca en respuesta a estímulos, mostrando el balance dinámico entre la activación del sistema simpático (acelera el corazón) y del parasimpático (lo desacelera).

Se mide en el dominio del tiempo (media y desviación estándar de los intervalos R-R) y en el dominio de la frecuencia, donde se identifican componentes importantes:
Banda de alta frecuencia (HF): 0.15 – 0.4 Hz → asociada con actividad parasimpática.
Banda de baja frecuencia (LF): 0.04 – 0.15 Hz → refleja actividad simpática y parasimpática combinadas.
Banda de muy baja frecuencia (VLF): <0.04 Hz → mecanismos más complejos, menos comprendidos.

**Transformada Wavelet**

La Transformada Wavelet es una técnica de análisis tiempo-frecuencia que permite descomponer una señal en componentes localizados tanto en el tiempo como en la frecuencia. A diferencia de la FFT (Transformada Rápida de Fourier), la wavelet permite detectar cambios transitorios y analizar señales no estacionarias, como el ECG.



**Usos en señales biológicas**:
Detección de picos R en ECG.
Análisis de la variabilidad de la frecuencia cardíaca HRV.
Caracterización de señales EEG, EMG y otras biopotenciales para ver cómo cambian en el tiempo.

**Tipos de wavelet comunes en señales biológicas**:
Daubechies (db): muy usada para detectar picos R por su forma similar a las ondas ECG.
Coiflets y Symlets: versiones modificadas de Daubechies, con mejores propiedades de simetría y regularidad.
Wavelet de Morlet: útil en transformada wavelet continua (CWT), por su buena resolución frecuencia-temporal.

##


## Diseño de filtro IIR

 Se realizo el filtrado eliminando ruido de baja frecuencia (movimientos respiratorios) y ruido de añta frecuencia (actividad muscular, interferencia electrica), se uso una frecuencia de muestreo de 250Hz, con frecuencias de corte de 0.5Hz para eliminar oscilaciones lentas que no son propias del electrocardiograma, y de 40 Hz obteniendo los componentes del QRS (los cuales oscilan entre 10-30Hz) y elimina el ruido muscular que es mayor a 40Hz

## Resultados

Analisis HVR en el dominio del tiempo: Se calcularon los parametros sobre el intervalos R-R 
-Media RR: Frecuencia cardiaca promedio 80bpm
-SDNN:  Mide la dispersión de los intervalos entre latidos cardíacos, lo que puede indicar la salud del sistema nervioso autónomo
-RMSSD: Refleja la actividad parasimpatica 
-pNN50: Parámetro utilizado en el análisis de la variabilidad de la frecuencia cardiaca (VFC) que mide la proporción de intervalos R-R consecutivos en un electrocardiograma (ECG



Durante reposo, se espera una HRV moderada, con dominio vagal (parasimpático)

## Conclusiones

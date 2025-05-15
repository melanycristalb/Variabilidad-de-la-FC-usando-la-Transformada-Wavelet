# Variabilidad-de-la-FC-usando-la-Transformada-Wavelet

## Tabla de Contenidos 
1.[Introducción](#introducción)
2.[Requisitos](#requisitos)
3.[Fundamento teorico](#fundamento-teorico)
4.[Resultados y Gráficas](#resultados-y-gráficas)
5.[Conclusión](#conclusión)

## Introducción 
El análisis de la variabilidad de la frecuencia cardíaca (HRV) es una herramienta no invasiva ampliamente utilizada para evaluar el funcionamiento del sistema nervioso autónomo (SNA), particularmente el balance entre sus ramas simpática y parasimpática. La HRV se mide a partir de los cambios en los intervalos entre latidos sucesivos del corazón (intervalos R-R), extraídos de una señal electrocardiográfica (ECG). Este análisis permite detectar alteraciones fisiológicas asociadas a estrés, enfermedades cardiovasculares, fatiga o estados emocionales.

En esta práctica de laboratorio se pretende aplicar herramientas de procesamiento digital de señales (DSP) para el análisis cuantitativo de la HRV. Para ello, se adquiere una señal ECG de un sujeto en estado de reposo y se aplica un conjunto de técnicas que incluyen el filtrado digital IIR, la detección de picos R, el cálculo de intervalos R-R, y el análisis en el dominio del tiempo. Posteriormente, se implementa una transformada wavelet para observar cómo varían las frecuencias fisiológicas asociadas a la HRV a lo largo del tiempo, permitiendo así una caracterización más completa y dinámica del comportamiento cardíaco.

Dado que esta práctica involucra la captura de señales fisiológicas de un ser humano, se consideraron principios éticos fundamentales. Previamente a la adquisición de la señal ECG, se obtuvo el consentimiento informado del participante. Este documento fue firmado tras una explicación clara del procedimiento, sus fines académicos, la duración del experimento, el manejo confidencial de los datos, y la opción de retirarse en cualquier momento sin consecuencias. Además, se garantizó que el participante no presentara condiciones médicas que contraindiquen la participación en la prueba
.

## Requisitos
- **Python** Instalado en tu sistema.
- **Arduino** Instalado en tu sistema.
- **Bibliotecas de Python:** `numpy`,`matplotlib.pyplot`,`scipy`,`sklearn`.
-**Modulo AD8232**
- **Electrodos**

## Fundamento teorico
**Actividad simpática y parasimpática del sistema nervioso autónoma**

El sistema nervioso autónomo (SNA) regula funciones involuntarias del cuerpo como la frecuencia cardíaca, la respiración y la digestión. Se divide en dos:

**Simpática**: Prepara al cuerpo para situaciones de “lucha o huida”. Aumenta la frecuencia cardíaca, la presión arterial y dilata las vías respiratorias.
Estimulación simpática: Incrementa la frecuencia cardíaca (taquicardia) al liberar noradrenalina, que actúa sobre los receptores beta del corazón.

**Parasimpática**: Promueve un estado de “descanso y digestión”. Disminuye la frecuencia cardíaca, aumenta la actividad digestiva y favorece la relajación.
Estimulación parasimpática: Reduce la frecuencia cardíaca (bradicardia) a través del nervio vago, que libera acetilcolina, disminuyendo la velocidad de despolarización del nodo sinoauricular.

SNA (Sistema Nervioso Autónomo):
Regula la actividad del corazón a través de la rama simpática (acelera frecuencia cardíaca) y parasimpática (la reduce). La HRV (Heart Rate Variability) refleja el balance entre estas ramas.

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

En el presente estudio se aplicó la transformada waveleta la señal interpolada de HRV, utilizando la wavelet tipo Morlet, recomendada para señales biológicas debido a su adecuada resolución en el dominio tiempo-frecuencia. El espectrograma resultante permitió observar la distribución dinámica de las frecuencias a lo largo del tiempo, revelando una mayor potencia sostenida en la banda de baja frecuencia (0.04–0.15 Hz), asociada a la regulación del sistema simpático y parasimpático. En contraste, la banda de alta frecuencia (HF: 0.15–0.4 Hz), vinculada principalmente a la actividad parasimpática modulada por la respiración, mostró una potencia reducida y poco variable. Esta diferencia sugiere un predominio simpático o una actividad vagal disminuida, lo cual es consistente con un estado de reposo sin estimulación externa, pero con un bajo rango de oscilación respiratoria. A lo largo del tiempo, las frecuencias se mantuvieron relativamente estables, sin transiciones bruscas, reflejando una condición fisiológica controlada  durante el periodo de medición.

## Diseño de filtro IIR

 Se realizo el filtrado eliminando ruido de baja frecuencia (movimientos respiratorios) y ruido de añta frecuencia (actividad muscular, interferencia electrica), se uso una frecuencia de muestreo de 250Hz, con frecuencias de corte de 0.5Hz para eliminar oscilaciones lentas que no son propias del electrocardiograma, y de 40 Hz obteniendo los componentes del QRS (los cuales oscilan entre 10-30Hz) y elimina el ruido muscular que es mayor a 40Hz

 ## Variabilidad de la frecuencia cardiaca (HVR)

 Para evaluar la variabilidad de la frecuencia cardíaca (HRV) en el dominio del tiempo, se calcularon los parámetros estadísticos a partir de los intervalos R-R detectados en la señal ECG filtrada. Entre ellos se encuentran la media de los intervalos R-R (AVNN), que refleja el ritmo cardíaco promedio; la desviación estándar de los intervalos R-R (SDNN), como medida de la variabilidad global del sistema nervioso autónomo; el RMSSD, que cuantifica la variabilidad a corto plazo asociada principalmente a la actividad parasimpática; y el pNN50, que representa el porcentaje de diferencias sucesivas entre intervalos R-R mayores a 50 ms. En el análisis realizado, la media de los intervalos R-R fue consistente con una frecuencia cardíaca cercana a 80 bpm, mientras que los valores de SDNN y RMSSD se mantuvieron en rangos moderados, sugiriendo un equilibrio aceptable entre las ramas simpática y parasimpática. No obstante, un valor bajo de pNN50 indicó escasa fluctuación entre latidos consecutivos, lo cual podría reflejar una actividad vagal disminuida o un patrón respiratorio muy regular, especialmente durante condiciones de reposo. Este análisis estadístico permite no solo caracterizar el comportamiento autonómico del sujeto, sino también establecer una línea base sobre la cual podrían evaluarse futuros estados de estrés, fatiga o disfunción autonómica.

## Resultados

Analisis HVR en el dominio del tiempo: Se calcularon los parametros sobre el intervalos R-R 
-Media RR: Frecuencia cardiaca promedio 80bpm
-SDNN:  Mide la dispersión de los intervalos entre latidos cardíacos, lo que puede indicar la salud del sistema nervioso autónomo
-RMSSD: Refleja la actividad parasimpatica 
-pNN50: Parámetro utilizado en el análisis de la variabilidad de la frecuencia cardiaca (VFC) que mide la proporción de intervalos R-R consecutivos en un electrocardiograma (ECG

## Diagrama de flujo


Durante reposo, se espera una HRV moderada, con dominio vagal (parasimpático)

## Conclusiones

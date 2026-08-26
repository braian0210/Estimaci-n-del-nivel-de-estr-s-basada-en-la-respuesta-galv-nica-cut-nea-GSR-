# Estimaci-n-del-nivel-de-estr-s-basada-en-la-respuesta-galv-nica-cut-nea-GSR-

INTRODUCCIÓN

La actividad electrodérmica (Electrodermal Activity, EDA) agrupa los fenómenos eléctricos que ocurren a nivel de la piel, siendo la conductancia cutánea el más utilizado en ingeniería biomédica,  la facilidad con la que la piel conduce electricidad, modulada por la actividad de las glándulas sudoríparas ecrinas bajo control del sistema nervioso simpático, medida típicamente mediante  corriente directa con electrodos de Ag-AgCl [1]. Esta señal posee dos componentes complementarias, una componente tónica o basal, el nivel de conductancia cutánea (SCL), y una componente fásica o transitoria, la respuesta de conductancia cutánea (SCR o GSR), que se manifiesta como un incremento  de la conductancia ante un estímulo, seguido de un retorno gradual y considerablemente más lento hacia el valor basal [1].

La selección del sitio anatómico de registro es determinante para la calidad de esta señal. Clásicamente, la palma y los dedos han sido preferidos por concentrar glándulas sudoríparas con mayor respuesta emocional específica; sin embargo, la frente ha sido documentada desde hace más de setenta años como un sitio igualmente capaz de producir sudoración de origen emocional. McGregor demostró experimentalmente que la frente responde tanto a estímulos térmicos como emocionales, empleando un modelo de tensión anticipatoria en estudiantes que esperaban el resultado de un examen oral [2].  Estudios posteriores han corroborado que la frente concentra una de las densidades más altas de glándulas sudoríparas ecrinas de todo el cuerpo, aunque advierten que su respuesta está más influenciada por carga térmica que la de sitios como la palma [3], razón por la cual la temperatura ambiental debe controlarse durante el registro. Trabajos recientes en ingeniería de instrumentación han confirmado la frente como uno de varios sitios corporales viables para la adquisición de EDA junto con el pie, el dedo y el hombro, con la salvedad de una mayor variabilidad interindividual respecto a la palma [4].

Sobre esta base fisiológica, distintos trabajos han validado sistemas de bajo costo para la adquisición de GSR mediante microcontroladores de propósito general, empleando divisores resistivo-capacitivos y electrodos superficiales conectados a plataformas como Arduino [5]. La utilidad de esta señal como indicador de estrés ha sido demostrada en población universitaria, donde el análisis conjunto de la variabilidad de la frecuencia cardiaca y la GSR permite diferenciar de forma efectiva estados de reposo y de estrés inducido [6], y su capacidad para reflejar esfuerzo mental ha sido explorada específicamente mediante dispositivos vestibles [7].

En esta práctica se diseñó  un dispositivo vestible basado en el microcontrolador ESP32-S3, capaz de capturar de forma continua las variaciones de la GSR mediante un divisor de tensión resistivo-capacitivo con electrodos ubicados en la frente, y transmitir dicha señal de forma inalámbrica por Bluetooth a un computador para su visualización y análisis en tiempo real.

OBJETIVOS

Objetivo General:

• Proporcionar un sistema de medición continua de estrés
basado en respuesta galvánica cutánea (GSR).
Objetivos Específicos:

• Identificar las componentes estacionaria y transitoria de la GSR.

• Elaborar un dispositivo vestible que permita capturar de forma continua las
variaciones de la GSR.

• Plantear hipótesis desde la fisiología humana sobre el rol de la GSR como
indicador de estrés.

PARTE A.

1. Llevar a cabo una revisión de la literatura sobre la actividad electrodérmica y
respuesta galvánica cutánea.

La actividad electrodérmica (EDA) es el término general que agrupa los distintos fenómenos eléctricos medibles en la piel humana, el mecanismo fisiológico involucrado está relacionado principalmente con la activación de las glándulas sudoríparas ecrinas. Estas glándulas reciben la señal de fibras nerviosas simpáticas colinérgicas, que utilizan la acetilcolina como neurotransmisor para generar la respuesta de sudoración. A diferencia de otras respuestas autonómicas, Debido a que la EDA no presenta una influencia parasimpática que contrarreste su respuesta, puede utilizarse como un indicador bastante directo de la activación del sistema nervioso simpático en una persona [1].

Existen dos formas fundamentales de registrar esta actividad. El método endosomático mide la diferencia de potencial que existe de forma espontánea entre un sitio activo (palma o planta) y un sitio de referencia relativamente inactivo (antebrazo), sin aplicar corriente externa. El método exosomático, ampliamente preferido en la literatura por su sencillez de interpretación, aplica una corriente directa (DC) de bajo voltaje constante (típicamente 0.5 V) a través de un par de electrodos, generalmente de Ag-AgCl, situados sobre la piel. Dado que la piel se comporta como una resistencia, la corriente resultante es proporcional al inverso de dicha resistencia, es decir, a la conductancia cutánea [1]. Existe también la alternativa de corriente alterna (AC), que reduce artefactos de polarización electródica, aunque su uso permanece considerablemente menos extendido [1].

La señal de conductancia cutánea posee dos componentes claramente diferenciables:

- Nivel de conductancia cutánea (SCL, Skin Conductance Level): componente tónica o basal, que varía lentamente en el tiempo  y refleja el estado general de activación autonómica del sujeto.
  
- Respuesta de conductancia cutánea (SCR o GSR, Skin Conductance Response): corresponde a la parte transitoria de la señal que se presenta sobre la SCL. Se caracteriza por un aumento relativamente rápido de la conductancia, que suele aparecer después de 1 a 3 segundos, seguido de una disminución más lenta hasta regresar al nivel basal. Esta diferencia entre la rapidez con la que aumenta y disminuye la señal es una de las principales características que permite identificar una SCR real y diferenciarla del ruido o de posibles artefactos en la medición [1].

Un problema metodológico documentado es que las SCR suelen ser de magnitud pequeña en comparación con la SCL sobre la que se superponen, lo que dificulta su observación directa si el sistema de adquisición no cuenta con suficiente rango o una función de autoescalado adecuada [1].

Desde el punto de vista de aplicación en ingeniería biomédica, la GSR ha sido validada como indicador efectivo de estrés en población universitaria, donde su análisis conjunto con la variabilidad de la frecuencia cardiaca permite diferenciar estadísticamente estados de reposo y de estrés inducido [6]. También ha sido empleada en dispositivos vestibles de bajo costo basados en microcontroladores de propósito general (Arduino), interfaz gráfica y divisores resistivos similares al empleado en esta práctica [5], así como en la predicción de esfuerzo mental mediante características extraídas de la señal en registros prolongados de uso cotidiano [7].

2. Investigue sobre los efectos de las corrientes directa y alterna en seres
humanos (norma IEC 60479, ítems 1-5).



3. Con valores de alimentación entre +3.3 y +5 VDC, realice los cálculos
necesarios para garantizar que a través de la piel de un sujeto sano circule una
corriente no mayor a 1 mA. Para ello, contemple en caso extremo en el que la
resistencia de la piel equivale a un cortocircuito (i.e., Rskin = 0 Ω).



4. Diseñe un dispositivo vestible que permita capturar las variaciones de la GSR y
transmitirlas de forma alámbrica a un computador personal. Medite muy bien
sobre la región anatómica a la cual se sujetarán los electrodos para capturar la
señal con un mínimo de interferencia.



PARTE B

1. Construya y presente el dispositivo para medir la GSR en tiempo real y que
permita visualizar la señal tal y como es capturada. Evalúe el comportamiento
del dispositivo mientras el sujeto que lo lleva puesto (i.e., sujeto de prueba) se
mueve, camina o realiza tareas como escribir.

2. Pídale al sujeto de prueba que, en reposo y cómodamente sentado, realice una
inspiración profunda y que luego exhale lentamente. En respuesta, la GSR
debe aumentar considerablemente en valor para luego regresar muy
paulatinamente al valor inicial. Tome nota de los valores máximo y mínimo y
defina, con base en ellos, umbrales para denotar poco estrés, estrés moderado
y elevado.

3. Realice las modificaciones y/o adiciones al dispositivo que sean necesarias
para que éste transmita los datos de forma inalámbrica al computador personal
o, incluso, a un celular. Para este caso, lo que se mostrará no será la señal 
sino un mensaje o alerta que indique el “nivel” de estrés que esa persona
percibe.

PARTE C
1. Presente el dispositivo para medir la GSR en tiempo real y que, mediante
transmisión inalámbrica, muestre el nivel de estrés que percibe un sujeto
mientras resuelve problemas que demandan cierto nivel de concentración y
esfuerzo mental. Para ello, se le aplicará un breve examen al sujeto de prueba
mientras lleva puesto el vestible.

2. Documente la práctica explicando paso a paso cuál fue el procedimiento que
se siguió y dando respuesta a las preguntas que se formulan en la guía (ver
Parte 15). Suministre una breve conclusión y elabore un repositorio en la
plataforma GitHub que contenga toda la información recopilada en las partes A
y B. Asegúrese de incluir gráficas con buena resolución. Cada estudiante debe
tener su propia cuenta y deben aparecer como colaboradores en el repositorio.
En caso contrario, solo se calificará al estudiante que aparece como editor.

REFERENCIAS

[1] SPR Ad Hoc Committee on Electrodermal Measures. "Publication recommendations for electrodermal measurements." Psychophysiology, vol. 49, no. 8, pp. 1017–1034, 2012. doi: 10.1111/j.1469-8986.2012.01384.x

[2] I. A. McGregor. "The Sweating Reactions of the Forehead." The Journal of Physiology, vol. 116, no. 1, pp. 26–34, 1952.

[3] C. A. Machado-Moreira, F. Wilmink, A. Meijer, I. B. Mekjavic, y N. A. S. Taylor. "Local differences in sweat secretion from the head during rest and exercise in the heat." European Journal of Applied Physiology, vol. 104, pp. 257–264, 2008. doi: 10.1007/s00421-007-0645-y

[4] J. Brandstetter, E.-M. Knoch, y F. Gauterin. "Towards In-Vehicle Non-Contact Estimation of EDA-Based Arousal with LiDAR." Sensors, vol. 25, no. 23, art. 7395, 2025.

[5] A. N. Jayanthi, R. Nivedha, y C. Vani. "Galvanic Skin Response Measurement and Analysis." International Journal of Applied Engineering Research, vol. 10, no. 16, 2015.

[6] J. R. Jiménez Cruz y M. A. González Rivera. "Estimación del estrés por medio de la entropía de la variabilidad de la frecuencia cardíaca y la respuesta galvánica de la piel." Pistas Educativas, no. 134, pp. 322–340, nov. 2019.

[7] W. Romine, N. Schroeder, T. Banerjee, y J. Graft. "Toward Mental Effort Measurement Using Electrodermal Activity Features." Sensors, vol. 22, no. 19, art. 7363, 2022.

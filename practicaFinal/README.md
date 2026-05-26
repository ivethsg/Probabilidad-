# Proyecto Final: Análisis Estadístico de Datos COVID-19 en Python
**Asignatura:** Probabilidad y Estadística  

**Estudiante:** Iveth Esperanza Santacruz Guerrero

**Docente:** Dr. José Gabriel Rodríguez Rivas  
**Grupo:** 2Y

**Periodo del semestre:** 6

**Fecha de entrega:**  25/05/2026

**Integrantes del equipo:** Iveth Santacruz
---
##  2. Marco Teórico: Tipos de Muestreo y Teorema del Límite Central

### A. Tipos de Muestreo

En el análisis estadístico, el muestreo es el proceso de seleccionar un subconjunto de individuos de una población para estimar las características de todo el universo de datos. Se dividen en dos grandes familias:

#### 1. Muestreo Probabilístico
Todos los elementos de la población tienen una probabilidad conocida y diferente de cero de ser seleccionados. Garantiza la representatividad estadística.

* **Aleatorio Simple:** Cada elemento de la población tiene exactamente la misma probabilidad de ser elegido. Se asigna un número a cada individuo y se seleccionan al azar (por ejemplo, usando funciones como `df.sample()` en Python).
* **Sistemático:** Se elige un punto de partida de forma aleatoria y luego se selecciona cada $k$-ésimo elemento de una lista ordenada de la población (donde $k = \text{Población} / \text{Muestra}$).
* **Estratificado:** La población se divide en subgrupos homogéneos llamados "estratos" (por ejemplo, clasificar por rangos de edad o sexo). Luego, se toma una muestra aleatoria simple de cada estrato para asegurar que todos los grupos estén justamente representados.
* **Por Conglomerados:** Se utiliza cuando la población ya está dividida naturalmente en grupos o "conglomerados" heterogéneos (por ejemplo, escuelas o estados geográficos). Se seleccionan algunos conglomerados al azar y se analiza a todos los individuos dentro de ellos.

#### 2. Muestreo NO Probabilístico
La selección de los elementos no depende de la probabilidad, sino del criterio del investigador o de las condiciones de la investigación. No permite hacer generalizaciones estadísticas exactas sobre la población.

* **Por Conveniencia:** Los elementos se seleccionan porque están fácilmente disponibles para el investigador (por ejemplo, encuestar solo a los pacientes que asisten a un hospital específico en un turno).
* **Por Juicio (o Intencional):** El investigador utiliza su experiencia y conocimiento experto para seleccionar una muestra que considera representativa o útil para el estudio.
* **Bola de Nieve:** Se localiza a algunos individuos con características específicas, y estos se encargan de reclutar o recomendar a otros sujetos de su círculo social. Es ideal para poblaciones de difícil acceso.

---

### B. Teorema del Límite Central (TLC)

#### Explicación del Teorema
El Teorema del Límite Central es uno de los pilares fundamentales de la estadística inferencial. Establece que, si se toman muestras aleatorias repetidas de tamaño $n$ de cualquier población (sin importar si la población original es uniforme, asimétrica o exponencial), a medida que el tamaño de la muestra ($n$) se vuelve lo suficientemente grande (generalmente $n \ge 30$), la **distribución de las medias muestrales se aproximará a una distribución normal (Campana de Gauss)**.

La media de esta nueva distribución de medias será igual a la media de la población original ($\mu_x = \mu$), y su desviación estándar (llamada error estándar) será igual a:

$$\sigma_x = \frac{\sigma}{\sqrt{n}}$$

#### Importancia para la Inferencia Estadística
La inferencia estadística busca deducir las características de una población gigante a partir del estudio de una muestra pequeña. El TLC es vital porque:
1. Permite aplicar las propiedades de la **Distribución Normal** (como el cálculo de valores $Z$, intervalos de confianza y pruebas de hipótesis) a poblaciones cuya forma original desconocemos por completo.
2. Garantiza que las medias calculadas a partir de muestras grandes van a estar agrupadas muy cerca de la verdadera media de la población, permitiendo hacer estimaciones con un margen de error matemáticamente controlado.

---

### C. Distribución Muestral de la Media

La **distribución muestral de la media** es la distribución de probabilidad de todas las medias posibles que se podrían calcular a partir de muestras del mismo tamaño extraídas de una población. 

#### Relación con el Teorema del Límite Central
La relación es directa y de dependencia absoluta: la distribución muestral de la media es el "objeto" o fenómeno de estudio, mientras que el **Teorema del Límite Central es la regla matemática que describe su comportamiento**. 

Sin el TLC, no sabríamos qué forma tiene la distribución muestral de la media si la población original fuera asimétrica; gracias al TLC, sabemos con certeza matemática que si el tamaño de muestra es grande, esa distribución adoptará una forma perfectamente simétrica y normal. Esto es justamente lo que justifica que en la Celda 6 de nuestro código hayamos podido modelar el comportamiento de los contagios por estado usando una distribución normal.
## 3. Contenido del Análisis e Interpretación Descriptiva

A partir de la carga y el procesamiento masivo de los registros utilizando la infraestructura de Google Drive conectada a Python (`pandas`), se obtienen las siguientes interpretaciones estructuradas sobre el comportamiento de la base de datos de salud:

### Clasificación y Flujo de Pacientes
1. **Resultado de las Pruebas:** Los datos discriminan con precisión matemática el volumen total de casos positivos, negativos y aquellos que permanecieron pendientes de resultado mediante la columna `RESULTADO_ANTIGENO`. Esta separación inicial permite delimitar el universo de estudio únicamente a los pacientes con diagnóstico confirmado para los análisis subsecuentes.
2. **Tipo de Paciente (Hospitalizados vs. Ambulatorios):** El gráfico circular (*pie chart*) revela la proporción crítica del impacto hospitalario. Un porcentaje mayoritario de pacientes ambulatorios sugiere un manejo sintomático domiciliario, mientras que la fracción hospitalizada representa de forma directa la tasa de severidad y saturación del sistema de salud durante el periodo evaluado.
3. **Condiciones Especiales y Demografía:** Se cuantificó de manera exacta la cantidad de pacientes que se encontraban en estado de embarazo, así como la representatividad de la población indígena dentro del conjunto de datos. Estos indicadores descriptivos permiten evaluar la vulnerabilidad y el impacto del virus en sectores específicos de la población.

### Visualizaciones y Tendencias Observadas
* **Distribución Geográfica (Gráfico de Barras Horizontal):** Permite ordenar de mayor a menor los estados con mayor carga epidemiológica mediante la variable `ENTIDAD_NAC`, facilitando la identificación visual de las regiones que fungieron como epicentros de la pandemia.
* **Distribución de Edad (Histograma con KDE):** Muestra donde se concentra la mayor frecuencia de contagios. La curva de densidad permite observar el sesgo de la distribución hacia las edades adultas y jóvenes.
* **Evolución Temporal (Gráfico de Líneas):** Registra los picos epidemiológicos (olas de contagio) a lo largo del tiempo, mapeando con precisión los momentos de mayor ingreso hospitalario a través de la columna de series temporales `FECHA_INGRESO`.
* **Distribución por Sexo (Barras Apiladas):** Evalúa la relación de concordancia simultánea entre el sexo del paciente y el resultado de su prueba de antígeno, permitiendo concluir si existía una mayor tasa de positividad diferencial.
* **Comorbilidades Crónicas (Gráfico de Barras):** Identifica cuáles patologías previas (como Hipertensión, Diabetes u Obesidad) se presentaron con mayor frecuencia absoluta evaluando los registros afirmativos (`'Si'`) en la población afectada.

---

##  4. Análisis de Probabilidades por Comorbilidad

Para cuantificar el impacto de las condiciones preexistentes en los pacientes confirmados, se aplicaron los principios fundamentales de la teoría de la probabilidad:

1. **Probabilidad Simple :**
   Calculada mediante el cociente del total de individuos que presentan una comorbilidad específica ($n$) entre el total general de registros de la base de datos ($N$).
   
   $$P(\text{Comorbilidad}) = \frac{\text{Total de casos con la comorbilidad}}{\text{Total general de registros}}$$
   
   *Interpretación:* Este valor representa la prevalencia base de enfermedades crónicas en la población evaluada. Nos dice qué tan común es encontrar a un paciente con Diabetes o Hipertensión dentro del espectro completo del histórico de datos.

2. **Probabilidad Condicional :**
   Determina la probabilidad de que un paciente posea una comorbilidad dado que pertenece a una entidad federativa de nacimiento en particular.
   
   $$P(\text{Comorbilidad} \mid \text{Estado}) = \frac{\text{Casos con la comorbilidad en ese Estado}}{\text{Total de casos registrados en ese Estado}}$$
   
   *Interpretación:* Esta métrica es fundamental para el análisis de salud pública regional, ya que demuestra que la vulnerabilidad de un paciente no es homogénea en todo el país. Las variaciones en los porcentajes condicionales reflejan disparidades geográficas en la salud de la población, hábitos alimenticios regionales y la distribución de factores de riesgo por estado.

---

## 5. Ejercicio Práctico de Distribución Normal

**Enunciado:** En un análisis de casos positivos de COVID por estado, el número de casos sigue una distribución normal con una media ($\mu$) de $2360$ casos y una desviación estándar ($\sigma$) de $714$ casos. Se busca calcular la probabilidad de que un estado seleccionado al azar registre entre $2000$ y $3000$ casos positivos.

**Planteamiento Matemático:**
Se desea calcular: 

$$P(2000 \le X \le 3000)$$

### Paso 1: Estandarización a valores de la variable Normal Estándar 
Para transformar la variable original $X$ a la distribución estándar $Z \sim N(0,1)$, aplicamos la fórmula de estandarización $Z = \frac{X - \mu}{\sigma}$:

* **Para el límite inferior ($X_1 = 2000$):**
  
  $$Z_1 = \frac{2000 - 2360}{714} = \frac{-360}{714} \approx -0.5042$$

* **Para el límite superior ($X_2 = 3000$):**
  
  $$Z_2 = \frac{3000 - 2360}{714} = \frac{640}{714} \approx 0.8964$$

De este modo, la probabilidad original se reescribe en términos de $Z$:

$$P(-0.5042 \le Z \le 0.8964)$$

### Paso 2: Cálculo de áreas bajo la curva utilizando la distribución acumulada (CDF)
Utilizando las funciones de densidad acumulada correspondientes (`scipy.stats.norm.cdf`):

* Área acumulada hasta el límite superior: 
  
  $$P(Z \le 0.8964) \approx 0.8150$$

* Área acumulada hasta el límite inferior: 
  
  $$P(Z \le -0.5042) \approx 0.3071$$

### Paso 3: Resta de áreas para obtener el intervalo
El área de la región encerrada entre ambos puntos críticos se obtiene restando el área menor de la mayor:

$$P(-0.5042 \le Z \le 0.8964) = 0.8150 - 0.3071 = 0.5079$$

### Interpretación Estadística del Ejercicio
El resultado matemático arroja un valor de **0.5079** (o **50.79%**). Esto significa que existe una probabilidad del **50.79%** de que cualquier entidad federativa tomada al azar registre un volumen de casos positivos situado en el rango de 2000 a 3000 casos. Al ser un porcentaje superior a la mitad del espacio probabilístico, se infiere que este intervalo abarca la zona de mayor densidad y comportamiento típico de la muestra, estando fuertemente influenciado por la proximidad de los límites respecto a la media de la distribución.

---

##  6. Conclusiones Generales del Proyecto
El desarrollo de este análisis masivo permitió constatar el poder de la estadística descriptiva e inferencial en la interpretación de fenómenos complejos de salud pública. A través de las visualizaciones y los modelos probabilísticos, se concluye que el impacto del virus estuvo profundamente ligado a las variables demográficas y clínicas de los pacientes. La presencia de comorbilidades altera drásticamente el perfil del paciente, y la distribución normal calculada para los estados demuestra que, a pesar de la dispersión de datos geográficos, los fenómenos biológicos masivos tienden a seguir patrones matemáticos predecibles y estables.

---

##  Conclusión Personal

**Iveth Santacruz**
> El desarrollo de este proyecto final consolidó de manera práctica los conceptos teóricos revisados a lo largo del semestre. La experiencia de migrar de cálculos manuales a Python en Google Colab demostró la verdadera utilidad de la estadística al manejar bases de datos con millones de registros. Automatizar el cálculo de probabilidades condicionales y modelar distribuciones normales mediante librerías como `pandas` y `scipy.stats` me brindó una perspectiva real de cómo la ingeniería y el análisis de datos se complementan para la resolución de problemas reales y el procesamiento de información a gran escala.

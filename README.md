# Análisis Predictivo en Counter-Strike: Global Offensive (CS:GO)

---

Este proyecto de Machine Learning se enfoca en el análisis y modelado predictivo de datos de partidas de Counter-Strike: Global Offensive (CS:GO). Nuestro objetivo principal es predecir el resultado de las rondas (`RoundWinner`) para contribuir al balanceo del juego, utilizando un dataset de más de 7000 partidas.

---

## 🎮 Contexto del Negocio

Valve, la compañía desarrolladora de CS:GO, nos contactó como equipo de análisis de datos y modelado de Machine Learning para explorar y crear modelos predictivos a partir de datos del juego.

En CS:GO, dos equipos de cinco jugadores, Terroristas (T) y Contra-Terroristas (CT), se enfrentan en cada partida. El objetivo de los Terroristas es plantar una bomba en uno de los sitios específicos del mapa y defenderla hasta que explote. Los Contra-Terroristas, por su parte, deben evitar que la bomba sea plantada o desactivarla si ya ha sido colocada.

Los datos utilizados provienen de más de 7000 partidas, con un máximo de 10 jugadores por partida. Estos datos fueron extraídos de "replays", archivos propietarios que contienen información detallada de cada acción de los jugadores. Se pre-procesaron y se consolidaron en un archivo CSV con 79.157 filas, donde cada fila representa a un jugador dentro de una partida, y 29 columnas que describen sus acciones.

### 🎯 Objetivo del Proyecto

El objetivo principal es **predecir el ganador de la ronda (`RoundWinner`)** basándose en las dinámicas de juego, buscando un equilibrio en el juego y proporcionando insights valiosos.

### 💡 Hipótesis Consideradas

Durante la fase de **Business Understanding**, planteamos varias hipótesis para guiar nuestro análisis y modelado:

* **Hipótesis 1: Más kills = mayor probabilidad de ganar.** Se postula que eliminar a los oponentes de manera efectiva aumenta las probabilidades de victoria al controlar el mapa y asegurar los objetivos.
* **Hipótesis 2: Mapas como `de_inferno` favorecen a los CTs.** Observaciones previas y la estructura de ciertos mapas sugieren una ventaja táctica para los Contra-Terroristas debido a diseños defensivos clave.
* **Hipótesis 3: Equipamiento costoso mejora la tasa de victorias.** Se espera que una mejor economía y acceso a equipamiento superior (rifles, chalecos, granadas) se traduzca directamente en un mayor `win rate`.

### 📊 Métricas de Éxito (KPIs)

Para evaluar el éxito de nuestros modelos, establecimos los siguientes KPIs:

* **Precisión del Modelo:** Aspiramos a que el modelo tenga una precisión superior al $70\%$ en sus predicciones.
* **Balance del Juego:** Que el modelo contribuya a un balance donde ambos equipos ganen entre el $45\%$ y el $55\%$ de las rondas, evitando desequilibrios significativos.
* **Correlación:** Que variables como `RoundKills` y `RoundHeadshots` muestren una correlación clara con el resultado de la ronda.

---

## 🚀 Nuestro Enfoque Paso a Paso

Para lograr nuestros objetivos, seguimos una metodología estructurada, abarcando las fases clave del ciclo de vida de un proyecto de Machine Learning:

### 1. Entendimiento del Negocio (Business Understanding)

* Definición del problema de negocio y objetivos.
* Identificación de contexto y datos relevantes.
* Formulación de hipótesis para modelos de regresión y clasificación.
* Establecimiento de KPIs para evaluar el rendimiento.

### 2. Entendimiento de los Datos (Data Understanding)

* Identificación de tipos de variables y atributos.
* Detección y análisis de valores nulos y `outliers`.
* Realización de análisis estadísticos básicos.
* Creación de matrices de correlación para identificar patrones.
* Detección de patrones y comportamientos en los datos.
* Ingeniería de nuevas variables a partir del análisis.

### 3. Preparación de los Datos (Data Preparation)

* Transformación de variables categóricas a numéricas (Encoding).
* Tratamiento de valores nulos.
* Manejo de `outliers`.
* Normalización o estandarización de datos (Escalamiento).

### 4. Modelado (Modeling)

Exploramos un amplio rango de modelos de Machine Learning, dividiéndolos en tareas de **regresión** y **clasificación** para abordar diferentes aspectos de nuestras hipótesis. Para cada modelo, realizamos:

* Selección de variables (X/Y).
* División de datos en conjuntos de entrenamiento y prueba (`Train/Test Split`).
* Ajuste de hiperparámetros.
* Aplicación de modelos y generación de predicciones.
* Obtención de métricas de rendimiento.

**Modelos de Regresión Explorados:**

* Regresión Lineal
* Support Vector Regression (SVR)
* Decision Tree Regressor
* Random Forest Regressor
* KNN Regressor

**Modelos de Clasificación Explorados:**

* Regresión Logística
* Support Vector Classification (SVC)
* Árbol de Clasificación
* Random Forest Classifier
* KNN Classifier

*Nota: También se consideró la posibilidad de Modelos de Clustering, aunque el enfoque principal fue en regresión y clasificación dadas las hipótesis planteadas.*

### 5. Evaluación (Evaluation)

En esta fase, analizamos las métricas obtenidas de cada modelo y cada hipótesis:

* **Métricas Clave:** Matriz de Confusión, $R^2$, RMSE, entre otras.
* Análisis detallado de cada hipótesis para modelos de regresión y clasificación.
* Identificación de oportunidades de mejora en el pre-procesamiento o en los modelos.

### 6. Despliegue (Deployment)

Una vez seleccionados los modelos con mejor rendimiento y justificación, se preparan para un posible despliegue.

* **Modelo de Regresión Final:** Regresión Lineal (para Hipótesis 1)
* **Modelo de Clasificación Final:** Random Forest Classifier (RFC) (para Hipótesis 2)

---

## 🛠️ Justificación de Modelos Finales

Tras un exhaustivo proceso de modelado y evaluación, seleccionamos los siguientes modelos como los más adecuados para abordar nuestras hipótesis, basándonos en su rendimiento y la interpretación de sus resultados:

### **Modelo de Regresión: Regresión Lineal (Hipótesis 1)**

Nuestra Hipótesis 1 buscaba determinar si "más kills es igual a más probabilidad de ganar". Aunque la hipótesis original se centraba en la victoria general, el análisis profundo nos llevó a enfocar el modelo de regresión en predecir `MatchKills` basándose en otras métricas de rendimiento individual como `MatchAssists` y `MatchHeadshots`.

Tras evaluar a fondo los cinco algoritmos distintos en nuestro dataset de CS:GO, llegamos a la conclusión contundente de que la **Regresión Lineal es el modelo que mejor predice `MatchKills`**, dado que ostenta el $R^2$ más elevado, un $0.754$.

**¿Por qué la Regresión Lineal resultó ser el mejor modelo?**

La Regresión Lineal mostró una habilidad sobresaliente para plasmar las relaciones no lineales complejas que son propias del gameplay en CS:GO. A diferencia de Random Forest, que asume relaciones directamente proporcionales, la Regresión Lineal puede modelar patrones más sofisticados entre nuestras variables predictoras (`MatchAssists`, `MatchHeadshots`) y `MatchKills`. En Counter-Strike, la dinámica del juego es intrínsecamente intrincada. Un jugador con muchas asistencias no siempre tendrá kills proporcionales, ya que esto depende del rol del jugador (support vs entry fragger), la coordinación del equipo y las situaciones tácticas específicas.

**Análisis Comparativo del Rendimiento de Modelos de Regresión:**

* **Regresión Lineal:** $R^2 = 0.754$ - El ganador indiscutible. Además, al considerar la relación `Headshots` vs `Kills`, mostró un $R^2=0.72$ y $MSE=3.1$, confirmando que los headshots son un buen predictor de kills, aunque con errores en valores extremos (más de 30 kills).
* **Random Forest:** $R^2 = 0.752$ - Buen rendimiento, pero un poco inferior.
* **Decision Tree:** $R^2 = 0.749$ - Propenso al overfitting. En el caso de `Headshots`, obtuvo un $R^2=0.73$ pero con alta varianza en predicciones extremas, sugiriendo que necesita mayor profundidad para capturar patrones complejos.
* **SVM:** $R^2 = 0.744$ - Sensible a los valores atípicos. Al evaluar `Equipamiento` vs `Kills` con SVR, se obtuvo un bajo desempeño ($R^2=0.0046$), demostrando que el valor del equipamiento no influye significativamente en las kills obtenidas.
* **KNN:** $R^2 = 0.726$ - El más bajo, también sensible a los valores atípicos.

**Interpretación Práctica de los Resultados:**

El $R^2$ de $0.754$ implica que nuestro modelo de Regresión Lineal explica aproximadamente el $75.4\%$ de la variabilidad en las eliminaciones de una partida. Esto es extraordinariamente sólido, sobre todo teniendo en cuenta la naturaleza intrínsecamente impredecible de CS:GO, donde factores como el timing perfecto, decisiones en fracciones de segundo y elementos de azar también influyen de forma importante.

**Robustez del Modelo:**

Con este modelo, podemos predecir con aproximadamente un $75\%$ de certeza cuántas eliminaciones obtendrá un jugador basándonos en sus asistencias esperadas, precisión de headshots y el valor del equipamiento inicial de su equipo. Esto tiene aplicaciones valiosas para análisis táctico, coaching y estrategias de equipo.

### **Modelo de Clasificación: Random Forest Classifier (Hipótesis 2)**

Nuestra Hipótesis 2 planteaba que "Mapas como `de_inferno` favorecen a los CTs". Sin embargo, durante el proceso de modelado, la exploración más profunda nos llevó a enfocar el modelo de clasificación en **predecir la supervivencia (`Survived`)** basándose en el `TeamStartingEquipmentValue`, que es una variable crucial para las decisiones tácticas del juego.

Después de evaluar minuciosamente los cinco algoritmos de clasificación para predecir la supervivencia en CS:GO basándose en el valor de equipamiento inicial del equipo (`TeamStartingEquipmentValue`), podemos determinar que **Random Forest Classifier es el modelo superior, obteniendo la Accuracy más alta de $60.14\%$**.

**¿Por qué Random Forest resultó ser el mejor modelo?**

Random Forest demostró ser el algoritmo más robusto para este problema de clasificación binaria tan desafiante. La supervivencia en CS:GO es inherentemente compleja y depende de múltiples factores más allá del equipamiento inicial, pero Random Forest logró extraer los patrones más significativos de esta única variable predictora. El modelo utilizó 50 árboles de decisión (`n_estimators=50`) con una profundidad máxima de 5 niveles, lo que le permitió capturar relaciones no lineales sin caer en overfitting. Esta configuración optimizada mediante validación cruzada demostró que el algoritmo puede balancear efectivamente entre bias y varianza, crucial cuando trabajamos con una sola característica predictora.

**Análisis Comparativo de Rendimiento de Modelos de Clasificación:**

* **Random Forest:** Accuracy = $60.14\%$ - El claro ganador.
* **KNN (k=20):** Accuracy = $59.8\%$ - Muy cercano, pero ligeramente inferior.
* **Regresión Logística:** Accuracy = $59.08\%$ - Sólido pero limitado por su linearidad. Al predecir `Supervivencia`, obtuvo un Accuracy=$67\%$ ($F1=75\%$ para no-supervivientes, $52\%$ para supervivientes). Mejoró con ajustes pero aún tiene un `recall` bajo ($45\%$) para la clase positiva.
* **Árbol de Clasificación:** Accuracy = $55\%$ - Vulnerable al overfitting con una sola variable. Para predecir `Headshots`, obtuvo un Accuracy=$60\%$ pero falló totalmente en predecir supervivientes (`recall=0\%`), evidenciando que los headshots no son predictores suficientes por sí solos para la supervivencia.
* **SVM (Kernel Lineal):** Accuracy = $62.6\%$ con un `recall` críticamente bajo ($21.6\%$) para supervivientes, indicando que las variables usadas (flanqueo, equipamiento) no son determinantes por sí solas. Requirió tiempos de entrenamiento significativamente mayores.

**Interpretación Detallada de los Resultados:**

La accuracy de $60.14\%$ puede parecer modesta, pero es importante contextualizar este resultado. Estamos intentando predecir supervivencia usando únicamente el valor de equipamiento inicial del equipo, lo cual es una tarea extremadamente desafiante. En CS:GO, la supervivencia depende de factores como habilidad individual, `positioning`, decisiones tácticas, `timing`, y hasta elementos de suerte que no están capturados en esta variable.

**Análisis del Reporte de Clasificación (Random Forest):**

* **Precision para "False" (No Sobrevivió):** $0.61$ - El modelo identifica correctamente el $61\%$ de las muertes predichas.
* **Recall para "False":** $0.91$ - Captura el $91\%$ de todas las muertes reales, excelente sensibilidad.
* **F1-Score para "False":** $0.73$ - Balance sólido entre precision y recall.
* **Precision para "True" (Sobrevivió):** $0.52$ - Más desafiante predecir supervivencia.
* **Recall para "True":** $0.15$ - Solo captura el $15\%$ de las supervivencias reales.

**Hallazgos Clave Adicionales:**

* Las habilidades individuales (`headshots`) predicen mejor el rendimiento (`kills`) que factores de equipamiento.
* Ningún modelo actual predice efectivamente la supervivencia (todos tienen `recall` < $50\%$ para esta clase).
* El desbalance de clases afecta significativamente los modelos de clasificación.

**Qué nos dice esto sobre el comportamiento del modelo:**

El modelo es significativamente mejor prediciendo muertes que supervivencias. Esto tiene sentido lógico: equipos con menor valor de equipamiento inicial tienden a tener mayores probabilidades de muerte, una relación más directa y predecible. La supervivencia, por otro lado, puede ocurrir incluso con equipamiento básico debido a factores externos no capturados.

**Robustez y Optimización:**

El `split` óptimo de $0.3$ ($30\%$ para `testing`) aseguró suficientes datos para entrenamiento mientras mantenía una evaluación robusta. Los hiperparámetros optimizados (`max_depth=5`, `criterion='gini'`) previenen el `overfitting`, crucial cuando trabajamos con datasets de CS:GO que pueden tener patrones complejos.

**Implicaciones Prácticas:**

Con este modelo, los equipos pueden estimar con aproximadamente $60\%$ de precisión las probabilidades de supervivencia basándose en su inversión inicial en equipamiento. Esto es valioso para decisiones económicas estratégicas: ¿vale la pena hacer "force-buy" o es mejor una "eco round"?

A continuación, se muestran los gráficos que respaldan visualmente estos hallazgos y demuestran la superioridad del modelo Random Forest para esta tarea de clasificación.

*(Aquí puedes insertar la tabla resumen de las 3 hipótesis de clasificación si la tienes en formato imagen o texto.)*

---

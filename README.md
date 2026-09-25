# Perfil-Exportador-de-Santa-Fe
LIMPIEZA Y TRANSFORMACIÓN DE DATOS

Perfil exportador de empresas santafesinas


**Contexto del proyecto**

El proyecto se centra en la preparación y transformación de datos de comercio exterior para construir una base confiable de exportaciones de empresas santafesinas. Los datos de origen provienen de archivos Excel descargados de Softrade y presentan inconsistencias de localidad, nombres de empresas, codificación de caracteres y registros que requieren validación antes de ser utilizados para análisis.

**OBJETIVO DEL PROYECTO**
Construir una base de datos consolidada, limpia y consistente de las exportaciones de empresas santafesinas, aplicando procesos reproducibles de filtrado, validación y transformación para habilitar su análisis y visualización en Power BI.

**MI ROL**
Equipo tecnico responsable del proceso de limpieza y transformación de datos: descarga y preparación de archivos, filtrado de empresas santafesinas, normalización de información, control de duplicados e inconsistencias y generación de la base final para análisis.

**PREGUNTA DE NEGOCIO**
¿Cuál es el perfil exportador de las empresas santafesinas y qué características de sus exportaciones pueden identificarse a partir de la información de comercio exterior?


**Herramientas utilizadas**
- Python — filtrado, normalización y consolidación de archivos.
- pandas — manipulación y transformación de datos tabulares.
- unidecode — normalización de texto y caracteres especiales.
- openpyxl — lectura y escritura de archivos Excel.
- Excel — revisión y validación manual de la base consolidada.
- Power BI — generación de indicadores y visualizaciones a partir de la base final.

**Proceso de trabajo**

**1. Preparación de los datos**
Una vez descargados los archivos de Softrade, se definió un flujo de procesamiento mediante dos notebooks de Python ejecutados desde Visual Studio Code. El objetivo fue reducir el universo de registros hasta identificar las operaciones correspondientes a empresas santafesinas.
Los notebooks requieren Python 3.x, Visual Studio Code con las extensiones de Python y Jupyter, y las librerías pandas, unidecode y openpyxl.

**2. Filtrado por localidad**
El primer notebook recorre los archivos descargados y conserva las filas cuya columna Localidad corresponde a Santa Fe. Para evitar pérdidas de información, se contemplan variantes de escritura y problemas de codificación, como tildes mal interpretadas.
Definición de las localidades válidas y de un diccionario de normalización.
Lectura de los archivos Excel numerados.
Conversión de la columna Localidad a mayúsculas.
Normalización de variantes de escritura.
Filtrado de registros correspondientes a Santa Fe.
Consolidación de los resultados en Base_Unificada_localidad.xlsx.

**3. Corrección de localidades**
El filtrado por localidad no resulta suficiente en todos los casos: algunas empresas exportadoras que operan desde Santa Fe tienen registrada otra localidad en Softrade, por ejemplo, la correspondiente a su casa central. Para resolver estos casos se utiliza un archivo auxiliar, Empresas modificadas.xlsx, con la correspondencia entre exportador y localidad correcta.
La base actualizada se guarda como Exportaciones_actualizadas.xlsx, con un nombre que puede adaptarse al período analizado. El archivo auxiliar debe revisarse y actualizarse periódicamente.

**4. Filtrado por empresa**
El segundo notebook complementa el filtrado anterior utilizando una lista validada de empresas exportadoras santafesinas. Este enfoque permite recuperar registros cuando la localidad está mal cargada o presenta inconsistencias.
Construcción de una lista manual de empresas exportadoras santafesinas.
Inclusión de variantes de razón social y errores tipográficos.
Normalización del nombre del exportador.
Filtrado de los archivos de origen.
Consolidación en Base_perfil_exportador.xlsx.

**5. Cruce y validación de resultados**
Los dos métodos de filtrado se utilizan de manera complementaria. El filtrado por localidad permite obtener una cobertura amplia, mientras que el filtrado por empresa aporta mayor precisión en los casos en que la información de localidad presenta errores.
Antes de avanzar con el análisis, se comparan ambas salidas para detectar inconsistencias y evitar duplicaciones, especialmente cuando una misma empresa aparece en ambas bases.

**6. Transformación de datos**
Una vez consolidada la información, se realiza una revisión manual del archivo para garantizar la calidad de las variables utilizadas en el análisis.
Control de duplicados entre las bases filtradas por localidad y por empresa.
Construcción de la variable Sector a partir de los primeros dos dígitos del nomenclador Mercosur.
Clasificación de los productos en las categorías Primario, MOI, MOA y Energía, siguiendo la clasificación utilizada por INDEC. Lo cual se logro a partir del siguiente código:

Control de completitud de las variables clave: Exportador, Localidad, Mes, Rubro NCM, País de destino, Valor FOB USD, Vía de transporte y Aduana de salida.
Para ello, dessarollamos script como el siguiente:
Eliminación de registros evidentemente erróneos o incompletos.
Homogeneización de nombres de países y rubros.
Creación de filtros y variables de apoyo para el análisis y la visualización en Power BI.

**Resultado**
El proceso genera una base consolidada y validada que funciona como fuente única de verdad para los indicadores y visualizaciones posteriores. Entre otros usos, la base permite analizar el valor de las exportaciones por empresa y período, además de segmentar la información por sector, rubro, destino, transporte y aduana de salida.

**Valor para el negocio**
La principal contribución del proyecto es transformar archivos de origen heterogéneos en una fuente de datos estructurada y reutilizable. Esto reduce el trabajo manual posterior, mejora la consistencia de los indicadores y facilita que la información de comercio exterior pueda ser utilizada para generar reportes y apoyar la toma de decisiones.

**Flujo resumido**
Softrade → Python → Filtrado por localidad + Filtrado por empresa → Validación y deduplicación → Transformación → Base consolidada → Power BI


# Encuesta de salarios Ask a Manager 2021💼📈

Este repositorio contiene el modelado de datos y visualización del conjunto de datos recolectados por “Ask a Manager”. La información corresponde a sueldos que tienen profesionales en diferentes disciplinas (principalmente en Estados Unidos). La información se recolecta mediante el [formulario](https://www.askamanager.org/2021/04/how-much-money-do-you-make-4.html) y los dato se almacenan en el siguiente [enlace](https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792 ).



 


## Documentación modelado


1. Variables en la base de datos original

| Variable            | Descripción                                                                                                           | Tipo de Dato   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|----------------|
| **Timestamp**          | Fecha en que se diligencio la encuesta                                                         | `date`     |
| **How old are you?**          | Edad (categorías: under 18, 18-24, 25-34, 45-54, 35-44, 65 or over, 55-64)                                                        | `category`     |
| **What industry do you work in?**          | Industria en la que trabaja                                                          | `category`     |
| **Job title?**          | Titulo profesional                                                          | `category`     |
| **If your job title needs additional context, please clarify here:**          | Información detallada sobre su titulo profesional                                                          | `category`     |
| **What is your annual salary?**          | Salario anual                                                          | `category`     |
| **How much additional monetary compensation do you get**          | Compensaciones adicionales recibidas al año                                                          | `category`     |
| **Please indicate the currency**          | Tipo de moneda                                                          | `category`     |
| **If "Other," please indicate the currency here:**          | Otro tipo de moneda                                                          | `string`     |
| **If your income needs additional context, please provide it here:**          | Contexto sobre los ingresos                                                          | `string`     |
| **What country do you work in?**          | País donde trabaja                                                          | `string`     |
| **If you're in the U.S., what state do you work in?**          | Estado para el caso de Estados Unidos                                                         | `string`     |
| **What city do you work in?**          | Ciudad donde trabaja                                                          | `string`     |
| **How many years of professional work experience do you have overall?**          | Años de experiencia laboral durante toda su vida laboral (categorías: 1 year or less, 2 - 4 years, 5-7 years, 8 - 10 years, 11 - 20 years, 21 - 30 years, 31 - 40 years, 41 years or more)                                                        | `category`     |
| **How many years of professional work experience do you have in your field?**          | Años de experiencia laboral en su campo laboral laboral                                                         | `category`     |
| **What is your highest level of education completed?**          | Nivel de educación más alto completado (categorías: College degree, High School, Master's degree, PhD, Professional degree (MD, JD, etc.), Some college)                                                        | `category`     |
| **What is your gender?**          | Género (categorías: Woman, Man, Non-binary, Other or prefer not to answer, Prefer not to answer)                                                         | `category`     |
| **What is your race?**          | Raza                                                         | `category`     |

2. Variables luego del modelado

| Variable            | Descripción                                                                                                           | Tipo de Dato   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|----------------|
| **edad**          | Edad                                                         | `category`     |
| **industria**          | Industria en la que trabaja                                                         | `category`     |
| **titulo_profesional**          | Titulo profesional                                                         | `category`     |
| **moneda_agg**          | Moneda estandarizada (para la categoría de Otros)                                                         | `category`     |
| **pais**          | País estandarizado                                                         | `category`     |
| **ciudad**          | Ciudad estandarizada                                                         | `category`     |
| **años_experiencia_total**          | Años de experiencia laboral durante toda su vida laboral (mismas categorías)                                                         | `category`     |
| **años_experiencia_industria**          | Años de experiencia laboral en su campo laboral (mismas categorías)                                                         | `category`     |
| **nivel_educacion**          | Nivel de educación más alto completado (mismas categorías)                                                         | `category`     |
| **genero**          | Género (mismas categorías)                                                         | `category`     |
| **raza**          | Raza                                                         | `category`     |
| **salario_anual_cop**          | Salario anual convertido a COP                                                         | `float`     |
| **compensaciones_cop**          | Compensaciones recibidas convertido a COP                                                         | `float`     |
| **salario_total_cop**          | Salario total (salario anual y compensaciones) convertido a COP                                                         | `float`     |

3. Paso a paso para la actualización y modelado de datos


En el [Notebook Modelado de datos](https://github.com/soniakolaya/Encuesta_salarios/blob/main/Modelado_datos.ipynb) se encuentra el código en Python pdel proceso que se va a detallar a continuación:

**Cargue:** Se inicia cargando el conjunto de datos (raw data) de la encuesta. Estos datos son descargados en formato csv del [enlace](https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792 ). Los datos se almacenaron en la carpeta *data*.

**Limpieza:** 
- En primer lugar se cambian los nombres de las columnas de dataframe donde se cargaron los datos para una mejor manipulación y entendimiento. 
- Se realiza una vista general de los datos para conocer el número de registros no nulos por columna. 
- Se cambia el tipo de datos a las variables *salario_anual* y *compensaciones* para la conversión a COP. 
- Se rellenan los valores nulos de las variables *genero*, *titulo_profesional*, y *nivel_educacion*.
- Se crean las funciones *estandarizar_ciudad(nombre)* y *estandarizar_pais(nombre)* para estandarizar los valores de *pais* y *ciudad*, dado que estas variables en el formulario son abiertas, tenian muchos errores.
- Se crea la función *estandarizar_otra_moneda(moneda)* para estandarizar los tipos de moneda almacenados en la categoría otros.
- Se crea una función *convertir_a_cop(monto,moneda)* que permite convertir un monto de dinero a una moneda, en este caso a COP. 

**Creación nuevas variables**
- Se crea las nuevas variables *salario_anual_cop* y *compensaciones_cop* mediante la conversión de los valores a pesos colombianos.
- Se crea la variable *salario_total_cop* como la suma de *salario_anual_cop* y *compensaciones_cop*.

Finalmente se guarda en la carpeta *data* la base limpia y se exporta al LookerStudio para la creación del dashboard.
## Tablero interactivo

[Ver reporte en Looker Studio](https://lookerstudio.google.com/s/nfEWA6ylDn4)


<iframe width="600" height="400" src="https://lookerstudio.google.com/reporting/xxxxx" frameborder="0" allowfullscreen></iframe>



## Autores

- Sonia Olaya: [sk.olaya@uniandes.edu.co](sk.olaya@uniandes.edu.co)


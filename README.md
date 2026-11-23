# Proyecto ConnectaTel -- Análisis de usuarios

## Objetivo del proyecto

Explorar y analizar los datos de ConnectaTel para comprender el perfil
de sus usuarios y sus patrones de consumo de llamadas y mensajes. El
análisis busca identificar problemas de calidad de datos, describir los
segmentos de clientes y generar conclusiones y recomendaciones que
apoyen decisiones comerciales.

## Datasets utilizados

El proyecto trabaja con los siguientes conjuntos de datos:

-   **`users.csv`**: información de los usuarios, como edad, ciudad y
    fecha de registro.
-   **`usage.csv`**: registros de uso de los servicios, incluyendo el
    tipo de actividad y variables asociadas a llamadas y mensajes.
-   **`plans.csv`**: información de los planes disponibles.

Durante el análisis se crean tablas y columnas derivadas, entre ellas
`user_profile`, que reúne información agregada por usuario. Esta última
es un dataframe generado durante el notebook, no uno de los archivos CSV
originales.

> Los nombres anteriores corresponden a los archivos utilizados en el
> proyecto. Si los archivos tienen otro nombre o ubicación en tu
> entorno, actualiza las rutas de lectura en el notebook.

## Etapas del análisis realizadas

1.  **Carga y exploración inicial**
    -   Carga de los datasets con Pandas.
    -   Revisión de dimensiones, tipos de datos, estadísticas
        descriptivas y valores faltantes.
2.  **Limpieza y preparación**
    -   Revisión de valores centinela, como `-999` en `age`.
    -   Sustitución de valores inválidos, como `"?"` en `city`.
    -   Conversión y validación de fechas en `reg_date`, marcando como
        nulas las fechas fuera del rango establecido (2022--2024).
    -   Análisis de los valores nulos de `duration` y `length` según
        `type`. Se conservaron los nulos cuando el campo no aplica al
        tipo de registro.
3.  **Análisis de valores faltantes y atípicos**
    -   Evaluación de la relación entre los valores faltantes de
        `duration` y `length` y el tipo de actividad.
    -   Visualización de distribuciones mediante histogramas y boxplots.
    -   Cálculo de límites con el método IQR para `cant_mensajes`,
        `cant_llamadas` y `cant_minutos_llamada`.
    -   Conservación de los valores atípicos al no contar con evidencia
        de que fueran errores.
4.  **Agregación y perfilamiento de usuarios**
    -   Agrupación de los registros de uso por `user_id`.
    -   Cálculo de la cantidad de mensajes, cantidad de llamadas y total
        de minutos de llamadas.
    -   Unión de los datos agregados con la información de usuarios para
        construir `user_profile`.
5.  **Análisis estadístico y visualización**
    -   Cálculo de estadísticas descriptivas para variables numéricas.
    -   Revisión de la distribución de la variable categórica `plan`.
    -   Elaboración de histogramas y boxplots para explorar el
        comportamiento de las variables.
6.  **Segmentación de usuarios**
    -   Creación de `grupo_uso`:
        -   **Bajo uso:** menos de 5 llamadas y menos de 5 mensajes.
        -   **Uso medio:** menos de 10 llamadas y menos de 10 mensajes,
            siempre que no pertenezca a Bajo uso.
        -   **Alto uso:** los demás casos.
    -   Creación de `grupo_edad`:
        -   **Joven:** menor de 30 años.
        -   **Adulto:** desde 30 y menor de 60 años.
        -   **Adulto Mayor:** 60 años o más.
    -   Visualización de la cantidad de usuarios en cada grupo.
7.  **Análisis ejecutivo**
    -   Interpretación de los segmentos por edad y nivel de uso.
    -   Identificación de patrones de consumo y valores atípicos.
    -   Elaboración de recomendaciones para la oferta de planes y las
        estrategias de fidelización.

### Librerías

El notebook utiliza principalmente:

-   `pandas` para manipulación y análisis de datos.
-   `numpy` para operaciones numéricas.
-   `matplotlib` para gráficos.
-   `seaborn` para visualizaciones estadísticas.

En Colab, estas librerías suelen estar disponibles. Si alguna falta,
instálala en una celda:

``` python
!pip install pandas numpy matplotlib seaborn
```



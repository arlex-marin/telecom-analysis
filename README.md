# Análisis de Comportamiento de Clientes - ConnectaTel

## Objetivo del Proyecto

Este proyecto analiza el comportamiento de uso de los clientes de ConnectaTel, una empresa de telecomunicaciones con operaciones en México y Colombia. El objetivo es identificar patrones de consumo (llamadas y mensajes), detectar comportamientos atípicos, crear segmentos de clientes y generar recomendaciones comerciales para optimizar la oferta de planes y mejorar la experiencia del usuario.

## Datasets Utilizados

El análisis integra tres fuentes de datos:

**plans.csv** - Catálogo de planes vigentes con columnas: plan_name, price, minutes_included, gb_included, cost_per_extra.

**users_latam.csv** - Información de clientes registrados con columnas: user_id, age, city, plan, reg_date, churn_date.

**usage.csv** - Registro detallado de uso del servicio con columnas: id, user_id, type, duration, length, date.

Periodo de análisis: Datos registrados hasta el año 2024. Total de usuarios: 4,000 clientes. Total de registros de uso: 40,000 transacciones.

## Etapas del Análisis

### Paso 1: Carga y Exploración Inicial
- Carga de los 3 datasets con pandas.
- Revisión de estructura: .shape, .info(), .head().
- Identificación de tipos de datos y posibles inconsistencias.

### Paso 2: Identificación de Problemas de Calidad
- Valores nulos: Conteo y proporción por columna.
- Sentinels detectados: age con valor -999 (edad imposible) y city con valor "?" (categoría desconocida).
- Fechas imposibles: 40 registros con año 2026 en reg_date (año no transcurrido).
- Nulos estructurales: duration y length son MAR (Missing At Random), dependientes de type.

### Paso 3: Limpieza Básica
- Reemplazo de -999 en age por la mediana.
- Reemplazo de "?" en city por NaN.
- Marcado de fechas futuras como NaT.
- Conversión segura de columnas de fecha con pd.to_datetime(errors='coerce').

### Paso 4: Estadísticas de Uso por Usuario
- Agregación de usage por user_id: cant_mensajes, cant_llamadas, cant_minutos_llamada.
- Combinación con users para crear un perfil completo (user_profile).

### Paso 5: Visualización y Detección de Outliers
- Histogramas de age, cant_mensajes, cant_llamadas, cant_minutos_llamada segmentados por plan.
- Boxplots para identificar valores atípicos.
- Método IQR aplicado para cuantificar outliers superiores.

### Paso 6: Segmentación de Clientes
- Grupo de Uso: Bajo uso, Uso medio, Alto uso (basado en llamadas y mensajes).
- Grupo de Edad: Joven (menor a 30), Adulto (30-59), Adulto Mayor (60 o más).
- Visualización: Countplots de cada segmento.

### Paso 7: Insights Ejecutivos
- Diagnóstico de calidad de datos.
- Identificación de segmentos valiosos.
- Interpretación de outliers como oportunidad de negocio.
- Recomendaciones concretas para nuevos planes y estrategias comerciales.

## Cómo Ejecutar el Notebook

### Requisitos previos

Instala las dependencias necesarias con:
pip install pandas numpy matplotlib seaborn jupyter

### Ejecución

1. Clona el repositorio o descarga los archivos del proyecto.
2. Asegúrate de que los datasets estén en la misma carpeta que el notebook: plans.csv, users_latam.csv, usage.csv.
3. Abre el notebook con Jupyter: jupyter notebook connectatel_analysis.ipynb
4. Ejecuta todas las celdas en orden (Kernel, Restart and Run All).

### Estructura del proyecto

connectatel-analysis/
- connectatel_analysis.ipynb (Notebook principal con todo el análisis)
- plans.csv (Datos de planes)
- users_latam.csv (Datos de usuarios)
- usage.csv (Datos de uso)
- README.md (Este archivo)

## Resultados Clave

Usuarios totales: 4,000. Edad promedio: 48.1 años. Mensajes promedio por usuario: 5.5. Llamadas promedio por usuario: 4.5. Minutos promedio por usuario: 23.3. Outliers detectados en minutos: 109 usuarios (2.73%). Plan Básico: 64.9% de usuarios. Plan Premium: 35.1% de usuarios.

## Principales Recomendaciones

1. Plan Intermedio "Plus" para usuarios de uso medio (50% de la base).
2. Plan "Senior" para Adultos Mayores, con más minutos y menos mensajes.
3. Plan "Joven Digital" para menores de 30 años, enfocado en mensajería.
4. Paquete adicional para usuarios de alto consumo (outliers).
5. Rediseñar límites de planes actuales (no generan diferenciación real).

## Autor

Este proyecto fue desarrollado como parte del sprint de análisis de datos para ConnectaTel, aplicando técnicas de limpieza, exploración, visualización y segmentación en Python.

¿Preguntas o sugerencias? Contacta al equipo de datos.

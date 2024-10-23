# Data Lake Project with Amazon S3 and Athena

## Descripción del Proyecto

Este proyecto consiste en la creación de un **Data Lake** utilizando los servicios de **Amazon Web Services (AWS)**, específicamente **Amazon S3** para el almacenamiento de datos y **Amazon Athena** para el procesamiento y consulta de los mismos. El objetivo principal es integrar datos provenientes de diferentes fuentes, como bases de datos relacionales (PostgreSQL) y archivos CSV, para permitir consultas eficientes utilizando SQL sobre grandes volúmenes de datos sin necesidad de infraestructura adicional.

El proyecto incluye la extracción, transformación e integración de los datos en un Data Lake, junto con ejemplos detallados de consultas realizadas sobre los datos integrados.

## Estructura del Proyecto

El proyecto se desarrolla íntegramente en un **notebook**, donde se siguen los siguientes pasos:

1. **Carga de Librerías y Configuración del Entorno**:  
    Se utilizan librerías como `pandas`, `boto3`, y `sqlalchemy`, además de la librería `dotenv` para manejar las credenciales a través de un archivo `.env`. Estas credenciales se utilizan para conectar con PostgreSQL y AWS.

2. **Conexión a la Base de Datos y Extracción de Datos**:  
    Los datos de las tablas `orders` y `products` se extraen desde una base de datos PostgreSQL y se almacenan en DataFrames de `pandas`. Además, se carga un archivo CSV con la tabla `order_details`.

3. **Unificación de los Datos**:  
    Se realiza la integración de las tres tablas (`orders`, `products`, `order_details`) utilizando las llaves foráneas `order_id` y `product_id`, y se guarda el resultado en un archivo CSV llamado `merged_orders.csv`.

4. **Almacenamiento en Amazon S3**:  
    El archivo `merged_orders.csv` se sube a un bucket de **Amazon S3**. Este archivo almacenado en S3 será la fuente de datos que se consultará posteriormente en **Amazon Athena**.

5. **Creación de la Tabla en Athena**:  
    Se utiliza **Amazon Athena** para crear una tabla externa que apunta a los datos almacenados en S3. La tabla se define con el esquema adecuado para que las consultas SQL puedan acceder a la información integrada.

6. **Ejecución de Consultas en Athena**:  
    Se implementaron funciones que permiten ejecutar consultas SQL en Athena directamente desde el notebook. Las funciones están diseñadas para aceptar cualquier consulta, verificar el estado de la consulta y devolver los resultados en un DataFrame de `pandas`.

7. **Consultas de Ejemplo**:  
    El proyecto incluye varias consultas de ejemplo que pueden ser ejecutadas para analizar los datos, como:
    - Obtener las primeras 10 filas de la tabla.
    - Calcular el total de ventas por país.
    - Obtener la cantidad de productos vendidos por categoría.
    - Calcular el descuento promedio aplicado por empleado.

## Requisitos

Antes de ejecutar el notebook, asegúrate de tener instaladas las siguientes dependencias:

- `pandas`
- `boto3`
- `sqlalchemy`
- `dotenv`

Puedes instalar estas dependencias utilizando `pip`:

```sh
pip install pandas boto3 sqlalchemy python-dotenv psycopg2
```

Además, deberás configurar un archivo `.env` con las credenciales necesarias para conectar a PostgreSQL y AWS. El archivo `.env` debe contener las siguientes variables:

```env
POSTGRES_USER=your_postgres_user
POSTGRES_PASSWORD=your_postgres_password
POSTGRES_HOST=your_postgres_host
POSTGRES_PORT=your_postgres_port
POSTGRES_DB=your_postgres_db

AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
S3_BUCKET_NAME=your_s3_bucket_name
ATHENA_RESULT_BUCKET=s3://your-athena-result-bucket
```

## Ejecución del Proyecto

1. **Paso 1: Configuración del Entorno**  
   Asegúrate de tener configurado tu archivo `.env` con las credenciales correctas para PostgreSQL y AWS.

2. **Paso 2: Conectar y Procesar los Datos**  
   Ejecuta las celdas del notebook para conectar a la base de datos, cargar los datos y unificarlos.

3. **Paso 3: Subida a S3 y Configuración de Athena**  
   Una vez que los datos estén unificados, se suben a S3 y se configura Athena para que pueda consultar la información.

4. **Paso 4: Realizar Consultas SQL**  
   Utiliza las funciones provistas en el notebook para ejecutar consultas SQL en Athena y analizar los datos según sea necesario.

## Conclusión

Este proyecto demuestra cómo un **Data Lake** en AWS, utilizando **Amazon S3** para el almacenamiento y **Amazon Athena** para las consultas, puede integrarse fácilmente con datos de diversas fuentes para generar análisis escalables y eficientes. La arquitectura implementada permite consultas ad-hoc sin necesidad de mover grandes volúmenes de datos, lo que ofrece una solución flexible y de bajo costo para proyectos de análisis de datos.

Para más detalles y ejecución de código, consulta el **notebook** del proyecto.

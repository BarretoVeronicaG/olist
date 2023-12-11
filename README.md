![g3](https://github.com/BarretoVeronicaG/olist/assets/138631372/47fa3155-955c-4f70-8c56-1bad49e7ed9d)
# Olist Dataset                            

## **INTRODUCCIÓN**
Nuestro cliente es una empresa de E-Commerce de Argentina, que nos contrató para que realicemos un análisis del mercado Brasilero, utilizando la información provista de la empresa OLIST
Buscamos elaborar un tablero que permita describir el conjunto de datos entregados explorando el mercado brasileño entre los años 2016 y 2018

[**BASE DE DATOS_1**](https://drive.google.com/drive/folders/1ZGym_RAYdFoqzB9NGG_axmpXlc31fQ2e?usp=drive_link)
[**BASE DE DATOS_2**](https://drive.google.com/drive/folders/1mU_Pdqzqkp5MSDL2OjQBuMtwgHS-r-hj?usp=drive_link)

## **OBJETIVOS Y ALCANCES**
Nuestro alcance está orientado a Logística, tiempos de entrega, Productos y ventas y buscamos:

- Encontrar los productos más vendidos, los mejor calificados, así como medir sus ventas en periodos de tiempo 
- Explorar tiempos de entrega
- Analizar la relación de los tiempos de entrega con la satisfacción del cliente
- Verificar relación entre tiempo de entrega, producto y ubicación del cliente

## **DESCRIPCIÓN Y CONTENIDO DEL DATASET**
Base de datos provista por OLIST, que conecta pequeños negocios de todo Brasil, y se envian los productos desde centros OLIST a los clientes directos.
Los datos incluyen cosas como el estado del pedido, el precio, el pago, el envío, los productos y las reseñas. Los datos de geolocalización están asociados a códigos postales con coordenadas. 
Estos estan distribuidos en  11 tablas, incluyendo las siguientes elementos:


- Customers
- Sellers
- Products
- Product Category
- Orders
- Order Reviews
- Order Payments
- Order Items
- Geolocation
- Marketing


## **[ANÁLISIS EXPLOTARIO DE DATOS (EDA)](https://colab.research.google.com/drive/1bshbGjL9_eAs9u156hEGosSPF-lm0r7b#scrollTo=UAu9JfMHok-_)**   
Evaluamos, en primer lugar de forma general las Tablas, e identificamos que se cuenta con los datos de 100.000 pedidos de Brasil entre 2016 y 2018. 
Decidimos efectuar una lista de la información que necesitamos saber a priori:

-Nombre y número de de columnas, y número de filas
-Vista previa de las tablas, y de sus primeras 5 filas
-Identificación de los tipos de cada columnas
-Presencia de valores nulos
-Identificación de datos duplicados
-Exploración de la estadística general de los datos
-Elaboración de gráficos de barras e histogramas para evaluar la información 

En primer utilizamos la herramienta de Google, COLAB y por medio del lenguaje Python.
Luego se procedieron a efectuar los siguientes pasos: 

1)  Primero que se precisa efectuar es la importación de las librerias de Python

            ```
            import numpy as np
            import pandas as pd
            import matplotlib.pyplot as plt
            from matplotlib import rcParams
            import seaborn as sns
            ```

2) Importamos los CSV con los datasets, que previamente habiamos decidido guardar en el Drive de Google
   
            ```
            from google.colab import drive
            drive.mount('/content/drive')
            
            customers = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_customers_dataset.csv')
            geolocation = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_geolocation_dataset.csv')
            sellers = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_sellers_dataset.csv')
            order_items = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_order_items_dataset.csv')
            payments = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_order_payments_dataset.csv')
            reviews = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_order_reviews_dataset.csv')
            orders = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_orders_dataset.csv')
            products = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_products_dataset.csv')
            deals = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_closed_deals_dataset.csv')
            product_category = pd.read_csv('/content/drive/MyDrive/Olist Dataset/product_category_name_translation.csv')
            mkt = pd.read_csv('/content/drive/MyDrive/Olist Dataset/olist_marketing_qualified_leads_dataset.csv')
            ```

3) Proceder con el  Análisis Exploratorio de Datos

      - En primer lugar hicimos una identificación de las columnas y las filas
           ```
           datasets = [customers, geolocation, sellers, order_items, payments, reviews, orders, products, deals,
           product_category, mkt]
           titles = ["customers","geolocations","items", "payments", "orders", "products","reviews","sellers","category_translation", "lead_type", "origin" ]
           
           info_df = pd.DataFrame({},)
           info_df['dataset']= titles
           
           info_df['no_of_columns']= [len(df.columns) for df in datasets ]
           info_df['columns_name']= [', '.join(list(df.columns)) for df in datasets]
           info_df['no_of_rows'] = [len(df) for df in datasets]
           
           info_df.style.background_gradient(cmap='Greys')
         
           ```
         ![1 ncolumnas](https://github.com/BarretoVeronicaG/olist/assets/138631372/d8711367-c31f-4796-809d-45080b7e30a6)

      - Luego hicimos una visualización de las 5 primeras filas de cada una de las tablas, mediante el código:

                 ```
                 sellers.head()
                 customers.head()
                 products.head()
                 product_category.head()
                 geolocation.head()
                 orders.head()
                 order_items.head()
                 deals.head()
                 payments.head()
                 mkt.head()
                 reviews.head()
                 ```
               
                 Un ejemplo:
                 
                 ![2 vistapreviatabla](https://github.com/BarretoVeronicaG/olist/assets/138631372/c13acb8d-895d-46af-b19a-43eac5fad494)

      - Se procedió a efecutar una identificación de los tipos de datos de cada una de las tablas:
    
               ```
                sellers.dtypes
                customers.dtypes
                products.dtypes
                product_category.dtypes
                geolocation.dtypes
                deals.dtypes
                orders.dtypes
                order_items.dtypes
                payments.dtypes
                mkt.dtypes
                reviews.dtypes
               ```
            
           Los resultados se resumen en la siguiente Tabla:
          
        
           | TABLAS                                   | DATOS-STRING        | DATOS-NUMERO ENTERO (int) | DATOS-NUMERO DECIMALES (float) |
           |    :---:                                 |     :---:           |           :---:           |                :---:           | 
           | olist_customers_dataset                  | X                   |                           |                   X            | 
           | olist_geolocation_dataset                |                     | X                         |                                | 
           | olist_sellers_dataset                    | X                   | X                         |                                | 
           | olist_order_items_dataset                | X                   | X                         |                  X             | 
           | olist_order_payments_dataset             | X                   | X                         |                  X             | 
           | olist_order_reviews_dataset              | X                   | X                         |                                | 
           | olist_orders_dataset                     | X                   |                           |                                | 
           | olist_products_dataset                   | X                   |                           |         X                      | 
           | olist_closed_deals_dataset               | X                   |                           |             X                   | 
           | product_category_name_translation        | X                   |                           |                                | 
           | olist_marketing_qualified_leads_dataset  | X                   |                           |                                | 
             
      - El próximo paso fue la búsqueda de nulos:
      
                ```
                sellers.isnull().sum()
                customers.isnull().sum()
                products.isnull().sum()
                product_category.isnull().sum()
                geolocation.isnull().sum()
                deals.isnull().sum()
                orders.isnull().sum()
                order_items.isnull().sum()
                payments.isnull().sum()
                mkt.isnull().sum()
                reviews.isnull().sum() 
                 ```
        Los resultados se resumen en la siguiente Tabla:
 
        | TABLAS                            | COLUMNA                         | N° DE VALORES|
        |    :---:                          |     :---:                       |         :---:|  
        |olist_products_datase              |  product_category_name          |    610       |
        |                                   | product_name_lenght             |       610    |
        |                                   |  product_description_lenght     |     610      |
        |                                   | product_photos_qty              |        610   |
        |                                   | product_weight_g                |          2   |
        |                                   | product_length_cm               |           2  |
        |                                   | product_height_cm               |            2 |
        |                                   | product_width_cm                |             2|
        | olist_sellers_dataset             |   business_segment              | 1            |
        |                                   |   lead_type                     | 6            |
        |                                   |   lead_behaviour_profile        | 177          |
        |                                   |   has_company                   | 779          |
        |                                   |   has_gtin                      | 778          |
        |                                   |   average_stock                 | 776          |
        |                                   |   business_type                 | 10           |
        |                                   | declared_product_catalog_size   |   773        |
        |olist_orders_dataset               | order_approved_at               |     160      |       
        |                                   |order_delivered_carrier_date     |   1783       |
        |                                   |   order_delivered_customer_dat  |   2965       |
        |marketing_qualified_leads_dataset  | origin                          |60            |
        | olist_order_reviews_dataset       | review_comment_title            |   87656      | 
        |                                   | review_comment_message          |    58247     |

      - A continuación se revisó la presencia de duplicados en las tablas:
       
                 ```
                  sellers.duplicated().sum()
                  customers.duplicated().sum()
                  products.duplicated().sum()
                  product_category.duplicated().sum()
                  geolocation.duplicated().sum()
                  deals.duplicated().sum()
                  orders.duplicated().sum()
                  order_items.duplicated().sum()
                  payments.duplicated().sum()
                  mkt.duplicated().sum()
                  reviews.duplicated().sum()
                 ```
    
        *Olist_geolocation_dataset*, tiene 261831 valores duplicados. 
        Esto se debe a que se identifican varios códigos postales diferentes, asociados a la misma ciudad y geolo

      -  Luego se realizó la búsqueda de la información estadística de cada dataset:
          
                 ```
                  sellers.describe()
                  customers.describe()
                  products.describe()
                  geolocation.describe()
                  deals.describe()
                  orders.describe()
                  payments.describe()
                  order_items.describe()
                  mkt.describe()
                  reviews.describe()
                    
                 ```
     - Finalmente graficamos algunaos de los resultados, para poder comprender con que tipo de información contamos:
         
        **GEOLOCALIZACIÓN: olist_geolocation_dataset.**
       
         Se observa en un histograma la distribución de los datos de ubicación, tomando como como independiente (eje x), el dato de código postal, y como variable           dependiente (eje y), la frecuencia de cada codigo postal-
         
         ![4](https://github.com/BarretoVeronicaG/olist/assets/138631372/e0ef444c-0cfd-415f-a632-06a7ce7be0fd)
  
        **COMPRAS EFECTUADAS: olist_closed_deals_dataset.**
       
         Utilizamos una grafico de barras para graficar, las distintas estrategias de marketing usadas para la ventta como eje independiente (eje x) y la 
        frecuencia de uso de cada una en el eje y como variable dependiente. Online medium, es la más predominante.
         
                  
         ![5](https://github.com/BarretoVeronicaG/olist/assets/138631372/9d81f034-8478-4390-856e-fa9a4f1106d4)
         
       **COMPRAS EFECTUADAS: olist_closed_deals_dataset.**
       
       Observamos nuevamente, por medio de un gráfico de barras, los tipos de negocios por los que se efectuan ls ventas, en el eje x, con respecto a la 
       frecuencia de cada una en el eje y. La más recurrente es la reventa.
       
         ![6](https://github.com/BarretoVeronicaG/olist/assets/138631372/ca29a01d-723c-455b-b3b3-5e9fd215df8e)
         
       **ORDENES:olist_orders_dataset.**
       
       Por medio de un gráfico de barras, incidamos los estatus de las órdenes (eje x) con respecto al recuento, cantidad de órdenes (eje Y). Se concluyo que la 
       mayor cantidad de órdenes fueron entregadas.
       
         ![7](https://github.com/BarretoVeronicaG/olist/assets/138631372/1a339ccb-9dd9-46e7-ad8c-2168a7deed37)
         
       **PAGOS:olist_order_payments_dataset.**
       
       En este gráfico podemos observar en el eje independiente (eje x), los tipos de pagos efectuados en las compras, con respecto a la cantidad de compras 
       efectuadas con cada tipo de pago. La mayor cantidad de compras fueron efectuadas con tarjeta de crédito.
       
         ![8](https://github.com/BarretoVeronicaG/olist/assets/138631372/08f5de76-1426-400f-aa11-8901889f91fc)
         
       **PAGOS:olist_order_payments_dataset.**
       
       Observamos en este gráfico de tipo boxplot, que muestra a simple vista la mediana y los cuartiles de los datos, ​ y también pueden representarse sus valores 
        atípicos, los valores detro de los tipos de pago. Se identifican algunos valores atípicos alredor de los 14000 reales.
       
         ![9](https://github.com/BarretoVeronicaG/olist/assets/138631372/59ee77d4-94d5-497f-ac2e-eb1dbdb53e17)
         
       **MARKETING: olist_marketing_qualified_leads_dataset**
       
       Por medio de un diagrama de barras, se grafica en el eje X, los origines de las estrategias de marketing utilizadas para la venta, con la cantidad 
       efectuada de cada una. Se observa que la estrategia más utilizada es la búsqueda orgánica.
       
         ![10](https://github.com/BarretoVeronicaG/olist/assets/138631372/1fa05d45-0070-4aa7-9dc8-f5e876729cc5)
         
       **REVIEWS:olist_order_reviews_dataset.**
       
       Efectuamos por medio de un gráfico de torta, una análisis de la cantidad de reviews posititvas, con un rating de más de 4, en comparación con las peores           reviews con rating de menos de 3. Se puede observar una mayor cantidad de reviews positivas, con un 77% frente a un 22% de reviews negativas.
       
         ![11](https://github.com/BarretoVeronicaG/olist/assets/138631372/30839993-4b45-4c6a-b28a-e16296b0b281)

5) Conclusión de la exploración de los datos
   
   Con esta información finalmente decimos con cuales tablas ibamos a continuar para el proceso de ETL y posterior procesamiento para la visualización, las mismas 
   corresponden a:

   **olist_closed_deals_dataset** y **olist_marketing_qualified_leads**, ya que al enfocarse en el área de marketing y no se ajusta a los KPI's en los que 
   elegimos enfocarnos
   De la misma forma, elegimos no utilizar la información de la tabla olist_sellers_dataset, ya que nos interesa la información de los clientes y específicamente 
   los datos específicos de los vendedores.

## **INDICADORES (KPI's)**

Los indicadores finales sobre los que decimos trabajar son:

- Total Ventas/Categoria - TOP 10
- Número de productos vendidos por mes y año
- Proceso de entrega de las órdenes
- Promedio Dias De Entrega
- Mejores/Peores  Categorías Según Los Consumidores”

## **[LIMPIEZA DE DATOS (ETL)](https://console.cloud.google.com/bigquery?ws=!1m5!1m4!4m3!1sethereal-brace-360713!2sDATASET!3sFINAL3&project=dolar-mep)**
Decidimos continuar trabajando dentro del entorno de google, por lo que elegimos conectar con GCP (GOOGLE CLOUD PLATFORM) par el resto del proceso de almacenamiento de datos y la gestión de la visualización de los mismos




https://github.com/BarretoVeronicaG/olist/assets/138631372/50701b2a-1630-42ef-91f4-b36490b9bf30




## **[DASHBOARD](https://lookerstudio.google.com/s/uEhB_SuI3pk)**
Finalmente con con el analisis previo efectuado, realizamos una visualización de datos utilizando la herramienta *Looker Studio*, ya que pertenece al entorno donde estamos desarrollando nuestro Proyecto, facilitando la conexión, y además tiene una interfaz intuitiva con un buen diseño
La misma se efectuó por medio de Big Query.


![Análisis_Olist_E-Commerce-001](https://github.com/BarretoVeronicaG/olist/assets/138631372/fbb5ea74-ea52-4900-8eda-297c2b105856)

![Análisis_Olist_E-Commerce-002](https://github.com/BarretoVeronicaG/olist/assets/138631372/122cda41-7cce-4328-b616-98bc2b8a3caf)

![Análisis_Olist_E-Commerce-003](https://github.com/BarretoVeronicaG/olist/assets/138631372/f709261a-85a0-4f35-89f3-532dbebc2ece)

## **CONCLUSIONES**

Según los datos, Olist E-commerce tiene alrededor de 99.441 pedidos durante 2016-2018.
 
La empresa tiene una tasa de éxito del 82.4%. 

Su valoración media de los productos es de 4,02 estrellas, con categorías de productos que van tan alto como 4,64 estrellas (de un máximo de 5) y tan bajo como 2,5 estrellas. Las opiniones desfavorables probablemente indican que podría haber problemas con la calidad de los productos en algunas categorías de productos. 

El rendimiento de la entrega también podría influir en las puntuaciones de las reseñas y, sin duda, el porcentaje de éxito podría mejorarse.

Con la supervisión y análisis periódico de las opiniones de los clientes, se podrá obtener constantemente, nueva información sobre la calidad de los productos e identificar áreas de mejora. 

Los retrasos en las entregas (17,6% demoradas), pueden deberse a determinados retos demográficos, accesibilidad y posible optimización de rutas.


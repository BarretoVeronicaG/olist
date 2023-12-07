# Olist Dataset                            

![g3](https://drive.google.com/file/d/12wAeTE_uU_piC0USo3gPDpONuWHh1NcL/view?usp=drive_link)

## **INTRODUCCIÓN**
Nuestro cliente es una empresa de E-Commerce de Argentina, que nos contrató para que realicemos un análisis del mercado Brasilero, utilizando la información provista de la empresa OLIST
Buscamos elaborar un tablero que permita describir el conjunto de datos entregados explorando el mercado brasileño entre los años 2016 y 2018

##**OBJETIVOS Y ALCANCES**
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


##**[ANÁLISIS EXPLOTARIO DE DATOS (EDA)](https://colab.research.google.com/drive/1bshbGjL9_eAs9u156hEGosSPF-lm0r7b#scrollTo=UAu9JfMHok-_)**   
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

En primer lugar hicimos una identificación de las columnas y las filas
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
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://drive.google.com/file/d/1dEkPlFDnd3F9_6AKRjy5EtfFWf7W7e3C/view?usp=sharing">
  <source media="(prefers-color-scheme: light)" srcset="https://drive.google.com/file/d/1dEkPlFDnd3F9_6AKRjy5EtfFWf7W7e3C/view?usp=sharing">
  <img alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://drive.google.com/file/d/1dEkPlFDnd3F9_6AKRjy5EtfFWf7W7e3C/view?usp=sharing">
</picture>

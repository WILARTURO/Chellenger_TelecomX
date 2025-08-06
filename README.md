# Análisis de Evasión de Clientes (Churn) - Telecom X

## Descripción del Proyecto

Este proyecto de análisis de datos investiga los factores que contribuyen a la evasión de clientes (`Churn`) en la empresa Telecom X. A través de la preparación de datos (ETL) y el análisis exploratorio (EDA), se identifican patrones clave que influyen en la decisión de los clientes de cancelar sus servicios. El objetivo es proporcionar insights que sirvan como base para estrategias de retención más efectivas.

## Conjunto de Datos

El análisis se basa en el archivo `Datos_TelecomX.csv`, que contiene información detallada sobre los clientes de Telecom X. Las variables clave exploradas incluyen: `Churn` (la variable objetivo), `customer.tenure`, `account.Contract`, `internet.InternetService`, `account.Charges.Monthly` y `account.Charges.Total`.

---

## 1. Configuración y Carga Inicial de Datos

Este bloque de código configura el entorno de trabajo, carga el archivo CSV y muestra una visión general de los datos antes de la limpieza.

```python
# Importar las librerías necesarias
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Configuración para un mejor estilo visual de los gráficos
sns.set(style="whitegrid")

# Cargar el archivo CSV
# Asegúrate de que el archivo 'Datos_TelecomX.csv' esté en la misma carpeta o sube
# el archivo a tu sesión de Google Colab.
df = pd.read_csv('Datos_TelecomX.csv')

# Mostrar las primeras filas del DataFrame
print("Primeras 5 filas del dataset:")
print(df.head())

# Mostrar información del DataFrame para verificar tipos de datos
print("\nInformación del DataFrame antes de la limpieza:")
print(df.info())

# Identificar y manejar valores faltantes en 'account.Charges.Total'
# Los valores en blanco se reemplazan por NaN para poder tratarlos.
df['account.Charges.Total'] = df['account.Charges.Total'].replace(' ', np.nan)

# Convertir la columna a tipo numérico. 'errors=coerce' convierte
# los valores no numéricos a NaN.
df['account.Charges.Total'] = pd.to_numeric(df['account.Charges.Total'], errors='coerce')

# Rellenar los valores nulos (NaN) resultantes con 0, asumiendo
# que son clientes nuevos sin cargos aún.
df['account.Charges.Total'].fillna(0, inplace=True)

# Verificar que la columna ha sido convertida y no tiene nulos
print("\nInformación del DataFrame después de la limpieza:")
print(df.info())

# Convertir la variable objetivo 'Churn' a formato numérico (0 y 1) para el análisis
df['Churn_num'] = df['Churn'].apply(lambda x: 1 if x == 'Yes' else 0)

print("\nLa columna 'Churn' ha sido convertida a 'Churn_num' (1 = Yes, 0 = No).")

# Calcular el porcentaje de evasión
total_clientes = len(df)
clientes_evadidos = df[df['Churn'] == 'Yes'].shape[0]
porcentaje_evasion = (clientes_evadidos / total_clientes) * 100

print(f"\nTotal de clientes: {total_clientes}")
print(f"Clientes que se evadieron: {clientes_evadidos}")
print(f"Porcentaje de evasión (Churn Rate): {porcentaje_evasion:.2f}%")

# Visualización de la distribución de Churn
plt.figure(figsize=(6, 5))
sns.countplot(x='Churn', data=df, palette='pastel')
plt.title('Distribución de Clientes por Evasión (Churn)', fontsize=16)
plt.xlabel('Evasión (Churn)')
plt.ylabel('Número de Clientes')
plt.show()

# Definir las variables categóricas de interés
categorical_vars = [
    'customer.gender', 'customer.SeniorCitizen', 'customer.Partner',
    'customer.Dependents', 'phone.PhoneService', 'internet.InternetService',
    'account.Contract', 'account.PaymentMethod'
]

# Crear subplots para visualizar la evasión por cada variable categórica
fig, axes = plt.subplots(nrows=4, ncols=2, figsize=(18, 20))
fig.suptitle('Distribución de Evasión (Churn) por Variables Categóricas', fontsize=20, y=1.02)

for i, var in enumerate(categorical_vars):
    row = i // 2
    col = i % 2
    sns.countplot(
        data=df,
        x=var,
        hue='Churn',
        ax=axes[row, col],
        palette='viridis'
    )
    axes[row, col].set_title(f'Evasión por {var}', fontsize=14)
    axes[row, col].set_xlabel('')
    axes[row, col].set_ylabel('Número de Clientes')
    axes[row, col].tick_params(axis='x', rotation=45)

plt.tight_layout()
plt.show()

# Para un análisis más detallado, se imprimen las proporciones
for var in categorical_vars:
    print(f"\nDistribución de Churn por {var}:")
    churn_rate = df.groupby(var)['Churn'].value_counts(normalize=True).unstack().mul(100).round(2)
    print(churn_rate)
    print("-" * 50)

# Definir las variables numéricas de interés
numerical_vars = ['customer.tenure', 'account.Charges.Monthly', 'account.Charges.Total']

# Crear subplots para visualizar la evasión por cada variable numérica
fig, axes = plt.subplots(nrows=len(numerical_vars), ncols=2, figsize=(18, 15))
fig.suptitle('Distribución de Evasión (Churn) por Variables Numéricas', fontsize=20, y=1.02)

for i, var in enumerate(numerical_vars):
    # Boxplot para ver la mediana y la dispersión
    sns.boxplot(
        data=df,
        x='Churn',
        y=var,
        ax=axes[i, 0],
        palette='magma'
    )
    axes[i, 0].set_title(f'Boxplot de {var} por Churn', fontsize=14)
    axes[i, 0].set_xlabel('Evasión (Churn)')
    axes[i, 0].set_ylabel(var)

    # Histograma para ver la distribución de frecuencias
    sns.histplot(
        data=df,
        x=var,
        hue='Churn',
        ax=axes[i, 1],
        kde=True,
        palette='magma'
    )
    axes[i, 1].set_title(f'Histograma de {var} por Churn', fontsize=14)
    axes[i, 1].set_xlabel(var)
    axes[i, 1].set_ylabel('Frecuencia')

plt.tight_layout()
plt.show()

# Definir las variables numéricas de interés
numerical_vars = ['customer.tenure', 'account.Charges.Monthly', 'account.Charges.Total']

# Crear subplots para visualizar la evasión por cada variable numérica
fig, axes = plt.subplots(nrows=len(numerical_vars), ncols=2, figsize=(18, 15))
fig.suptitle('Distribución de Evasión (Churn) por Variables Numéricas', fontsize=20, y=1.02)

for i, var in enumerate(numerical_vars):
    # Boxplot para ver la mediana y la dispersión
    sns.boxplot(
        data=df,
        x='Churn',
        y=var,
        ax=axes[i, 0],
        palette='magma'
    )
    axes[i, 0].set_title(f'Boxplot de {var} por Churn', fontsize=14)
    axes[i, 0].set_xlabel('Evasión (Churn)')
    axes[i, 0].set_ylabel(var)

    # Histograma para ver la distribución de frecuencias
    sns.histplot(
        data=df,
        x=var,
        hue='Churn',
        ax=axes[i, 1],
        kde=True,
        palette='magma'
    )
    axes[i, 1].set_title(f'Histograma de {var} por Churn', fontsize=14)
    axes[i, 1].set_xlabel(var)
    axes[i, 1].set_ylabel('Frecuencia')

plt.tight_layout()
plt.show()

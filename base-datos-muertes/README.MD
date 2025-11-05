# 💀 Muertes Accidentales - Base de Datos

## 📋 Descripción

Sistema de base de datos para el **registro y seguimiento de hechos relacionados con personas**, diseñado bajo el **modelo relacional** y normalizado hasta la **Tercera Forma Normal (3FN)**.

---

## 🗂️ Estructura del Proyecto

proyecto/
├── README.md
├── diagrams/
│ ├── modelo-conceptual.png
│ ├── modelo-logico-1FN.mmd
│ ├── modelo-logico-2FN.mmd
│ └── modelo-logico-3FN.mmd
└── database/
└── muertes-database.sql


---

## 🎯 Características

- ✅ **Normalización completa hasta 3FN**  
- ✅ **Integridad referencial** mediante claves foráneas  
- ✅ **Compatibilidad UTF-8** (soporte para tildes, ñ y emojis)  

---

## 📊 Modelo de Datos

### 🔸 Entidades Principales

| Entidad | Descripción |
|----------|-------------|
| **PERSONA** | Información demográfica de individuos |
| **HECHO** | Registro de eventos asociados a personas |
| **FECHA** | Datos temporales del hecho |
| **UBICACION** | Información geográfica del hecho |

### 🔹 Tablas de Catálogo

| Catálogo | Descripción |
|-----------|--------------|
| **MAYOR_MENOR** | Clasificación por mayoría de edad |
| **GRUPO_EDAD_QUINQUENAL** | Rangos de edad (0–4, 5–9, etc.) |
| **DEPARTAMENTO** | Departamentos con código DANE |
| **MUNICIPIO** | Municipios con código DANE |

---

## 🔗 Relaciones Entre Tablas

PERSONA (1) ──▶ (N) HECHO
HECHO (1) ──▶ (1) FECHA
HECHO (1) ──▶ (1) UBICACION
MUNICIPIO (N) ──▶ (1) DEPARTAMENTO
PERSONA (N) ──▶ (1) MAYOR_MENOR
PERSONA (N) ──▶ (1) GRUPO_EDAD_QUINQUENAL
UBICACION (N) ──▶ (1) MUNICIPIO


---

## 📈 Formas Normales Aplicadas

### 🧩 Primera Forma Normal (1FN)
- ✅ Todos los atributos contienen **valores atómicos**  
- ✅ No hay **grupos repetitivos**  
- ✅ Cada tabla tiene **clave primaria definida**

---

### ⚙️ Segunda Forma Normal (2FN)
- ✅ Cumple con 1FN  
- ✅ No existen **dependencias parciales**  
- ✅ Todos los atributos no clave **dependen de la clave primaria completa**

---

### 🧠 Tercera Forma Normal (3FN)
- ✅ Cumple con 2FN  
- ✅ No hay **dependencias transitivas**  
- ✅ Separación lógica de catálogos (**MAYOR_MENOR**, **GRUPO_EDAD_QUINQUENAL**)  
- ✅ Normalización geográfica (**DEPARTAMENTO**, **MUNICIPIO**)

---

## 🧾 Autor
Juan Pablo Quijano

---
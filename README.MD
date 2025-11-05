Muertes-Accidentales - Base de Datos

📋 Descripción

Sistema de base de datos para el registro y seguimiento de hechos relacionados con personas, diseñado bajo el modelo relacional en Tercera Forma Normal (3FN).

🗂️ Estructura del Proyecto

proyecto/
│
├── README.md
├── diagrams/
│   ├── modelo-conceptual.png
│   ├── modelo-logico-1FN.mmd
│   ├── modelo-logico-2FN.mmd
│   └── modelo-logico-3FN.mmd
│
└── database/
    └── muertes-database.sql
🎯 Características

✅ Normalización hasta 3FN
✅ Integridad referencial con claves foráneas
✅ Soporte completo UTF-8 (tildes, ñ, emojis)

📊 Modelo de Datos
Entidades Principales

PERSONA: Información demográfica de individuos
HECHO: Registro de eventos asociados a personas
FECHA: Datos temporales del hecho
UBICACION: Información geográfica del hecho

Tablas de Catálogo

MAYOR_MENOR: Clasificación por mayoría de edad
GRUPO_EDAD_QUINQUENAL: Rangos de edad (0-4, 5-9, etc.)
DEPARTAMENTO: Departamentos con código DANE
MUNICIPIO: Municipios con código DANE

🔗 Relaciones
PERSONA (1) ──→ (N) HECHO
HECHO (1) ──→ (1) FECHA
HECHO (1) ──→ (1) UBICACION
MUNICIPIO (N) ──→ (1) DEPARTAMENTO
PERSONA (N) ──→ (1) MAYOR_MENOR
PERSONA (N) ──→ (1) GRUPO_EDAD_QUINQUENAL
UBICACION (N) ──→ (1) MUNICIPIO


📈 Formas Normales Aplicadas

Primera Forma Normal (1FN)

✅ Todos los atributos contienen valores atómicos
✅ No hay grupos repetitivos
✅ Cada tabla tiene clave primaria

Segunda Forma Normal (2FN)

✅ Cumple 1FN
✅ No hay dependencias parciales
✅ Todos los atributos no clave dependen de la clave primaria completa

Tercera Forma Normal (3FN)

✅ Cumple 2FN
✅ No hay dependencias transitivas
✅ Separación de catálogos (MAYOR_MENOR, GRUPO_EDAD_QUINQUENAL)
✅ Normalización geográfica (DEPARTAMENTO, MUNICIPIO)


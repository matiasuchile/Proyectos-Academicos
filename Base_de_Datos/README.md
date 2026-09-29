# README — Proyecto Paraderos Santiago (Hito 3)

**Curso:** CC-3201 Bases de Datos  
**Grupo 06:** Matias CColque, Benjamín Brito, Gabriel Conejeros, Patricio Rivera  
**Profesor:** Eduardo Godoy V.  
**Fecha:** 29 de septiembre de 2026 — Santiago de Chile

---

## Descripción

Análisis de patrones de movilidad en el transporte público de Santiago usando datos del **DTPM** (viajes, etapas, subidas por paradero) y el **Índice de Prioridad Social (IPS) 2024** del MDSF.

**Hipótesis:** Existe relación entre los patrones de desplazamiento y la calidad de vida (IPS) de las comunas; los sectores más vulnerables dependen más del transporte público.

---

## Datasets

| Fuente | Contenido |
|--------|-----------|
| DTPM — Tabla de Viajes | Registros individuales de viajes |
| DTPM — Tabla de Etapas | Detalle origen/destino por etapa |
| DTPM — Subidas por Paradero | Promedio cada 30 min |
| MDSF — IPS 2024 | Índice de prioridad social comunal |
| BCN — Reportes Comunales | Datos sociodemográficos |

**Limitaciones:** solo viajes pagados (excluye evasión), bajadas menos precisas, una sola semana de estudio.

---

## Entidades Principales

| Entidad | Llave Primaria |
|---------|----------------|
| Viaje | id_viaje |
| Pasajero | id_tarjeta |
| Paradero | SIMIT + dia + media_hora |
| Etapa | id_etapa + dia + hora_inicio |
| Comuna | nombre |

**Relaciones:** realiza (Pasajero→Viaje), contiene (Viaje→Etapa), tiene (Viaje↔Paradero), posee (Etapa↔Paradero), pertenece (Paradero→Comuna).

---

## Modelo Relacional

Esquema normalizado en **BCNF**. Tablas: `Comuna`, `Pasajero`, `Viaje`, `Etapa`, `Paradero`, `Tiene`, `Posee`.

---

## Implementación

- **Lenguaje:** Python (psycopg2, pandas)
- **BD:** PostgreSQL
- **Carga:** paraderos (.xlsb), viajes y etapas (CSV), comunas (manual)
- **Control:** se omite el día sin archivo de etapas para mantener integridad

---

##  Consultas Diseñadas

1. Top 5 paraderos con más subidas
2. Comunas vulnerables con mayor demanda
3. Promedio de etapas por comuna según IPS
4. Demanda por media hora por comuna
5. Dispersión del peak (veces que se supera la mitad del peak)
6. Distancia promedio por viaje en horario AM según comuna e IPS

---

## Optimizaciones

**Índices:** `paradero(nombre_comuna)`, `paradero(simit)`, `viaje(id_viaje, dia, hora_inicio)`, `tiene(id_viaje, dia)`, `tiene(simit)`.

**Vistas materializadas:**
- `demanda_paradero`: demanda agregada por comuna
- `viajes_y_comuna`: precalcula JOINs Viaje-Tiene-Paradero-Comuna

---

## Referencias

- DTPM — Matrices de Viaje: https://www.dtpm.cl
- MDSF — IPS 2024 y CASEN 2022
- BCN — Reportes Comunales (SIIT)

---

## Conclusión

Esquema relacional en BCNF con consultas e índices que permiten analizar la relación entre movilidad y vulnerabilidad social en Santiago, optimizando el rendimiento mediante vistas materializadas.

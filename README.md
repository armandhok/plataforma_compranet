# plataforma_compranet

***********************************************************

### Funcionalidad requerida API

*En este documento, se especifican las diferentes variables y agregados necesarios que el API debe exponer como puntos de acceso, así como los parámetros y criterios de búsqueda y filtrado de cada uno, para el desarrollo de la plataforma de contrataciones abiertas.*

* **Estadísticos generales:**
    * Parámetros de búsqueda/filtrado
      * Nivel de gobierno (federal, estatal, municipal)
    * Agregados
      * Número de dependencias
      * Número de procedimientos de contratación
      * Montos totales
    * Ejemplo Respuesta:

```json 
{"nivel_gob": "federal",  "num_dep": 176,  "num_proc": 5460000, "monto": 500000000 }
```

* **Resumen de montos (Diagrama de dona):**
    * Parámetros de búsqueda/filtrado
      * Nivel de gobierno (federal, estatal, municipal)
      * Tipo de procedimiento (licitación pública, adjudicación directa, convenio de colaboración, invitación a tres, otros)
      * Materia de contratación (obra pública, bienes y servicios)
      * Año (fecha de firma)
    * Agregados
      * Número de procedimientos
      * Porcentaje que representa dicho número de procedimientos
      * Montos totales
    * Ejemplo Respuesta:

```json 
{"anio": 2017, "objeto": "tipo_procedimiento", "resultados": [{"tipo": "licitación pública", "num_proc": 39000, "monto": 195000000}, {"tipo": "adjudicación directa", "num_proc": 517000, "monto": 1454999000},"..."{"tipo": "invitación a tres", "num_proc": 45600, "monto": 243423243}]}
{"anio": 2017, "objeto": "materia_de_contratación", "resultados": [{"tipo": "obra pública", "num_proc": 43200, "monto": 16000000}, {"tipo": "bienes", "num_proc": 532000, "monto": 146599000},"..." {"tipo": "servicios", "num_proc": 487600, "monto":987654}]}
```

* **Resumen de montos (Sunburst):**
    * Parámetros de búsqueda/filtrado
      * Nivel de gobierno (federal, estatal, municipal)
      * Institución (dependencia/secretaría,  entidades, municipios)
      * Materia de contratación (obra pública, bienes y servicios)
      * Tipo de procedimiento  (licitación pública, adjudicación directa, convenio de colaboración, invitación a tres, otros)
      * Monto (cuartiles de la distribución general de montos)
    * Agregados
      * Número de contrataciones
      * Monto total
    * Ejemplo respuesta:

```json 
{"nivel_gobierno": "federal", "monto": 6435323, "num_contratos": 43233, "instituciones": [{"institucion": "sep", "monto": 7644, "num_contratos": 764, "materias": [{"materia": "servicios", "monto": 234, "num_contratos": 34, "tipos": [{"tipo": "licitación pública", "monto": 131, "num_contratos": 32, "montos": [{"quartil": 1, "monto": 32, "num_contratos": 17}"..."]}"..."]}"..."]}"..."]}
```

* **Contrataciones en el tiempo:**
    * Parámetros de búsqueda/filtrado
      * Nivel de gobierno
      * Año, mes (fecha de firma)
      * Paginación
    * Parámetros de ordenamiento
      * Monto
      * Fecha
    * Agregados
      * Institución
      * Monto de contratación
      * Vigencia en días naturales
      * Fecha de firma
      * Tipo de procedimiento (licitación pública, adjudicación directa, convenio de colaboración, invitación a tres, otros)
      * Titulo de procedimiento
    * Ejemplo respuesta:

```json 
[{"nombre_proc": "proc_1", "institucion": "imss", "anio": 2017, "mes": "enero", "fecha_firma": "2017-01-12 T 18:00:00", "vigencia_dias": 1345, "tipo": "liciatación pública", "monto": 84882142332’}"...".]
```


* **Procedimientos de contratación:**
    * Parámetros de búsqueda/filtrado
      * Nivel de gobierno
      * Año, mes (fecha de firma)
      * Paginación
    * Parámetros de ordenamiento
      * Monto
      * Fecha
      * Institución
      * Etapa (planeación, licitación, adjudicación, contratación, implementación)
    * Agregados
      * Institución
      * Monto de contratación
      * Vigencia en días naturales
      * Fecha de firma
      * Tipo de procedimiento (licitación pública, adjudicación directa, convenio de colaboración, invitación a tres, otros)
      * Titulo de procedimiento
    * Ejemplo respuesta:

```json 
[{"nombre_proc": "proc_1", "anio": 2017, "mes": "enero", "fecha_firma": "2017-01-12 T 18:00:00", "etapa": "Contratación", "tipo": "liciatación pública", "monto": 84882142332, "institucion": "SCT", "nivel_gob": "Federal"}"...".]
```

* *Nota: Comprendemos que algunos de los criterios de búsqueda y filtros son redundantes, no obstante desglosamos la funcionalidad por sección para mayor comprensión del desarrollador. El que éste tome la decisión de integrar diversos puntos de acceso en uno mismo es una decisión de diseño.*

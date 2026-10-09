# Formulación del problema

## Título

**Diseño e implementación de una base de datos relacional normalizada para la gestión de historias clínicas de pacientes del área de oftalmología y glaucoma.**

## Problema

El área de oftalmología y glaucoma maneja información clínica que posee múltiples relaciones y una alta dependencia del histórico del paciente. Un diseño de datos inadecuado puede generar redundancia, inconsistencias, pérdida de trazabilidad y dificultades para consultar la evolución clínica.

Por esta razón, se requiere construir una base de datos relacional en MySQL que permita organizar correctamente pacientes, historias clínicas, consultas, diagnósticos, antecedentes, exámenes oftalmológicos, tratamientos y controles de glaucoma.

El diseño deberá aplicar técnicas de modelado conceptual, lógico y físico, así como un proceso de normalización hasta la Cuarta Forma Normal. Posteriormente se deberán implementar mecanismos de consulta y procesamiento mediante SQL, incluyendo consultas básicas, intermedias y avanzadas, subconsultas, funciones agregadas, vistas, procedimientos almacenados, funciones, triggers y eventos.

El resultado deberá ser una base de datos íntegra, consistente, escalable y capaz de responder consultas relacionadas con el seguimiento histórico y clínico de los pacientes.

Cada paciente puede asistir a múltiples consultas a lo largo del tiempo y, durante cada atención, pueden generarse diferentes tipos de datos clínicos.

Por ejemplo:

```
Paciente
   |
   +-- Datos personales
   |
   +-- Historia clínica
   |
   +-- Antecedentes
   |
   +-- Consultas
   |      |
   |      +-- Diagnósticos
   |      +-- Examen oftalmológico
   |      +-- Presión intraocular
   |      +-- Tratamientos
   |
   +-- Estudios especializados
          |
          +-- OCT
          +-- Campo visual
          +-- Paquimetría
          +-- Gonioscopía
```

En pacientes con glaucoma, la necesidad de conservar información histórica es aún mayor, debido a que variables como la presión intraocular, el estado del nervio óptico, la paquimetría, los resultados de OCT y los campos visuales deben compararse entre diferentes controles.

Si esta información se almacena de manera desestructurada, pueden aparecer problemas como:

- duplicidad de datos;
- inconsistencias entre registros;
- redundancia;
- dificultad para establecer relaciones entre consultas y resultados;
- pérdida de trazabilidad;
- dificultad para consultar la evolución histórica;
- dificultad para obtener indicadores;
- problemas para generar reportes;
- almacenamiento de información repetida;
- dependencia excesiva de campos de texto libre.

Por esta razón se requiere diseñar una base de datos relacional que permita representar correctamente la información clínica y mantener su integridad.

# 2. Situación problema

La información de una historia clínica oftalmológica está compuesta por múltiples entidades relacionadas entre sí.

Por ejemplo, un paciente puede presentar:

```
1 paciente
      |
      +-- 1 historia clínica
      |
      +-- N consultas
      |
      +-- N diagnósticos
      |
      +-- N tratamientos
      |
      +-- N mediciones de presión intraocular
      |
      +-- N estudios OCT
      |
      +-- N campos visuales
```

Además, muchas variables deben manejarse separadamente para:

```
OD = ojo derecho
OI = ojo izquierdo
```

Un diseño inadecuado podría conducir a estructuras como:

```
paciente
--------------------------------------------------
id
nombre
diagnostico1
diagnostico2
diagnostico3
medicamento1
medicamento2
presion_od_1
presion_oi_1
presion_od_2
presion_oi_2
oct1
oct2
campo_visual1
campo_visual2
```

Este diseño presenta importantes problemas de normalización.

Entre ellos:

- grupos repetitivos;
- múltiples valores dentro de una misma entidad;
- dificultad para agregar nuevos registros;
- redundancia;
- anomalías de inserción;
- anomalías de actualización;
- anomalías de eliminación.

Por esta razón será necesario aplicar un proceso formal de normalización.

# 3. Problema central

Se requiere diseñar una base de datos relacional en MySQL que permita gestionar de forma estructurada la información correspondiente a historias clínicas de pacientes atendidos en el área de oftalmología y glaucoma.

El diseño deberá permitir representar adecuadamente las relaciones existentes entre pacientes, historias clínicas, consultas, diagnósticos, antecedentes, medicamentos, tratamientos, estudios oftalmológicos y controles de glaucoma.

La estructura deberá minimizar redundancias y anomalías mediante un proceso de normalización hasta alcanzar la **Cuarta Forma Normal —4FN—**.

Además, la base de datos deberá permitir realizar operaciones de consulta y procesamiento de información utilizando SQL en diferentes niveles de complejidad.

# 4. Pregunta problema

**¿Cómo diseñar e implementar una base de datos relacional en MySQL, normalizada hasta la Cuarta Forma Normal, que permita almacenar, relacionar, consultar y procesar eficientemente la información de las historias clínicas de pacientes del área de oftalmología y glaucoma?**

# 5. Objetivo general

Diseñar e implementar una base de datos relacional en MySQL para la gestión de historias clínicas del área de oftalmología y glaucoma, aplicando técnicas de modelado de datos, normalización hasta 4FN, integridad referencial y consultas SQL de diferentes niveles de complejidad.

# 6. Objetivos específicos

1. Identificar las entidades, atributos y relaciones necesarias para representar la información clínica de pacientes de oftalmología y glaucoma.
2. Construir el modelo conceptual de la base de datos.
3. Diseñar el modelo lógico relacional.
4. Elaborar el Diagrama Entidad-Relación —DER—.
5. Aplicar el proceso de normalización hasta alcanzar la Cuarta Forma Normal.
6. Implementar el modelo físico utilizando MySQL.
7. Definir claves primarias y foráneas.
8. Implementar restricciones de integridad utilizando:

```
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
CHECK
DEFAULT
```

1. Insertar datos de prueba coherentes con el dominio del problema.
2. Construir consultas SQL básicas.
3. Construir consultas SQL de nivel intermedio.
4. Construir consultas SQL avanzadas.
5. Implementar subconsultas.
6. Aplicar funciones agregadas.
7. Utilizar agrupamientos con `GROUP BY` y filtros con `HAVING`.
8. Implementar vistas para facilitar consultas recurrentes.
9. Desarrollar procedimientos almacenados.
10. Implementar funciones almacenadas.
11. Crear disparadores —triggers— para automatizar operaciones y auditoría.
12. Utilizar eventos programados cuando el caso de estudio lo requiera.

# 7. Alcance del proyecto

El proyecto estará limitado al diseño, implementación y explotación de la base de datos.

No incluirá:

```
Frontend
Aplicación web
Aplicación móvil
API REST
Backend
Interfaces gráficas
```

El producto principal será una base de datos funcional en MySQL.

# 8. Alcance funcional de la base de datos

La base de datos deberá permitir gestionar información relacionada con:

```
Pacientes
Historias clínicas
Profesionales
Consultas
Antecedentes
Diagnósticos
Especialidades
Exámenes oftalmológicos
Presión intraocular
Paquimetrías
Gonioscopías
OCT
Campos visuales
Tratamientos
Medicamentos
Procedimientos
Controles de glaucoma
Archivos clínicos
Auditoría
```

# 9. Entidades preliminares

A partir del análisis inicial podrían identificarse entidades como:

```
patients
clinical_histories
medical_visits
healthcare_professionals
specialties
medical_histories
diagnoses
visit_diagnoses
ophthalmologic_exams
intraocular_pressures
pachymetry_exams
gonioscopy_exams
oct_exams
visual_field_exams
glaucoma_records
glaucoma_controls
medications
treatments
procedures
clinical_documents
audit_logs
```

Estas entidades deberán validarse y refinarse durante el modelado.

# 10. Modelo conceptual esperado

En el modelo conceptual deberán representarse las entidades principales sin depender todavía de detalles específicos del motor MySQL.

Una aproximación inicial podría ser:

```
PACIENTE
   |
   | 1
   |
   | 1
   v
HISTORIA_CLINICA
   |
   | 1
   |
   | N
   v
CONSULTA
   |
   +------------------+
   |                  |
   v                  v
DIAGNOSTICO       EXAMEN_OFTALMOLOGICO
                      |
        +-------------+-------------+
        |             |             |
        v             v             v
       PIO           OCT       CAMPO_VISUAL
```

Además:

```
PACIENTE
   |
   | 1
   |
   | N
   v
TRATAMIENTO
```

y:

```
PACIENTE
   |
   | 1
   |
   | N
   v
CONTROL_GLAUCOMA
```

[](https://i.ibb.co/m5gDRPbG/imagen-conceptual.png)

# 11. Modelo lógico esperado

El modelo lógico deberá transformar las entidades conceptuales en relaciones.

Ejemplo:

```
PATIENTS
-------
id PK
document_type_id FK
document_number
first_name
last_name
birth_date
sex

CLINICAL_HISTORIES
------------------
id PK
patient_id FK

MEDICAL_VISITS
--------------
id PK
clinical_history_id FK
professional_id FK
visit_date
reason
assessment
plan
```

El modelo completo deberá incluir todas las claves y cardinalidades.

​	[](https://i.ibb.co/SwKhKBMv/logico.png)

# 12. Diagrama Entidad-Relación

El DER deberá representar:

- entidades;
- atributos;
- claves primarias;
- claves foráneas;
- relaciones;
- cardinalidades;
- participación;
- entidades asociativas.

Por ejemplo:

```
PATIENT
1
|
|
1
CLINICAL_HISTORY

CLINICAL_HISTORY
1
|
|
N
MEDICAL_VISIT

MEDICAL_VISIT
N
|
|
N
DIAGNOSIS
```

La relación muchos a muchos entre consulta y diagnóstico deberá resolverse mediante una entidad asociativa:



```
VISIT_DIAGNOSES
```

[](https://i.ibb.co/nq376QYn/erd-sistema-de-historia-cl-nica-oftalmol-gica.png)

# 13. Proceso de normalización

Uno de los componentes principales del proyecto será demostrar el proceso de normalización.

La normalización deberá desarrollarse progresivamente.

# 14. Datos no normalizados

Podría partirse de una estructura como:

```
HISTORIA_CLINICA

paciente
documento
telefono
consulta_fecha
diagnosticos
medicamentos
presion_od
presion_oi
oct
campo_visual
```

Ejemplo:

```
Paciente:
Carlos Gómez

Diagnósticos:
Glaucoma, Catarata

Medicamentos:
Latanoprost, Timolol
```

Aquí existen valores multivaluados.

# 15. Primera Forma Normal —1FN

La 1FN exige:

- atributos atómicos;
- ausencia de grupos repetitivos;
- una celda debe contener un solo valor.

Incorrecto:

```
diagnosticos:
Glaucoma, Catarata
```

Correcto:

```
VISIT_DIAGNOSES

visit_id | diagnosis_id
------------------------
1        | 5
1        | 8
```

# 16. Segunda Forma Normal —2FN

La 2FN requiere:

- estar en 1FN;
- eliminar dependencias parciales respecto a claves compuestas.

Ejemplo:

```
VISIT_DIAGNOSES

visit_id
diagnosis_id
diagnosis_name
```

Si:

```
diagnosis_name
```

depende únicamente de:

```
diagnosis_id
```

debe trasladarse a:

```
DIAGNOSES
```

# 17. Tercera Forma Normal —3FN

La 3FN elimina dependencias transitivas.

Ejemplo incorrecto:

```
PATIENTS

patient_id
city_id
city_name
department_name
```

Si:

```
patient_id -> city_id
city_id -> city_name
```

entonces:

```
city_name
```

no debe almacenarse directamente en `patients`.

Se crean catálogos independientes.

# 18. Forma Normal de Boyce-Codd —BCNF

Cuando sea pertinente, deberán revisarse dependencias funcionales más estrictas.

Toda dependencia funcional:

```
X -> Y
```

deberá tener como determinante una superclave.

# 19. Cuarta Forma Normal —4FN

La 4FN será especialmente importante en este proyecto debido a la existencia de atributos multivaluados independientes.

Supóngase:

```
PATIENT

patient_id
allergy
family_history
```

Un paciente puede tener:

```
N alergias
```

y también:

```
N antecedentes familiares
```

ambos independientes.

Una única relación podría producir combinaciones artificiales:

```
Alergia A + Antecedente 1
Alergia A + Antecedente 2
Alergia B + Antecedente 1
Alergia B + Antecedente 2
```

Esto representa una dependencia multivaluada.

Para alcanzar 4FN deberían separarse:

```
PATIENT_ALLERGIES
```

y:

```
PATIENT_FAMILY_HISTORIES
```

# 20. Ejemplo de aplicación de 4FN en el proyecto

Otra situación:

Un paciente puede tener múltiples:

```
medicamentos
```

y múltiples:

```
antecedentes
```

Estos conjuntos no dependen entre sí.

Incorrecto:

```
patient_medications_histories
```

Correcto:

```
PATIENT_MEDICATIONS

patient_id
medication_id
```

y:

```
PATIENT_HISTORIES

patient_id
history_type_id
description
```

## Evidencia de la normalizacion 

### Primera Forma Normal (1FN)

La 1FN exige atributos atómicos, ausencia de grupos repetitivos y un solo valor por celda.

**Incorrecto:**

Guardar diagnósticos como una lista en un solo texto dentro de la consulta:

```
diagnosticos: "Glaucoma, Catarata"
```

**Correcto:** Se desacopla en la tabla de unión `VISIT_DIAGNOSIS`:   

| **visit_id** | **diagnosis_id** | **diagnosis_type** |
| ------------ | ---------------- | ------------------ |
| 1            | 5                | Principal          |
| 1            | 8                | Secundario         |

### Segunda Forma Normal (2FN)

La 2FN requiere estar en 1FN y **eliminar dependencias parciales** respecto a claves compuestas.

**Ejemplo incorrecto:**

Tener `diagnosis_name` dentro de la tabla intermedia con clave compuesta `(visit_id, diagnosis_id)`:

Plaintext

```
VISIT_DIAGNOSIS (visit_id, diagnosis_id, diagnosis_name)
```

**Correcto:** Como `diagnosis_name` depende únicamente de `diagnosis_id` (y no de `visit_id`), la descripción pertenece exclusivamente a la tabla del catálogo `DIAGNOSIS`:   

Plaintext

```
DIAGNOSIS (diagnosis_id [PK], code, name, description)
VISIT_DIAGNOSIS (visit_id [PK, FK], diagnosis_id [PK, FK], diagnosis_type)
```

De igual forma, en la tabla de tratamientos y medicamentos `TREATMENT_MEDICATION`, los atributos de dosis y frecuencia dependerán de la clave compuesta completa `(treatment_id, medication_id)`. 

### Tercera Forma Normal (3FN)

La 3FN elimina **dependencias transitivas** (atributos no clave que dependen de otros atributos no clave).

**Ejemplo incorrecto:** Guardar la ciudad y el departamento directamente en la persona o paciente:   

Plaintext

```
PERSON (person_id, city_id, city_name, department_name, country)
```

Como `person_id -> city_id` y `city_id -> (city_name, department_name, country)`, los campos del municipio no deben almacenarse en `PERSON`.   

**Correcto:** Se crean catálogos independientes:   

Plaintext

```
CITY (city_id [PK], name, department, country)
PERSON (person_id [PK], identification_number, first_name, last_name, city_id [FK])
```

### Forma Normal de Boyce-Codd (BCNF)

En toda dependencia funcional determinante ($X \rightarrow Y$), $X$ debe ser una **superclave**.

**Aplicación en el proyecto:** En la asignación de usuarios y roles (`USER_ACCOUNT` y `USER_ROLE`), la relación de credenciales entre la persona y su cuenta de usuario garantiza que cada dependencia funcional provenga directamente de una superclave única (`person_id` es clave alternativa/única en `USER_ACCOUNT`). 

### Cuarta Forma Normal (4FN)

La 4FN elimina **dependencias multivaluadas independientes** ($X \twoheadrightarrow Y$) para evitar productos cartesianos y combinaciones artificiales de datos.

Un paciente puede tener $N$ alergias y $N$ antecedentes médicos. Si intentáramos registrar ambos atributos en una sola relación alrededor del paciente, se generarían duplicaciones innecesarias:   

- Alergia A + Antecedente 1
- Alergia A + Antecedente 2
- Alergia B + Antecedente 1
- Alergia B + Antecedente 2

**Correcto:** Para alcanzar la 4FN en nuestro modelo, se separan en entidades totalmente independientes conectadas a la clave del paciente (`patient_id`):   

Plaintext

```
PATIENT_ALLERGY (patient_id [PK, FK], allergy_id [PK, FK], reaction, severity)
PATIENT_BACKGROUND (patient_background_id [PK], patient_id [FK], background_type_id [FK]
```

# 21. Implementación física en MySQL

Después de validar el modelo lógico, deberá construirse el modelo físico mediante:

```
CREATE DATABASE
CREATE TABLE
ALTER TABLE
```

Se deberán utilizar tipos apropiados como:

```
BIGINT
INT
VARCHAR
TEXT
DATE
DATETIME
DECIMAL
BOOLEAN
```

[](https://i.ibb.co/nq376QYn/erd-sistema-de-historia-cl-nica-oftalmol-gica.png)

# 22. Restricciones

El proyecto deberá implementar restricciones.

Ejemplo:

```
CREATE TABLE patients (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    document_number VARCHAR(30) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    birth_date DATE NOT NULL,

    CONSTRAINT uq_patient_document
        UNIQUE(document_number)
);
```

# 23. Integridad referencial

Ejemplo:

```
CREATE TABLE clinical_histories (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    patient_id BIGINT NOT NULL,

    CONSTRAINT uq_history_patient
        UNIQUE(patient_id),

    CONSTRAINT fk_history_patient
        FOREIGN KEY(patient_id)
        REFERENCES patients(id)
);
```

# 24. Datos de prueba

El proyecto deberá incluir información suficiente para validar las consultas.

Por ejemplo:

```
20 pacientes
5 profesionales
10 tipos de diagnósticos
30 consultas
50 mediciones PIO
20 OCT
20 campos visuales
15 tratamientos
```

Los datos deberán ser coherentes con las relaciones definidas.

# 25. Consultas básicas

Deberán desarrollarse consultas como:

```
SELECT *
FROM patients;
```

Buscar por identificación:

```
SELECT *
FROM patients
WHERE document_number = '1098123456';
```

Ordenar:

```
SELECT *
FROM patients
ORDER BY last_name;
```

# 26. Consultas intermedias

Deberán utilizarse:

```
JOIN
ORDER BY
GROUP BY
HAVING
DISTINCT
CASE
```

Ejemplo:

```
SELECT
    p.first_name,
    p.last_name,
    mv.visit_date
FROM patients p
INNER JOIN clinical_histories ch
    ON p.id = ch.patient_id
INNER JOIN medical_visits mv
    ON ch.id = mv.clinical_history_id;
```

# 27. Consultas avanzadas

Ejemplo:

Obtener cada paciente con su última consulta:

```
SELECT
    p.id,
    p.first_name,
    p.last_name,
    MAX(mv.visit_date) AS last_visit
FROM patients p
INNER JOIN clinical_histories ch
    ON p.id = ch.patient_id
INNER JOIN medical_visits mv
    ON ch.id = mv.clinical_history_id
GROUP BY
    p.id,
    p.first_name,
    p.last_name;
```

# 28. Subconsultas

Ejemplo:

Obtener pacientes con más consultas que el promedio:

```
SELECT
    patient_id,
    total_visits
FROM (
    SELECT
        ch.patient_id,
        COUNT(*) AS total_visits
    FROM clinical_histories ch
    INNER JOIN medical_visits mv
        ON ch.id = mv.clinical_history_id
    GROUP BY ch.patient_id
) x
WHERE total_visits > (
    SELECT AVG(total_visits)
    FROM (
        SELECT
            COUNT(*) AS total_visits
        FROM clinical_histories ch
        INNER JOIN medical_visits mv
            ON ch.id = mv.clinical_history_id
        GROUP BY ch.patient_id
    ) y
);
```

# 29. Funciones agregadas

El proyecto deberá utilizar:

```
COUNT
SUM
AVG
MIN
MAX
```

Ejemplo:

```
SELECT
    AVG(pressure) AS average_pressure,
    MIN(pressure) AS minimum_pressure,
    MAX(pressure) AS maximum_pressure
FROM intraocular_pressures;
```

# 30. GROUP BY

Ejemplo:

```
SELECT
    eye,
    AVG(pressure) AS average_pressure
FROM intraocular_pressures
GROUP BY eye;
```

# 31. HAVING

Ejemplo:

```
SELECT
    patient_id,
    COUNT(*) AS controls
FROM glaucoma_controls
GROUP BY patient_id
HAVING COUNT(*) >= 3;
```

# 32. Procedimientos almacenados

Deberán implementarse procedimientos que representen operaciones del dominio.

Ejemplo conceptual:

```
sp_create_medical_visit
sp_register_intraocular_pressure
sp_register_diagnosis
sp_get_patient_history
```

Ejemplo:

```
DELIMITER $$

CREATE PROCEDURE sp_get_patient_visits(
    IN p_patient_id BIGINT
)
BEGIN

    SELECT
        mv.id,
        mv.visit_date,
        mv.reason
    FROM clinical_histories ch
    INNER JOIN medical_visits mv
        ON ch.id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY mv.visit_date DESC;

END $$

DELIMITER ;
```

# 33. Funciones almacenadas

Ejemplo:

Calcular edad del paciente:

```
DELIMITER $$

CREATE FUNCTION fn_patient_age(
    p_birth_date DATE
)
RETURNS INT
DETERMINISTIC
BEGIN

    RETURN TIMESTAMPDIFF(
        YEAR,
        p_birth_date,
        CURDATE()
    );

END $$

DELIMITER ;
```

Consulta:

```
SELECT
    first_name,
    last_name,
    fn_patient_age(birth_date) AS age
FROM patients;
```

# 34. Triggers

Se deberán utilizar triggers cuando exista una justificación clara.

Ejemplo:

Crear auditoría automática de cambios.

```
CREATE TABLE audit_logs (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    table_name VARCHAR(100),
    record_id BIGINT,
    action VARCHAR(20),
    changed_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

Trigger:

```
DELIMITER $$

CREATE TRIGGER trg_patient_after_update
AFTER UPDATE
ON patients
FOR EACH ROW
BEGIN

    INSERT INTO audit_logs(
        table_name,
        record_id,
        action
    )
    VALUES(
        'patients',
        NEW.id,
        'UPDATE'
    );

END $$

DELIMITER ;
```

# 35. Otros triggers posibles

```
Auditar cambios en consultas
Auditar tratamientos
Registrar cambios de diagnóstico
Registrar eliminación lógica
Actualizar fechas de modificación
```

# 36. Eventos

Si se desea incorporar eventos MySQL, podrían utilizarse para tareas como:

```
limpieza periódica de registros temporales
generación de resúmenes
actualización de tablas de indicadores
```

Ejemplo:

```
CREATE EVENT ev_daily_statistics
ON SCHEDULE EVERY 1 DAY
DO
    CALL sp_generate_daily_statistics();
```

# 37. Vistas

También deberían incorporarse vistas.

Por ejemplo:

```
CREATE VIEW vw_patient_last_visit AS
SELECT
    p.id AS patient_id,
    CONCAT(p.first_name, ' ', p.last_name) AS patient,
    MAX(mv.visit_date) AS last_visit
FROM patients p
INNER JOIN clinical_histories ch
    ON p.id = ch.patient_id
INNER JOIN medical_visits mv
    ON ch.id = mv.clinical_history_id
GROUP BY
    p.id,
    p.first_name,
    p.last_name;
```

# 38. Posibles consultas requeridas

El proyecto podría exigir al estudiante construir al menos:

```
10 consultas básicas
10 consultas intermedias
10 consultas avanzadas
5 subconsultas
5 consultas con funciones agregadas
3 vistas
3 procedimientos almacenados
3 funciones
3 triggers
1 evento programado
```

# 39. Preguntas que la base de datos deberá responder

Algunos ejemplos:

1. ¿Cuántos pacientes se encuentran registrados?

   Los pacientes registrados son 10

2. ¿Cuántas consultas ha tenido cada paciente?

   | [ paciente](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+COUNT(mv.visit_id)+AS+total_consultas FROM+patient+p JOIN+person+pe+ON+pe.person_id+%3D+p.person_id LEFT+JOIN+clinical_history+ch+ON+ch.patient_id+%3D+p.patient_id LEFT+JOIN+medical_visit+mv+ON+mv.clinical_history_id+%3D+ch.clinical_history_id GROUP+BY+p.patient_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`paciente`+ASC+&sql_signature=86f74dde3ef4c1a666c928dcc03298e60de89f5f5dbcd57519137cd3aaf1f85c&session_max_rows=25&is_browse_distinct=0) |                 | [total_consultas](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+COUNT(mv.visit_id)+AS+total_consultas FROM+patient+p JOIN+person+pe+ON+pe.person_id+%3D+p.person_id LEFT+JOIN+clinical_history+ch+ON+ch.patient_id+%3D+p.patient_id LEFT+JOIN+medical_visit+mv+ON+mv.clinical_history_id+%3D+ch.clinical_history_id GROUP+BY+p.patient_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`total_consultas`+ASC+&sql_signature=60b9d00df3e7e99d65f1aecd561243549f94a2ea5269cde76be7c542fbe9d3ff&session_max_rows=25&is_browse_distinct=0) |
   | ------------------------------------------------------------ | --------------- | ------------------------------------------------------------ |
   | 1                                                            | Carlos Gmez     | 6                                                            |
   | 2                                                            | Mara Rodrguez   | 2                                                            |
   | 3                                                            | Juan Martnez    | 2                                                            |
   | 4                                                            | Laura Hernndez  | 1                                                            |
   | 5                                                            | Andrs Moreno    | 1                                                            |
   | 6                                                            | Paula Rojas     | 1                                                            |
   | 7                                                            | Diego Surez     | 1                                                            |
   | 8                                                            | Valentina Mora  | 1                                                            |
   | 9                                                            | Gabriel Mendoza | 0                                                            |
   | 10                                                           | Andrés Gómez    | 0                                                            |

3. ¿Cuál fue la última consulta de un paciente?

   | 1    | Carlos Gmez    | 2026-10-08 17:33:24 |
   | ---- | -------------- | ------------------- |
   | 2    | Mara Rodrguez  | 2026-06-20 11:00:00 |
   | 3    | Juan Martnez   | 2026-06-15 10:30:00 |
   | 4    | Laura Hernndez | 2026-06-10 08:05:00 |
   | 5    | Andrs Moreno   | 2026-05-20 10:00:00 |
   | 6    | Paula Rojas    | 2026-06-01 09:00:00 |
   | 7    | Diego Surez    | 2026-06-03 11:00:00 |
   | 8    | Valentina Mora | 2026-06-05 14:00:00 |

4. ¿Qué pacientes tienen diagnóstico de glaucoma?

   | [patient_id](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+gt.name+AS+tipo_glaucoma FROM+glaucoma_record+gr JOIN+patient+p+ON+p.patient_id+%3D+gr.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+glaucoma_type+gt+ON+gt.glaucoma_type_id+%3D+gr.glaucoma_type_id WHERE+gr.active+%3D+TRUE+ ORDER+BY+`p`.`patient_id`+ASC+&sql_signature=a926ade85adc05a8411503f51d60e9cc41c69e79cf1854993e7fbc55519d5b3f&session_max_rows=25&is_browse_distinct=0) | [paciente](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+gt.name+AS+tipo_glaucoma FROM+glaucoma_record+gr JOIN+patient+p+ON+p.patient_id+%3D+gr.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+glaucoma_type+gt+ON+gt.glaucoma_type_id+%3D+gr.glaucoma_type_id WHERE+gr.active+%3D+TRUE+ ORDER+BY+`paciente`+ASC+&sql_signature=733c8988064b24d461476b514f09407339753569c13ef1c86900e8388212cb3e&session_max_rows=25&is_browse_distinct=0) | [tipo_glaucoma](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+gt.name+AS+tipo_glaucoma FROM+glaucoma_record+gr JOIN+patient+p+ON+p.patient_id+%3D+gr.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+glaucoma_type+gt+ON+gt.glaucoma_type_id+%3D+gr.glaucoma_type_id WHERE+gr.active+%3D+TRUE+ ORDER+BY+`tipo_glaucoma`+ASC+&sql_signature=a2a40708d5fe04b3d95b18fdbcf453e558d9c29ab20c5a62f37024b4fedc4588&session_max_rows=25&is_browse_distinct=0) |      |
   | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
   | 2                                                            | Mara Rodrguez                                                | Glaucoma primario de ngulo abierto                           |      |
   | 6                                                            | Paula Rojas                                                  | Glaucoma primario de ngulo abierto                           |      |

5. ¿Cuántos pacientes existen por tipo de glaucoma?

   | tipo_glaucoma                      | cantidad_pacientes |      |
   | ---------------------------------- | ------------------ | ---- |
   | Glaucoma primario de ngulo abierto | 2                  |      |

6. ¿Cuál es la presión intraocular promedio por ojo?

   | [ojo](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=e&sql_query=SELECT+e.code+AS+ojo%2C+e.name+AS+descripcion_ojo%2C+AVG(iop.pressure_value)+AS+pio_promedio FROM+intraocular_pressure+iop JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id GROUP+BY+e.eye_id%2C+e.code%2C+e.name+ ORDER+BY+`ojo`+ASC+&sql_signature=12063cda269d71a9c5774e19f73d55f30cc232da75e34fc20e138f4633817368&session_max_rows=25&is_browse_distinct=0) | [descripcion_ojo](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=e&sql_query=SELECT+e.code+AS+ojo%2C+e.name+AS+descripcion_ojo%2C+AVG(iop.pressure_value)+AS+pio_promedio FROM+intraocular_pressure+iop JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id GROUP+BY+e.eye_id%2C+e.code%2C+e.name+ ORDER+BY+`descripcion_ojo`+ASC+&sql_signature=d616df49b808ac73c761b1767b51b418aebfbab6ae9b2caddec5c64bbae9693b&session_max_rows=25&is_browse_distinct=0) | [pio_promedio](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=e&sql_query=SELECT+e.code+AS+ojo%2C+e.name+AS+descripcion_ojo%2C+AVG(iop.pressure_value)+AS+pio_promedio FROM+intraocular_pressure+iop JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id GROUP+BY+e.eye_id%2C+e.code%2C+e.name+ ORDER+BY+`pio_promedio`+ASC+&sql_signature=d15296cb7b89cc81dbefb273d24fda364d58d810f53d36d96401b6c139cd0bb0&session_max_rows=25&is_browse_distinct=0) |      |
   | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
   | OD                                                           | Ojo derecho                                                  | 18.000000                                                    |      |
   | OS                                                           | Ojo izquierdo                                                | 16.666667                                                    |      |

7. ¿Cuál es la presión máxima registrada por paciente?

   | [patient_id](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=p&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+MAX(iop.pressure_value)+AS+pio_maxima FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id GROUP+BY+p.patient_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`p`.`patient_id`+ASC+&sql_signature=d5d183c088ede8d5ebe4d96fd65653a671b17f195cafb261e6201f7aab6dad4c&session_max_rows=25&is_browse_distinct=0) | [paciente](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=p&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+MAX(iop.pressure_value)+AS+pio_maxima FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id GROUP+BY+p.patient_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`paciente`+ASC+&sql_signature=9011f8e49b5341ab1ab1faeeb90a13ec247c5245d8e1d9032ad687c88a74b8fb&session_max_rows=25&is_browse_distinct=0) | [pio_maxima](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=p&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+MAX(iop.pressure_value)+AS+pio_maxima FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id GROUP+BY+p.patient_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`pio_maxima`+ASC+&sql_signature=d1ea04c264b7f042b938727f67d427929d92dd747c1847b18d7fe4c39e4f4e9d&session_max_rows=25&is_browse_distinct=0) |      |
   | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
   | 1                                                            | Carlos Gmez                                                  | 22.00                                                        |      |
   | 2                                                            | Mara Rodrguez                                                | 28.00                                                        |      |
   | 6                                                            | Paula Rojas                                                  | 14.00                                                        |      |

8. ¿Qué pacientes tienen más de tres controles de glaucoma?

   Ninguno tiene mas de tres controles de glaucoma

9. ¿Qué profesionales han atendido más pacientes?

   | [professional_id](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=healthcare_professional&sql_query=SELECT+hp.professional_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+profesional%2C+COUNT(DISTINCT+ch.patient_id)+AS+pacientes_atendidos FROM+healthcare_professional+hp JOIN+person+pe+ON+pe.person_id+%3D+hp.person_id JOIN+medical_visit+mv+ON+mv.professional_id+%3D+hp.professional_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id GROUP+BY+hp.professional_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`hp`.`professional_id`+ASC+&sql_signature=53c75ef2a4846617cfba754455bd88791027c040946dae3f380129e0e4482d89&session_max_rows=25&is_browse_distinct=0) | [profesional](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=healthcare_professional&sql_query=SELECT+hp.professional_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+profesional%2C+COUNT(DISTINCT+ch.patient_id)+AS+pacientes_atendidos FROM+healthcare_professional+hp JOIN+person+pe+ON+pe.person_id+%3D+hp.person_id JOIN+medical_visit+mv+ON+mv.professional_id+%3D+hp.professional_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id GROUP+BY+hp.professional_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`profesional`+ASC+&sql_signature=cf0f43e384787d5ec6e1b4594b128309f68c61a21f26907873850bf923f6e74e&session_max_rows=25&is_browse_distinct=0) | [pacientes_atendidos ![Descendente](http://localhost:8081/themes/dot.gif) 1](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=healthcare_professional&sql_query=SELECT+hp.professional_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+profesional%2C+COUNT(DISTINCT+ch.patient_id)+AS+pacientes_atendidos FROM+healthcare_professional+hp JOIN+person+pe+ON+pe.person_id+%3D+hp.person_id JOIN+medical_visit+mv+ON+mv.professional_id+%3D+hp.professional_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id GROUP+BY+hp.professional_id%2C+pe.first_name%2C+pe.last_name+ ORDER+BY+`pacientes_atendidos`+ASC+&sql_signature=ee33163444903a4f29815afda73f218b9b09f09c8a61e4f8b2d1e607ac955937&session_max_rows=25&is_browse_distinct=0) |      |
   | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
   | 1                                                            | Ricardo Beltrn                                               | 3                                                            |      |
   | 2                                                            | Claudia Duarte                                               | 2                                                            |      |
   | 3                                                            | Felipe Quintero                                              | 2                                                            |      |
   | 4                                                            | Natalia Pardo                                                | 2                                                            |      |

10. ¿Qué medicamentos son utilizados con mayor frecuencia?

    | [medicamento](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=m&sql_query=SELECT+m.name+AS+medicamento%2C+COUNT(tm.treatment_id)+AS+frecuencia_uso FROM+treatment_medication+tm JOIN+medication+m+ON+m.medication_id+%3D+tm.medication_id GROUP+BY+m.medication_id%2C+m.name+ ORDER+BY+`medicamento`+ASC+&sql_signature=bd67412f5e611120d8b859839a2b5e14475ab8de94bf05e7ad6443bf1ec2a5e3&session_max_rows=25&is_browse_distinct=0) | [frecuencia_uso ![Descendente](http://localhost:8081/themes/dot.gif) 1](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=m&sql_query=SELECT+m.name+AS+medicamento%2C+COUNT(tm.treatment_id)+AS+frecuencia_uso FROM+treatment_medication+tm JOIN+medication+m+ON+m.medication_id+%3D+tm.medication_id GROUP+BY+m.medication_id%2C+m.name+ ORDER+BY+`frecuencia_uso`+ASC+&sql_signature=3ddde0b15d6415e7f006e1ed9fec051b8bfcc1a67b478d9d8c3746cae2212251&session_max_rows=25&is_browse_distinct=0) |      |
    | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
    | Latanoprost                                                  | 2                                                            |      |
    | Timolol                                                      | 1                                                            |      |
    | Lgrimas artificiales                                         | 1                                                            |      |
    | Dorzolamida                                                  | 1                                                            |      |
    | Hialuronato de sodio                                         | 1                                                            |      |

11. ¿Cuántos estudios OCT se realizaron por mes?

    | [mes ![Ascendente](http://localhost:8081/themes/dot.gif) 1](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=clinical_exam&sql_query=SELECT+DATE_FORMAT(ce.exam_date%2C+'%Y-%m')+AS+mes%2C+COUNT(ce.clinical_exam_id)+AS+total_oct FROM+clinical_exam+ce JOIN+exam_type+et+ON+et.exam_type_id+%3D+ce.exam_type_id WHERE+et.name+LIKE+'%OCT%' GROUP+BY+DATE_FORMAT(ce.exam_date%2C+'%Y-%m')+ ORDER+BY+`mes`+ASC+&sql_signature=720c86433731b71e063fcd2d54e0ac48874cdc5bf9c47472a8c7e8da8be1d26c&session_max_rows=25&is_browse_distinct=0) | [total_oct](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=clinical_exam&sql_query=SELECT+DATE_FORMAT(ce.exam_date%2C+'%Y-%m')+AS+mes%2C+COUNT(ce.clinical_exam_id)+AS+total_oct FROM+clinical_exam+ce JOIN+exam_type+et+ON+et.exam_type_id+%3D+ce.exam_type_id WHERE+et.name+LIKE+'%OCT%' GROUP+BY+DATE_FORMAT(ce.exam_date%2C+'%Y-%m')+ ORDER+BY+`total_oct`+ASC+&sql_signature=0c704386169749145e3d8079ae623452ef88ab84fb5ef88e724a3eb0be074cf4&session_max_rows=25&is_browse_distinct=0) |      |
    | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
    | 2026-06                                                      | 2                                                            |      |
    | 2026-05                                                      | 3                                                            |      |

12. ¿Qué pacientes no han tenido consulta durante determinado período?

    el paciente gabriel y andrez gomez

13. ¿Cuál es la evolución de la presión intraocular de un paciente?

    | [patient_id ![Descendente](http://localhost:8081/themes/dot.gif) 1](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+mv.visit_date%2C+e.code+AS+ojo%2C+iop.pressure_value%2C+iop.unit FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id+ ORDER+BY+`p`.`patient_id`+DESC+&sql_signature=5fddd32070cdc70cb27d4c8f63560f0cf976c734f8949db8306272bf81acbd8e&session_max_rows=25&is_browse_distinct=0) | [paciente](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+mv.visit_date%2C+e.code+AS+ojo%2C+iop.pressure_value%2C+iop.unit FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id+ ORDER+BY+`paciente`+ASC+&sql_signature=cab075dab032ab5f3ee7a5237dd9b1316605dc1bf874af46424618c8969d5e06&session_max_rows=25&is_browse_distinct=0) | [visit_date](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+mv.visit_date%2C+e.code+AS+ojo%2C+iop.pressure_value%2C+iop.unit FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id+ ORDER+BY+`mv`.`visit_date`+DESC+&sql_signature=bbc1f6af6dc7c6f6a14d6c27b30e721b48ab4db5bcf4a15731123e44b1d7d596&session_max_rows=25&is_browse_distinct=0) | [ojo](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+mv.visit_date%2C+e.code+AS+ojo%2C+iop.pressure_value%2C+iop.unit FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id+ ORDER+BY+`ojo`+ASC+&sql_signature=ebb3eb9e9efd4412e2c7ec589bbcc49b00c4e9ebcbea2b366ec74f593c78dfc5&session_max_rows=25&is_browse_distinct=0) | [pressure_value](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+mv.visit_date%2C+e.code+AS+ojo%2C+iop.pressure_value%2C+iop.unit FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id+ ORDER+BY+`iop`.`pressure_value`+ASC+&sql_signature=1e06690eda17510b6505a2a24fd3a639687e301ec1613184960ac3e8e0fcc2fd&session_max_rows=25&is_browse_distinct=0) | [unit](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+mv.visit_date%2C+e.code+AS+ojo%2C+iop.pressure_value%2C+iop.unit FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id+ ORDER+BY+`iop`.`unit`+ASC+&sql_signature=c14c5e6efe2ff4631145a163d6f061a9eba2c5e30cb1d3731fab3cebdfc986be&session_max_rows=25&is_browse_distinct=0) |      |
    | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
    | 1                                                            | Carlos Gmez                                                  | 2026-05-04 08:05:00                                          | OD                                                           | 16.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-05-04 08:05:00                                          | OS                                                           | 17.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-05-04 08:05:00                                          | OD                                                           | 15.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-05-04 08:05:00                                          | OD                                                           | 22.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-05-04 08:05:00                                          | OS                                                           | 18.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-06-01 09:00:00                                          | OD                                                           | 22.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-06-01 09:00:00                                          | OS                                                           | 20.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-06-01 09:00:00                                          | OD                                                           | 14.00                                                        | mmHg                                                         |      |
    | 1                                                            | Carlos Gmez                                                  | 2026-06-01 09:00:00                                          | OS                                                           | 16.00                                                        | mmHg                                                         |      |
    | 2                                                            | Mara Rodrguez                                                | 2026-05-05 08:05:00                                          | OD                                                           | 14.00                                                        | mmHg                                                         |      |
    | 2                                                            | Mara Rodrguez                                                | 2026-05-05 08:05:00                                          | OS                                                           | 15.00                                                        | mmHg                                                         |      |
    | 2                                                            | Mara Rodrguez                                                | 2026-05-05 08:05:00                                          | OD                                                           | 18.00                                                        | mmHg                                                         |      |
    | 2                                                            | Mara Rodrguez                                                | 2026-05-05 08:05:00                                          | OD                                                           | 28.00                                                        | mmHg                                                         |      |
    | 6                                                            | Paula Rojas                                                  | 2026-06-01 09:00:00                                          | OD                                                           | 13.00                                                        | mmHg                                                         |      |
    | 6                                                            | Paula Rojas                                                  | 2026-06-01 09:00:00                                          | OS                                                           | 14.00                                                        | mmHg                                                         |      |

14. ¿Qué pacientes presentan valores de PIO superiores a determinado umbral?

    | [patient_id](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+iop.pressure_value%2C+e.code+AS+ojo%2C+iop.measured_at FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id WHERE+iop.pressure_value+>+21+ ORDER+BY+`p`.`patient_id`+ASC+&sql_signature=f52c93ce5a04ed9996f798952ffa3a87b2ec5fbb8d678efdf93d7c7a6f318e8e&session_max_rows=25&is_browse_distinct=0) | [paciente](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+iop.pressure_value%2C+e.code+AS+ojo%2C+iop.measured_at FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id WHERE+iop.pressure_value+>+21+ ORDER+BY+`paciente`+ASC+&sql_signature=55a63f99518d32fd5cc97d793963d68d7c1f54f6195e301cb55f8a53c4d99792&session_max_rows=25&is_browse_distinct=0) | [pressure_value](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+iop.pressure_value%2C+e.code+AS+ojo%2C+iop.measured_at FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id WHERE+iop.pressure_value+>+21+ ORDER+BY+`iop`.`pressure_value`+ASC+&sql_signature=6074b1c12fd11335adc707a6201e8de0bb7ffb86111dd82d98693c72693a96d5&session_max_rows=25&is_browse_distinct=0) | [ojo](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+iop.pressure_value%2C+e.code+AS+ojo%2C+iop.measured_at FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id WHERE+iop.pressure_value+>+21+ ORDER+BY+`ojo`+ASC+&sql_signature=279a260d88f8ba0088d92986656df29b867dad843333ae0097c86e2861ba3859&session_max_rows=25&is_browse_distinct=0) | [measured_at](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=patient&sql_query=SELECT+DISTINCT+p.patient_id%2C+CONCAT(pe.first_name%2C+'+'%2C+pe.last_name)+AS+paciente%2C+iop.pressure_value%2C+e.code+AS+ojo%2C+iop.measured_at FROM+intraocular_pressure+iop JOIN+medical_visit+mv+ON+mv.visit_id+%3D+iop.visit_id JOIN+clinical_history+ch+ON+ch.clinical_history_id+%3D+mv.clinical_history_id JOIN+patient+p+ON+p.patient_id+%3D+ch.patient_id JOIN+person+pe+ON+pe.person_id+%3D+p.person_id JOIN+eye+e+ON+e.eye_id+%3D+iop.eye_id WHERE+iop.pressure_value+>+21+ ORDER+BY+`iop`.`measured_at`+DESC+&sql_signature=a421453839b78dea6b14fcc449d92882f5a948e429a30171eb0f3b348b09ff0d&session_max_rows=25&is_browse_distinct=0) |      |
    | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
    | 1                                                            | Carlos Gmez                                                  | 22.00                                                        | OD                                                           | 2026-06-01 09:15:00                                          |      |
    | 1                                                            | Carlos Gmez                                                  | 22.00                                                        | OD                                                           | 2026-01-10 08:00:00                                          |      |
    | 2                                                            | Mara Rodrguez                                                | 28.00                                                        | OD                                                           | 2026-02-15 09:00:00                                          |      |

15. ¿Cuántos procedimientos se realizaron por tipo?

    | [tipo_procedimiento](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=mp&sql_query=SELECT+mp.name+AS+tipo_procedimiento%2C+COUNT(vp.visit_procedure_id)+AS+total_realizados FROM+visit_procedure+vp JOIN+medical_procedure+mp+ON+mp.procedure_id+%3D+vp.procedure_id GROUP+BY+mp.procedure_id%2C+mp.name+ ORDER+BY+`tipo_procedimiento`+ASC+&sql_signature=c9798487fa69b1924d64418aa043c07f86f2875110c1be8248b7bfce049846d3&session_max_rows=25&is_browse_distinct=0) | [total_realizados ![Descendente](http://localhost:8081/themes/dot.gif) 1](http://localhost:8081/index.php?route=/sql&db=historia_clinica_oftalmologica&table=mp&sql_query=SELECT+mp.name+AS+tipo_procedimiento%2C+COUNT(vp.visit_procedure_id)+AS+total_realizados FROM+visit_procedure+vp JOIN+medical_procedure+mp+ON+mp.procedure_id+%3D+vp.procedure_id GROUP+BY+mp.procedure_id%2C+mp.name+ ORDER+BY+`total_realizados`+ASC+&sql_signature=3e04ddf38d030166a8c0a5182afc1109fe5da6d6a1007f8e1f30d75a67e869c3&session_max_rows=25&is_browse_distinct=0) |      |
    | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
    | Tonometra                                                    | 4                                                            |      |
    | Oftalmoscopia                                                | 2                                                            |      |
    | Campimetra                                                   | 1                                                            |      |
    | Biometra ocular                                              | 1                                                            |      |

## Identificación de Entidades y Atributos

A partir del modelo de la historia clínica oftalmológica, el sistema se divide en **10 módulos conceptuales**:

1. **Ubicación y Geografía:** `city`, `clinic`, `location`, `room`
2. **Personas y Usuarios:** `identification_type`, `person`, `user_account`, `role`, `permission`, `user_role`, `role_permission`, `audit_log`
3. **Personal Médico y Agenda:** `specialty`, `healthcare_professional`, `professional_specialty`, `professional_schedule`, `schedule_exception`
4. **Pacientes y Antecedentes:** `patient`, `background_type`, `patient_background`, `allergy`, `patient_allergy`, `clinical_history`
5. **Agendamiento:** `appointment_status`, `appointment_reason`, `appointment_type`, `appointment`, `appointment_status_history`
6. **Consultas Médicas:** `visit_type`, `medical_visit`, `diagnosis`, `visit_diagnosis`, `medical_procedure`, `visit_procedure`, `eye`
7. **Documentos Clínicos:** `document_type`, `clinical_document`
8. **Tratamientos y Medicamentos:** `treatment_status`, `treatment`, `medication`, `treatment_medication`
9. **Exámenes y Mediciones:** `unit_of_measure`, `exam_type`, `exam_parameter`, `exam_parameter_option`, `clinical_exam`, `exam_result`
10. **Módulo Específico Oftalmológico (Glaucoma y PIO):** `intraocular_pressure`, `glaucoma_type`, `glaucoma_record`, `glaucoma_control`, `alert`

## Diccionario de Datos

#### 1. Ubicación y Geografía

##### Tabla: `city`

*Descripción: Ciudades para la ubicación de personas y clínicas.*

| **Campo**    | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                      |
| ------------ | ---------------- | --------- | ------------- | -------------------------------------------------- |
| `city_id`    | BIGINT           | PK        | Sí            | Identificador único de la ciudad (Auto-increment). |
| `name`       | VARCHAR(100)     | -         | Sí            | Nombre de la ciudad.                               |
| `department` | VARCHAR(100)     | -         | Sí            | Departamento / Estado.                             |
| `country`    | VARCHAR(100)     | -         | Sí            | País de la ciudad.                                 |

##### Tabla: `clinic`

*Descripción: Información general de la institución de salud.*

| **Campo**   | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**           |
| ----------- | ---------------- | --------- | ------------- | --------------------------------------- |
| `clinic_id` | BIGINT           | PK        | Sí            | Identificador único de la clínica.      |
| `name`      | VARCHAR(150)     | -         | Sí            | Nombre de la institución médica.        |
| `address`   | VARCHAR(250)     | -         | Sí            | Dirección principal.                    |
| `phone`     | VARCHAR(30)      | -         | Sí            | Teléfono de contacto.                   |
| `email`     | VARCHAR(150)     | -         | Sí            | Correo institucional.                   |
| `active`    | BOOLEAN          | -         | Sí            | Estado activo/inactivo (Default: TRUE). |

##### Tabla: `location`

*Descripción: Sede o sucursal de la clínica.*

| **Campo**     | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**             |
| ------------- | ---------------- | --------- | ------------- | ----------------------------------------- |
| `location_id` | BIGINT           | PK        | Sí            | Identificador único de la sede.           |
| `clinic_id`   | BIGINT           | FK        | Sí            | Referencia a `clinic(clinic_id)`.         |
| `name`        | VARCHAR(150)     | -         | Sí            | Nombre de la sede.                        |
| `address`     | VARCHAR(250)     | -         | Sí            | Dirección de la sede.                     |
| `active`      | BOOLEAN          | -         | Sí            | Estado de disponibilidad (Default: TRUE). |

##### Tabla: `room`

*Descripción: Consultorios y salas físicas.*

| **Campo**     | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                      |
| ------------- | ---------------- | --------- | ------------- | -------------------------------------------------- |
| `room_id`     | BIGINT           | PK        | Sí            | Identificador único del consultorio.               |
| `location_id` | BIGINT           | FK        | Sí            | Referencia a `location(location_id)`.              |
| `name`        | VARCHAR(100)     | -         | Sí            | Nombre o número del consultorio.                   |
| `floor`       | VARCHAR(50)      | -         | No            | Piso o nivel dentro de la sede.                    |
| `active`      | BOOLEAN          | -         | Sí            | Disponibilidad física del espacio (Default: TRUE). |

#### 2. Personas, Usuarios y Seguridad

##### Tabla: `identification_type`

*Descripción: Tipos de documento de identidad (CC, CE, Pasaporte, etc.).*

| **Campo**                | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                 |
| ------------------------ | ---------------- | --------- | ------------- | --------------------------------------------- |
| `identification_type_id` | BIGINT           | PK        | Sí            | Identificador único del tipo de documento.    |
| `code`                   | VARCHAR(50)      | UK        | Sí            | Código corto del documento (CC, TI, PAS, CE). |
| `name`                   | VARCHAR(100)     | -         | Sí            | Nombre completo del tipo de documento.        |
| `description`            | VARCHAR(150)     | -         | No            | Descripción complementaria.                   |

##### Tabla: `person`

*Descripción: Registro base unificado para personas (Pacientes, Médicos, Usuarios).*

| **Campo**                | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                               |
| ------------------------ | ---------------- | --------- | ------------- | ----------------------------------------------------------- |
| `person_id`              | BIGINT           | PK        | Sí            | Identificador único de la persona.                          |
| `identification_type_id` | BIGINT           | FK        | Sí            | Referencia a `identification_type(identification_type_id)`. |
| `identification_number`  | VARCHAR(100)     | UK        | Sí            | Número único de documento de identidad.                     |
| `first_name`             | VARCHAR(100)     | -         | Sí            | Primer nombre.                                              |
| `middle_name`            | VARCHAR(100)     | -         | No            | Segundo nombre.                                             |
| `last_name`              | VARCHAR(100)     | -         | Sí            | Primer apellido.                                            |
| `second_last_name`       | VARCHAR(100)     | -         | No            | Segundo apellido.                                           |
| `birth_date`             | DATE             | -         | Sí            | Fecha de nacimiento.                                        |
| `gender`                 | VARCHAR(20)      | -         | Sí            | Género registrado.                                          |
| `phone`                  | VARCHAR(30)      | -         | No            | Teléfono de contacto.                                       |
| `email`                  | VARCHAR(150)     | -         | No            | Correo electrónico personal.                                |
| `address`                | VARCHAR(250)     | -         | No            | Dirección residencial.                                      |
| `city_id`                | BIGINT           | FK        | Sí            | Referencia a `city(city_id)`.                               |

##### Tabla: `user_account`

*Descripción: Cuentas de acceso al sistema.*

| **Campo**       | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                   |
| --------------- | ---------------- | --------- | ------------- | ----------------------------------------------- |
| `user_id`       | BIGINT           | PK        | Sí            | Identificador único de usuario.                 |
| `person_id`     | BIGINT           | FK, UK    | Sí            | Referencia a `person(person_id)`. Relación 1:1. |
| `username`      | VARCHAR(100)     | UK        | Sí            | Nombre de usuario único de sesión.              |
| `password_hash` | VARCHAR(255)     | -         | Sí            | Contraseña encriptada (Hash).                   |
| `active`        | BOOLEAN          | -         | Sí            | Estado de la cuenta de usuario (Default: TRUE). |
| `created_at`    | DATETIME         | -         | Sí            | Fecha y hora de creación de la cuenta.          |
| `last_login`    | DATETIME         | -         | No            | Registro del último inicio de sesión.           |

##### Tabla: `role`

*Descripción: Roles del sistema (Médico, Recepcionista, Administrador).*

| **Campo**     | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**    |
| ------------- | ---------------- | --------- | ------------- | -------------------------------- |
| `role_id`     | BIGINT           | PK        | Sí            | Identificador único del rol.     |
| `name`        | VARCHAR(100)     | UK        | Sí            | Nombre del rol.                  |
| `description` | VARCHAR(250)     | -         | No            | Descripción del alcance del rol. |
| `active`      | BOOLEAN          | -         | Sí            | Estado del rol (Default: TRUE).  |

##### Tabla: `permission`

*Descripción: Permisos atómicos del sistema.*

| **Campo**       | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**        |
| --------------- | ---------------- | --------- | ------------- | ------------------------------------ |
| `permission_id` | BIGINT           | PK        | Sí            | Identificador único del permiso.     |
| `name`          | VARCHAR(100)     | UK        | Sí            | Nombre/Código de acción del permiso. |
| `description`   | VARCHAR(250)     | -         | No            | Descripción de la acción permitida.  |

##### Tabla: `user_role`

*Descripción: Tabla intermedia entre usuarios y roles (N:M).*

| **Campo** | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**         |
| --------- | ---------------- | --------- | ------------- | ------------------------------------- |
| `user_id` | BIGINT           | PK, FK    | Sí            | Referencia a `user_account(user_id)`. |
| `role_id` | BIGINT           | PK, FK    | Sí            | Referencia a `role(role_id)`.         |

##### Tabla: `role_permission`

*Descripción: Tabla intermedia entre roles y permisos (N:M).*

| **Campo**       | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**             |
| --------------- | ---------------- | --------- | ------------- | ----------------------------------------- |
| `role_id`       | BIGINT           | PK, FK    | Sí            | Referencia a `role(role_id)`.             |
| `permission_id` | BIGINT           | PK, FK    | Sí            | Referencia a `permission(permission_id)`. |

##### Tabla: `audit_log`

*Descripción: Historial de auditoría para cambios en el sistema.*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                               |
| -------------- | ---------------- | --------- | ------------- | ----------------------------------------------------------- |
| `audit_log_id` | BIGINT           | PK        | Sí            | Identificador único de la auditoría.                        |
| `user_id`      | BIGINT           | FK        | Sí            | Referencia a `user_account(user_id)` que realizó la acción. |
| `action`       | VARCHAR(100)     | -         | Sí            | Acción ejecutada (INSERT, UPDATE, DELETE).                  |
| `table_name`   | VARCHAR(100)     | -         | Sí            | Tabla afectada.                                             |
| `record_id`    | BIGINT           | -         | Sí            | ID del registro modificado.                                 |
| `old_values`   | TEXT             | -         | No            | JSON o datos previos al cambio.                             |
| `new_values`   | TEXT             | -         | No            | JSON o datos posteriores al cambio.                         |
| `created_at`   | DATETIME         | -         | Sí            | Marca de tiempo del evento.                                 |

#### 3. Personal Médico y Agenda

##### Tabla: `specialty`

*Descripción: Especialidades y subespecialidades médicas.*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**            |
| -------------- | ---------------- | --------- | ------------- | ---------------------------------------- |
| `specialty_id` | BIGINT           | PK        | Sí            | Identificador único de la especialidad.  |
| `name`         | VARCHAR(100)     | UK        | Sí            | Nombre (ej. Oftalmología, Glaucoma).     |
| `description`  | VARCHAR(250)     | -         | No            | Descripción temática de la especialidad. |
| `active`       | BOOLEAN          | -         | Sí            | Estado (Default: TRUE).                  |

##### Tabla: `healthcare_professional`

*Descripción: Información del profesional de la salud.*

| **Campo**              | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**             |
| ---------------------- | ---------------- | --------- | ------------- | ----------------------------------------- |
| `professional_id`      | BIGINT           | PK        | Sí            | Identificador único del profesional.      |
| `person_id`            | BIGINT           | FK, UK    | Sí            | Referencia a `person(person_id)`.         |
| `professional_license` | VARCHAR(50)      | UK        | Sí            | Número de tarjeta o licencia profesional. |
| `active`               | BOOLEAN          | -         | Sí            | Estado operativo (Default: TRUE).         |

##### Tabla: `professional_specialty`

*Descripción: Relación entre médico y sus especialidades (N:M).*

| **Campo**         | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                            |
| ----------------- | ---------------- | --------- | ------------- | -------------------------------------------------------- |
| `professional_id` | BIGINT           | PK, FK    | Sí            | Referencia a `healthcare_professional(professional_id)`. |
| `specialty_id`    | BIGINT           | PK, FK    | Sí            | Referencia a `specialty(specialty_id)`.                  |

##### Tabla: `professional_schedule`

*Descripción: Agenda recurrente de atención del profesional.*

| **Campo**         | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                            |
| ----------------- | ---------------- | --------- | ------------- | -------------------------------------------------------- |
| `schedule_id`     | BIGINT           | PK        | Sí            | Identificador de la franja horaria.                      |
| `professional_id` | BIGINT           | FK        | Sí            | Referencia a `healthcare_professional(professional_id)`. |
| `room_id`         | BIGINT           | FK        | Sí            | Referencia a `room(room_id)`.                            |
| `day_of_week`     | SMALLINT         | -         | Sí            | Día de la semana (1 a 7).                                |
| `start_time`      | TIME             | -         | Sí            | Hora de inicio de atención.                              |
| `end_time`        | TIME             | -         | Sí            | Hora de finalización.                                    |
| `active`          | BOOLEAN          | -         | Sí            | Estado del horario.                                      |

##### Tabla: `schedule_exception`

*Descripción: Bloqueos de agenda, vacaciones o ausencias de médicos.*

| **Campo**        | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                      |
| ---------------- | ---------------- | --------- | ------------- | -------------------------------------------------- |
| `exception_id`   | BIGINT           | PK        | Sí            | Identificador de la excepción de agenda.           |
| `schedule_id`    | BIGINT           | FK        | Sí            | Referencia a `professional_schedule(schedule_id)`. |
| `exception_date` | DATE             | -         | Sí            | Fecha puntual de la novedad.                       |
| `reason`         | VARCHAR(250)     | -         | No            | Motivo de la no disponibilidad.                    |
| `available`      | BOOLEAN          | -         | Sí            | Indica si se habilita o inhabilita el día.         |

#### 4. Pacientes y Historia Clínica Base

##### Tabla: `patient`

*Descripción: Registro de paciente en el sistema.*

| **Campo**        | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**     |
| ---------------- | ---------------- | --------- | ------------- | --------------------------------- |
| `patient_id`     | BIGINT           | PK        | Sí            | Identificador único de paciente.  |
| `person_id`      | BIGINT           | FK, UK    | Sí            | Referencia a `person(person_id)`. |
| `admission_date` | DATE             | -         | Sí            | Fecha de alta/ingreso al sistema. |
| `active`         | BOOLEAN          | -         | Sí            | Estado del paciente.              |

##### Tabla: `background_type`

*Descripción: Tipos de antecedentes (Patológicos, Quirúrgicos, Familiares).*

| **Campo**            | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**          |
| -------------------- | ---------------- | --------- | ------------- | -------------------------------------- |
| `background_type_id` | BIGINT           | PK        | Sí            | Identificador del tipo de antecedente. |
| `name`               | VARCHAR(100)     | UK        | Sí            | Nombre de la categoría.                |
| `description`        | VARCHAR(250)     | -         | No            | Descripción de la categoría.           |

##### Tabla: `patient_background`

*Descripción: Antecedentes clínicos del paciente (4NF).*

| **Campo**               | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                       |
| ----------------------- | ---------------- | --------- | ------------- | --------------------------------------------------- |
| `patient_background_id` | BIGINT           | PK        | Sí            | Identificador del registro.                         |
| `patient_id`            | BIGINT           | FK        | Sí            | Referencia a `patient(patient_id)`.                 |
| `background_type_id`    | BIGINT           | FK        | Sí            | Referencia a `background_type(background_type_id)`. |
| `description`           | TEXT             | -         | Sí            | Detalle del antecedente médico.                     |
| `start_date`            | DATE             | -         | No            | Fecha aproximada de diagnóstico.                    |
| `end_date`              | DATE             | -         | No            | Fecha de resolución/fin (si aplica).                |
| `active`                | BOOLEAN          | -         | Sí            | Estado del antecedente.                             |

##### Tabla: `allergy`

*Descripción: Catálogo general de alergias.*

| **Campo**     | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**      |
| ------------- | ---------------- | --------- | ------------- | ---------------------------------- |
| `allergy_id`  | BIGINT           | PK        | Sí            | Identificador único de la alergia. |
| `name`        | VARCHAR(100)     | UK        | Sí            | Nombre de la sustancia/alérgeno.   |
| `description` | VARCHAR(250)     | -         | No            | Descripción o categoría.           |

##### Tabla: `patient_allergy`

*Descripción: Alergias reportadas por paciente (4NF).*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                |
| -------------- | ---------------- | --------- | ------------- | -------------------------------------------- |
| `patient_id`   | BIGINT           | PK, FK    | Sí            | Referencia a `patient(patient_id)`.          |
| `allergy_id`   | BIGINT           | PK, FK    | Sí            | Referencia a `allergy(allergy_id)`.          |
| `reaction`     | VARCHAR(250)     | -         | No            | Síntomas o manifestaciones clínicas.         |
| `severity`     | VARCHAR(50)      | -         | No            | Grado de severidad (Leve, Moderada, Severa). |
| `observations` | TEXT             | -         | No            | Comentarios adicionales.                     |

##### Tabla: `clinical_history`

*Descripción: Expediente o Historia Clínica electrónica del paciente.*

| **Campo**             | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                     |
| --------------------- | ---------------- | --------- | ------------- | ------------------------------------------------- |
| `clinical_history_id` | BIGINT           | PK        | Sí            | Identificador de la historia clínica.             |
| `patient_id`          | BIGINT           | FK, UK    | Sí            | Referencia a `patient(patient_id)`.               |
| `history_number`      | VARCHAR(50)      | UK        | Sí            | Código formateado de la historia (ej: HC-000100). |
| `created_at`          | DATETIME         | -         | Sí            | Fecha de apertura del expediente.                 |
| `updated_at`          | DATETIME         | -         | No            | Última actualización del expediente.              |

#### 5. Agendamiento de Citas

##### Tabla: `appointment_status`

*Descripción: Estados de una cita (Programada, Confirmada, Cancelada, Atendida).*

| **Campo**               | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción** |
| ----------------------- | ---------------- | --------- | ------------- | ----------------------------- |
| `appointment_status_id` | BIGINT           | PK        | Sí            | Identificador del estado.     |
| `name`                  | VARCHAR(80)      | UK        | Sí            | Nombre del estado de la cita. |
| `description`           | VARCHAR(250)     | -         | No            | Descripción descriptiva.      |

##### Tabla: `appointment_reason`

*Descripción: Motivos estandarizados de asignación de cita.*

| **Campo**               | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                              |
| ----------------------- | ---------------- | --------- | ------------- | ---------------------------------------------------------- |
| `appointment_reason_id` | BIGINT           | PK        | Sí            | Identificador del motivo.                                  |
| `name`                  | VARCHAR(150)     | UK        | Sí            | Título del motivo (Valoración inicial, Control PIO, etc.). |
| `description`           | VARCHAR(250)     | -         | No            | Descripción detallada.                                     |

##### Tabla: `appointment_type`

*Descripción: Modalidad y duración estimada de cita.*

| **Campo**             | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**               |
| --------------------- | ---------------- | --------- | ------------- | ------------------------------------------- |
| `appointment_type_id` | BIGINT           | PK        | Sí            | Identificador del tipo de cita.             |
| `name`                | VARCHAR(100)     | UK        | Sí            | Nombre (Primera vez, Control, Prioritaria). |
| `description`         | VARCHAR(250)     | -         | No            | Descripción del procedimiento de cita.      |
| `duration_minutes`    | INT              | -         | Sí            | Duración programada en minutos.             |

##### Tabla: `appointment`

*Descripción: Registro de citas médicas agendadas.*

| **Campo**               | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                             |
| ----------------------- | ---------------- | --------- | ------------- | --------------------------------------------------------- |
| `appointment_id`        | BIGINT           | PK        | Sí            | Identificador único de la cita.                           |
| `patient_id`            | BIGINT           | FK        | Sí            | Referencia a `patient(patient_id)`.                       |
| `professional_id`       | BIGINT           | FK        | Sí            | Referencia a `healthcare_professional(professional_id)`.  |
| `room_id`               | BIGINT           | FK        | Sí            | Referencia a `room(room_id)`.                             |
| `appointment_status_id` | BIGINT           | FK        | Sí            | Referencia a `appointment_status(appointment_status_id)`. |
| `appointment_reason_id` | BIGINT           | FK        | Sí            | Referencia a `appointment_reason(appointment_reason_id)`. |
| `appointment_type_id`   | BIGINT           | FK        | Sí            | Referencia a `appointment_type(appointment_type_id)`.     |
| `scheduled_start`       | DATETIME         | -         | Sí            | Fecha y hora de inicio agendada.                          |
| `scheduled_end`         | DATETIME         | -         | Sí            | Fecha y hora proyectada de cierre.                        |
| `notes`                 | TEXT             | -         | No            | Notas adicionales sobre el agendamiento.                  |
| `created_at`            | DATETIME         | -         | Sí            | Fecha en que fue agendada.                                |

##### Tabla: `appointment_status_history`

*Descripción: Trazabilidad histórica de cambios de estado de cita.*

| **Campo**               | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                     |
| ----------------------- | ---------------- | --------- | ------------- | ------------------------------------------------- |
| `status_history_id`     | BIGINT           | PK        | Sí            | Identificador del histórico.                      |
| `appointment_id`        | BIGINT           | FK        | Sí            | Referencia a `appointment(appointment_id)`.       |
| `appointment_status_id` | BIGINT           | FK        | Sí            | Referencia al nuevo estado asignado.              |
| `changed_by`            | BIGINT           | FK        | Sí            | Usuario que modificó la cita (`user_account`).    |
| `changed_at`            | DATETIME         | -         | Sí            | Marca de tiempo de modificación.                  |
| `comments`              | VARCHAR(250)     | -         | No            | Observaciones de la reprogramación o cancelación. |

#### 6. Consultas Médicas y Procedimientos

##### Tabla: `eye`

*Descripción: Catálogo de lateralidad de los ojos.*

| **Campo** | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                                |
| --------- | ---------------- | --------- | ------------- | ------------------------------------------------------------ |
| `eye_id`  | BIGINT           | PK        | Sí            | Identificador del ojo.                                       |
| `code`    | VARCHAR(20)      | UK        | Sí            | Código estándar (`OD`: Ojo Derecho, `OI`: Ojo Izquierdo, `OU`: Ambos Ojos). |
| `name`    | VARCHAR(100)     | -         | Sí            | Nombre largo del ojo evaluado.                               |

##### Tabla: `visit_type`

*Descripción: Tipo de atención médica.*

| **Campo**       | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                    |
| --------------- | ---------------- | --------- | ------------- | ------------------------------------------------ |
| `visit_type_id` | BIGINT           | PK        | Sí            | Identificador de tipo de atención.               |
| `name`          | VARCHAR(100)     | UK        | Sí            | Nombre (Consulta presencial, Urgencia, Control). |
| `description`   | VARCHAR(250)     | -         | No            | Descripción descriptiva.                         |

##### Tabla: `medical_visit`

*Descripción: Registro de una consulta médica efectuada.*

| **Campo**             | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                         |
| --------------------- | ---------------- | --------- | ------------- | ----------------------------------------------------- |
| `visit_id`            | BIGINT           | PK        | Sí            | Identificador único de la consulta.                   |
| `clinical_history_id` | BIGINT           | FK        | Sí            | Referencia a `clinical_history(clinical_history_id)`. |
| `appointment_id`      | BIGINT           | FK        | No            | Cita que generó la atención (si aplica).              |
| `professional_id`     | BIGINT           | FK        | Sí            | Profesional atendiente.                               |
| `visit_type_id`       | BIGINT           | FK        | Sí            | Referencia a `visit_type(visit_type_id)`.             |
| `visit_date`          | DATETIME         | -         | Sí            | Fecha y hora real de atención.                        |
| `reason`              | TEXT             | -         | Sí            | Anamnesis / Motivo expresado por el paciente.         |
| `observations`        | TEXT             | -         | No            | Observaciones médicas del especialista.               |

##### Tabla: `diagnosis`

*Descripción: Catálogo CIE-10/CIE-11 de diagnósticos.*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                   |
| -------------- | ---------------- | --------- | ------------- | ----------------------------------------------- |
| `diagnosis_id` | BIGINT           | PK        | Sí            | Identificador del diagnóstico.                  |
| `code`         | VARCHAR(50)      | UK        | Sí            | Código oficial de patología.                    |
| `name`         | VARCHAR(200)     | -         | Sí            | Nombre completo del diagnóstico.                |
| `description`  | VARCHAR(500)     | -         | No            | Criterios y anotaciones del diagnóstico.        |
| `active`       | BOOLEAN          | -         | Sí            | Disponibilidad del diagnóstico (Default: TRUE). |

##### Tabla: `visit_diagnosis`

*Descripción: Diagnósticos emitidos en una consulta (1NF / 2NF).*

| **Campo**        | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                            |
| ---------------- | ---------------- | --------- | ------------- | -------------------------------------------------------- |
| `visit_id`       | BIGINT           | PK, FK    | Sí            | Referencia a `medical_visit(visit_id)`.                  |
| `diagnosis_id`   | BIGINT           | PK, FK    | Sí            | Referencia a `diagnosis(diagnosis_id)`.                  |
| `diagnosis_type` | VARCHAR(50)      | -         | Sí            | Clasificación (`Principal`, `Secundario`, `Presuntivo`). |
| `observations`   | TEXT             | -         | No            | Anotaciones clínicas complementarias del diagnóstico.    |

##### Tabla: `medical_procedure`

*Descripción: Catálogo de procedimientos médicos u oftalmológicos.*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**    |
| -------------- | ---------------- | --------- | ------------- | -------------------------------- |
| `procedure_id` | BIGINT           | PK        | Sí            | Identificador del procedimiento. |
| `code`         | VARCHAR(50)      | UK        | Sí            | Código de tarifario o CUPS.      |
| `name`         | VARCHAR(100)     | -         | Sí            | Nombre del procedimiento médico. |
| `description`  | VARCHAR(500)     | -         | No            | Descripción de ejecución.        |
| `active`       | BOOLEAN          | -         | Sí            | Estado del registro.             |

##### Tabla: `visit_procedure`

*Descripción: Procedimientos efectuados durante una consulta.*

| **Campo**            | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                   |
| -------------------- | ---------------- | --------- | ------------- | ----------------------------------------------- |
| `visit_procedure_id` | BIGINT           | PK        | Sí            | Identificador único de la ejecución.            |
| `visit_id`           | BIGINT           | FK        | Sí            | Referencia a `medical_visit(visit_id)`.         |
| `procedure_id`       | BIGINT           | FK        | Sí            | Referencia a `medical_procedure(procedure_id)`. |
| `professional_id`    | BIGINT           | FK        | Sí            | Médico ejecutor.                                |
| `eye_id`             | BIGINT           | FK        | Sí            | Ojo intervenido (OD/OI/OU).                     |
| `performed_at`       | DATETIME         | -         | Sí            | Marca de tiempo del procedimiento.              |
| `observations`       | TEXT             | -         | No            | Complicaciones o detalles del procedimiento.    |

#### 7. Documentos Clínicos

##### Tabla: `document_type`

*Descripción: Tipos de adjuntos (Consentimientos, Resultados externos, Firma).*

| **Campo**          | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**        |
| ------------------ | ---------------- | --------- | ------------- | ------------------------------------ |
| `document_type_id` | BIGINT           | PK        | Sí            | Identificador único.                 |
| `name`             | VARCHAR(100)     | UK        | Sí            | Nombre de la categoría de documento. |
| `description`      | VARCHAR(250)     | -         | No            | Detalle del propósito.               |

##### Tabla: `clinical_document`

*Descripción: Archivos digitalizados anexados a las consultas.*

| **Campo**          | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                  |
| ------------------ | ---------------- | --------- | ------------- | ---------------------------------------------- |
| `document_id`      | BIGINT           | PK        | Sí            | Identificador único del archivo.               |
| `visit_id`         | BIGINT           | FK        | Sí            | Consulta a la que se asocia.                   |
| `document_type_id` | BIGINT           | FK        | Sí            | Categoría del documento.                       |
| `uploaded_by`      | BIGINT           | FK        | Sí            | Usuario que cargó el archivo (`user_account`). |
| `deleted_by`       | BIGINT           | FK        | No            | Usuario que realizó borrado lógico.            |
| `file_name`        | VARCHAR(255)     | -         | Sí            | Nombre original del archivo en disco/servidor. |
| `file_path`        | VARCHAR(500)     | -         | Sí            | Ruta lógica o URL del objeto almacenado.       |
| `mime_type`        | VARCHAR(100)     | -         | Sí            | Formato mime (PDF, PNG, JPEG).                 |
| `uploaded_at`      | DATETIME         | -         | Sí            | Fecha de carga del sistema.                    |
| `deleted_at`       | DATETIME         | -         | No            | Fecha de eliminación (Soft delete).            |

#### 8. Medicación y Tratamientos

##### Tabla: `treatment_status`

*Descripción: Estados del tratamiento (Activo, Finalizado, Suspendido).*

| **Campo**             | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**  |
| --------------------- | ---------------- | --------- | ------------- | ------------------------------ |
| `treatment_status_id` | BIGINT           | PK        | Sí            | Identificador del estado.      |
| `name`                | VARCHAR(80)      | UK        | Sí            | Nombre descriptivo del estado. |
| `description`         | VARCHAR(250)     | -         | No            | Detalles del estado.           |

##### Tabla: `treatment`

*Descripción: Plan terapéutico indicado en una atención.*

| **Campo**             | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**           |
| --------------------- | ---------------- | --------- | ------------- | --------------------------------------- |
| `treatment_id`        | BIGINT           | PK        | Sí            | Identificador del tratamiento.          |
| `visit_id`            | BIGINT           | FK        | Sí            | Referencia a `medical_visit(visit_id)`. |
| `treatment_status_id` | BIGINT           | FK        | Sí            | Estado del tratamiento.                 |
| `description`         | TEXT             | -         | Sí            | Plan general del tratamiento.           |
| `start_date`          | DATE             | -         | Sí            | Fecha inicial de indicación.            |
| `end_date`            | DATE             | -         | No            | Fecha estimada o real de cierre.        |
| `observations`        | TEXT             | -         | No            | Justificación clínica del tratamiento.  |

##### Tabla: `medication`

*Descripción: Vademécum o catálogo de fármacos oftálmicos.*

| **Campo**           | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                |
| ------------------- | ---------------- | --------- | ------------- | -------------------------------------------- |
| `medication_id`     | BIGINT           | PK        | Sí            | Identificador del medicamento.               |
| `name`              | VARCHAR(150)     | UK        | Sí            | Nombre comercial / común.                    |
| `active_ingredient` | VARCHAR(150)     | -         | Sí            | Principio activo (ej. Latanoprost, Timolol). |
| `concentration`     | VARCHAR(100)     | -         | No            | Concentración de la presentación (ej. 0.5%). |
| `presentation`      | VARCHAR(100)     | -         | No            | Presentación (Gotas, Gel, Suspensión).       |

##### Tabla: `treatment_medication`

*Descripción: Medicamentos recetados dentro de un tratamiento (2NF / 4NF).*

| **Campo**       | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**             |
| --------------- | ---------------- | --------- | ------------- | ----------------------------------------- |
| `treatment_id`  | BIGINT           | PK, FK    | Sí            | Referencia a `treatment(treatment_id)`.   |
| `medication_id` | BIGINT           | PK, FK    | Sí            | Referencia a `medication(medication_id)`. |
| `dosage`        | VARCHAR(100)     | -         | Sí            | Dosificación (ej: 1 gota).                |
| `frequency`     | VARCHAR(100)     | -         | Sí            | Posología (ej: Cada 12 horas).            |
| `duration`      | VARCHAR(100)     | -         | No            | Duración del tratamiento (ej: 30 días).   |
| `instructions`  | TEXT             | -         | No            | Indicaciones adicionales al paciente.     |

#### 9. Exámenes Clínicos y Parámetros

##### Tabla: `unit_of_measure`

*Descripción: Unidades físicas de medición.*

| **Campo** | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                        |
| --------- | ---------------- | --------- | ------------- | ---------------------------------------------------- |
| `unit_id` | BIGINT           | PK        | Sí            | Identificador de la unidad.                          |
| `name`    | VARCHAR(100)     | UK        | Sí            | Nombre (Milímetros de mercurio, Micras, Porcentaje). |
| `symbol`  | VARCHAR(20)      | -         | Sí            | Simbología (`mmHg`, `µm`, `%`).                      |

##### Tabla: `exam_type`

*Descripción: Tipos de exámenes especializados (OCT, Campo Visual, Paquimetría).*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                      |
| -------------- | ---------------- | --------- | ------------- | -------------------------------------------------- |
| `exam_type_id` | BIGINT           | PK        | Sí            | Identificador del examen.                          |
| `code`         | VARCHAR(50)      | UK        | Sí            | Código distintivo.                                 |
| `name`         | VARCHAR(150)     | -         | Sí            | Nombre del estudio (OCT Mácula, Campimetría 24-2). |
| `description`  | VARCHAR(250)     | -         | No            | Descripción analítica.                             |
| `active`       | BOOLEAN          | -         | Sí            | Disponibilidad.                                    |

##### Tabla: `exam_parameter`

*Descripción: Definición de variables paramétricas medibles por tipo de examen.*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                         |
| -------------- | ---------------- | --------- | ------------- | ----------------------------------------------------- |
| `parameter_id` | BIGINT           | PK        | Sí            | Identificador de la variable.                         |
| `exam_type_id` | BIGINT           | FK        | Sí            | Referencia a `exam_type(exam_type_id)`.               |
| `unit_id`      | BIGINT           | FK        | No            | Referencia a `unit_of_measure(unit_id)`.              |
| `name`         | VARCHAR(150)     | -         | Sí            | Nombre de la variable (Capa RNFL, VFI, CCT).          |
| `data_type`    | VARCHAR(30)      | -         | Sí            | Tipo esperado (`NUMERIC`, `TEXT`, `BOOLEAN`, `DATE`). |
| `description`  | VARCHAR(500)     | -         | No            | Especificaciones paramétricas.                        |
| `required`     | BOOLEAN          | -         | Sí            | Indica si es obligatorio su diligenciamiento.         |

##### Tabla: `exam_parameter_option`

*Descripción: Opciones predefinidas para parámetros cualitativos o selecciones.*

| **Campo**      | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                |
| -------------- | ---------------- | --------- | ------------- | -------------------------------------------- |
| `option_id`    | BIGINT           | PK        | Sí            | Identificador de la opción.                  |
| `parameter_id` | BIGINT           | FK        | Sí            | Referencia a `exam_parameter(parameter_id)`. |
| `value`        | VARCHAR(150)     | -         | Sí            | Valor de la lista desplegable.               |
| `description`  | VARCHAR(250)     | -         | No            | Aclaraciones del valor.                      |

##### Tabla: `clinical_exam`

*Descripción: Cabecera de ejecución de un examen ordenado e interpretado.*

| **Campo**          | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**            |
| ------------------ | ---------------- | --------- | ------------- | ---------------------------------------- |
| `clinical_exam_id` | BIGINT           | PK        | Sí            | Identificador del examen ejecutado.      |
| `visit_id`         | BIGINT           | FK        | Sí            | Consulta donde fue efectuado.            |
| `exam_type_id`     | BIGINT           | FK        | Sí            | Tipo de prueba especializada.            |
| `professional_id`  | BIGINT           | FK        | Sí            | Médico evaluador/interprete.             |
| `eye_id`           | BIGINT           | FK        | Sí            | Lateralidad examinada (OD/OI/OU).        |
| `exam_date`        | DATETIME         | -         | Sí            | Fecha y hora del procedimiento.          |
| `observations`     | TEXT             | -         | No            | Interpretación o conclusiones generales. |

##### Tabla: `exam_result`

*Descripción: Detalle paramétrico con valores capturados por cada estudio (1NF).*

| **Campo**          | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                   |
| ------------------ | ---------------- | --------- | ------------- | ----------------------------------------------- |
| `clinical_exam_id` | BIGINT           | PK, FK    | Sí            | Referencia a `clinical_exam(clinical_exam_id)`. |
| `parameter_id`     | BIGINT           | PK, FK    | Sí            | Referencia a `exam_parameter(parameter_id)`.    |
| `value_text`       | TEXT             | -         | No            | Valor asignado si es de tipo alfanumérico.      |
| `value_numeric`    | DECIMAL(12,4)    | -         | No            | Valor capturado si la variable es cuantitativa. |
| `value_boolean`    | BOOLEAN          | -         | No            | Valor booleano de la prueba.                    |
| `value_date`       | DATE             | -         | No            | Valor temporal registrado.                      |

#### 10. Módulo Específico Oftalmológico (Glaucoma, PIO y Alertas)

##### Tabla: `intraocular_pressure`

*Descripción: Registro dedicado para el monitoreo de Presión Intraocular (PIO).*

| **Campo**        | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                                |
| ---------------- | ---------------- | --------- | ------------- | ------------------------------------------------------------ |
| `pressure_id`    | BIGINT           | PK        | Sí            | Identificador de la tonometría.                              |
| `visit_id`       | BIGINT           | FK        | Sí            | Referencia a `medical_visit(visit_id)`.                      |
| `eye_id`         | BIGINT           | FK        | Sí            | Referencia a `eye(eye_id)` (`OD` u `OI`).                    |
| `measured_at`    | DATETIME         | -         | Sí            | Marca de tiempo precisa de la toma.                          |
| `pressure_value` | DECIMAL(6,2)     | -         | Sí            | Medición numérica de la presión.                             |
| `unit`           | VARCHAR(20)      | -         | Sí            | Unidad de medida (Default: 'mmHg').                          |
| `method`         | VARCHAR(100)     | -         | No            | Instrumental o método utilizado (Aplanación Goldmann, Aire). |

##### Tabla: `glaucoma_type`

*Descripción: Clasificación médica de glaucomas.*

| **Campo**          | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                                |
| ------------------ | ---------------- | --------- | ------------- | ------------------------------------------------------------ |
| `glaucoma_type_id` | BIGINT           | PK        | Sí            | Identificador del tipo.                                      |
| `name`             | VARCHAR(100)     | UK        | Sí            | Nombre (Glaucoma Ángulo Abierto, Ángulo Cerrado, Congénito). |
| `description`      | VARCHAR(500)     | -         | No            | Manifestaciones clínicas y criterios diagnósticos.           |

##### Tabla: `glaucoma_record`

*Descripción: Expediente específico del paciente diagnosticado con glaucoma.*

| **Campo**            | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                          |
| -------------------- | ---------------- | --------- | ------------- | ------------------------------------------------------ |
| `glaucoma_record_id` | BIGINT           | PK        | Sí            | Identificador del expediente del glaucoma.             |
| `patient_id`         | BIGINT           | FK        | Sí            | Paciente con la patología.                             |
| `eye_id`             | BIGINT           | FK        | Sí            | Ojo afectado (OD/OI/OU).                               |
| `glaucoma_type_id`   | BIGINT           | FK        | Sí            | Clasificación del glaucoma.                            |
| `diagnosis_date`     | DATE             | -         | Sí            | Fecha oficial de confirmación diagnóstica.             |
| `active`             | BOOLEAN          | -         | Sí            | Estado del registro (Default: TRUE).                   |
| `observations`       | TEXT             | -         | No            | Meta de presión objetivo (PIO Target) o estadiamiento. |

##### Tabla: `glaucoma_control`

*Descripción: Ficha de seguimiento periódico del glaucoma por consulta.*

| **Campo**             | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**              |
| --------------------- | ---------------- | --------- | ------------- | ------------------------------------------ |
| `glaucoma_control_id` | BIGINT           | PK        | Sí            | Identificador de la ficha de control.      |
| `glaucoma_record_id`  | BIGINT           | FK        | Sí            | Expediente de origen `glaucoma_record`.    |
| `visit_id`            | BIGINT           | FK        | Sí            | Consulta en la que se efectúa el control.  |
| `control_date`        | DATE             | -         | Sí            | Fecha de la valoración de control.         |
| `observations`        | TEXT             | -         | No            | Evolución de la excavación o campo visual. |

##### Tabla: `alert`

*Descripción: Alertas automatizadas por presiones críticas o requerimientos de seguimiento.*

| **Campo**     | **Tipo de Dato** | **Llave** | **Requerido** | **Descripción / Restricción**                                |
| ------------- | ---------------- | --------- | ------------- | ------------------------------------------------------------ |
| `alert_id`    | BIGINT           | PK        | Sí            | Identificador único de la alerta.                            |
| `patient_id`  | BIGINT           | FK        | Sí            | Referencia a `patient(patient_id)`.                          |
| `created_by`  | BIGINT           | FK        | Sí            | Usuario que desencadena o registra la alerta (`user_account`). |
| `visit_id`    | BIGINT           | FK        | No            | Consulta que originó el aviso.                               |
| `title`       | VARCHAR(100)     | -         | Sí            | Título descriptivo (ej: `PIO ELEVADA`).                      |
| `message`     | TEXT             | -         | Sí            | Mensaje o sugerencia de intervención médica.                 |
| `alert_type`  | VARCHAR(50)      | -         | Sí            | Clasificación de riesgo (`ALERTA`, `CRÍTICA`, `SEGUIMIENTO`). |
| `created_at`  | DATETIME         | -         | Sí            | Marca de tiempo de emisión.                                  |
| `resolved_at` | DATETIME         | -         | No            | Fecha en la que la alerta fue atendida o desactivada.        |

# 40. Producto final esperado

El proyecto deberá entregar:

```
1. Formulación del problema
2. Identificación de entidades
3. Diccionario preliminar de datos
4. Modelo conceptual
5. DER
6. Modelo lógico
7. Evidencia de normalización:
   - 1FN
   - 2FN
   - 3FN
   - BCNF cuando aplique
   - 4FN
8. Modelo físico MySQL
9. Script DDL
10. Script de datos de prueba
11. Banco de 250 ejercicios MySQL
12. Evidencias de ejecución
```



# 42. Pregunta orientadora final

**¿Cómo modelar, normalizar e implementar en MySQL una base de datos relacional para historias clínicas de oftalmología y glaucoma que permita garantizar integridad, reducir redundancia y soportar consultas y procesos SQL de diferentes niveles de complejidad?**

### 1. Diseñar el Modelo Entidad-Relación por Módulos

Divide el sistema en componentes claros para evitar mezclar responsabilidades:

- **Personas y Usuarios:** Separa los datos de la persona (`person`) de sus roles (`patient`, `healthcare_professional`, `user_account`). Así evitas duplicar información si un médico también es paciente.
- **Atención Clínica:** Conecta las citas (`appointment`), la historia clínica (`clinical_history`), las consultas (`medical_visit`), los diagnósticos y los procedimientos.
- **Módulo Oftalmológico:** Crea tablas específicas para la presión intraocular (`intraocular_pressure`), la lateralidad del ojo (`eye`: OD/OI), el control del glaucoma (`glaucoma_record`, `glaucoma_control`) y los exámenes (`clinical_exam`).

### 2. Normalizar hasta 4NF

Aplica las reglas de normalización para eliminar redundancias y evitar errores al insertar, editar o borrar datos:

- **1NF:** Atomiza todos los campos (separa nombres/apellidos y almacena resultados de exámenes en filas independientes, no en listas de texto).
- **2NF:** Asegura que en tablas intermedias con llaves compuestas (como `treatment_medication`), cada atributo dependa de la clave completa.
- **3NF:** Elimina dependencias transitivas (extrae las especialidades a `specialty` y las ciudades a `city`).
- **4NF:** Elimina dependencias multivaluadas independientes (gestiona antecedentes y alergias en tablas separadas ligadas al paciente).

### 3. Garantizar Integridad y Lógica de Negocio

Protege la coherencia de la información médica desde la base de datos:

- **Llaves Foráneas (`FK`):** Usa reglas de restricción (`RESTRICT`) en tablas críticas para impedir que se borre a un paciente que tenga historial.
- **Restricciones Unicas (`UNIQUE`):** Asegura que no existan documentos, licencias médicas ni números de historia clínica duplicados.
- **Triggers y Funciones:** Automatiza la validación de reglas clínicas (ej. evitar fechas incoherentes de tratamiento, calcular edades o registrar auditorías en `audit_log`).

### 4. Soporte para Consultas de Diferente Complejidad

Gracias a los índices en claves primarias (`BIGINT`) y foráneas, la estructura soporta desde operaciones diarias hasta analítica avanzada:

- **Transacciones rápidas (OLTP):** Búsquedas directas de pacientes, citas o consultas por ID.
- **Seguimiento clínico:** Historial de la PIO de un paciente o listado de tratamientos activos.
- **Analítica y Reportes:** Agregaciones complejas (`AVG`, `MAX`, `COUNT`) para calcular la presión intraocular máxima, promedios por ojo o el total de exámenes OCT realizados por período sin degradar el rendimiento.

# Banco de 250 ejercicios MySQL

## Proyecto: Historias clínicas de Oftalmología y Glaucoma

Este banco de ejercicios está organizado en cinco categorías:

1. Consultas SQL.
2. Subconsultas.
3. Procedimientos almacenados.
4. Triggers.
5. Funciones almacenadas.

Cada categoría contiene **50 ejercicios**, para un total de **250 actividades**.

Como referencia, se asume que la base de datos contiene entidades similares a:

```
patients
clinical_histories
medical_visits
healthcare_professionals
specialties
diagnoses
visit_diagnoses
glaucoma_records
glaucoma_controls
intraocular_pressures
pachymetry_exams
gonioscopy_exams
oct_exams
visual_field_exams
medications
treatments
procedures
clinical_documents
audit_logs
```

## Base de datos:

```sql
DROP DATABASE IF EXISTS historia_clinica_oftalmologica;
CREATE DATABASE historia_clinica_oftalmologica
  CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE historia_clinica_oftalmologica;
 
SET FOREIGN_KEY_CHECKS = 0;
 
-- ============================ 1. UBICACIÓN ============================
CREATE TABLE clinic (
  clinic_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name      VARCHAR(150) NOT NULL,
  address   VARCHAR(250),
  phone     VARCHAR(30),
  email     VARCHAR(150),
  active    BOOLEAN NOT NULL DEFAULT TRUE
) ENGINE=InnoDB;
 
CREATE TABLE location (
  location_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  clinic_id   BIGINT NOT NULL,
  name        VARCHAR(150) NOT NULL,
  address     VARCHAR(250),
  active      BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT fk_location_clinic FOREIGN KEY (clinic_id) REFERENCES clinic(clinic_id)
) ENGINE=InnoDB;
 
CREATE TABLE room (
  room_id     BIGINT AUTO_INCREMENT PRIMARY KEY,
  location_id BIGINT NOT NULL,
  name        VARCHAR(100) NOT NULL,
  floor       VARCHAR(50),
  active      BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT fk_room_location FOREIGN KEY (location_id) REFERENCES location(location_id)
) ENGINE=InnoDB;
 
CREATE TABLE city (
  city_id    BIGINT AUTO_INCREMENT PRIMARY KEY,
  name       VARCHAR(100) NOT NULL,
  department VARCHAR(100),
  country    VARCHAR(100)
) ENGINE=InnoDB;
 
CREATE TABLE identification_type (
  identification_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(50) NOT NULL,
  description VARCHAR(150)
) ENGINE=InnoDB;
 
-- ============================ 2. PERSONAS =============================
CREATE TABLE person (
  person_id               BIGINT AUTO_INCREMENT PRIMARY KEY,
  identification_type_id  BIGINT NOT NULL,
  identification_number   VARCHAR(30) NOT NULL,
  first_name              VARCHAR(100) NOT NULL,
  middle_name             VARCHAR(100),
  last_name               VARCHAR(100) NOT NULL,
  second_last_name        VARCHAR(100),
  birth_date              DATE,
  gender                  VARCHAR(30),
  phone                   VARCHAR(30),
  email                   VARCHAR(150),
  address                 VARCHAR(250),
  city_id                 BIGINT,
  CONSTRAINT uq_person_identification UNIQUE (identification_type_id, identification_number),
  CONSTRAINT fk_person_idtype FOREIGN KEY (identification_type_id) REFERENCES identification_type(identification_type_id),
  CONSTRAINT fk_person_city   FOREIGN KEY (city_id) REFERENCES city(city_id)
) ENGINE=InnoDB;
 
CREATE TABLE patient (
  patient_id     BIGINT AUTO_INCREMENT PRIMARY KEY,
  person_id      BIGINT NOT NULL UNIQUE,
  admission_date DATE,
  active         BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT fk_patient_person FOREIGN KEY (person_id) REFERENCES person(person_id)
) ENGINE=InnoDB;
 
CREATE TABLE healthcare_professional (
  professional_id      BIGINT AUTO_INCREMENT PRIMARY KEY,
  person_id            BIGINT NOT NULL UNIQUE,
  professional_license VARCHAR(50),
  active               BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT fk_prof_person FOREIGN KEY (person_id) REFERENCES person(person_id)
) ENGINE=InnoDB;
 
CREATE TABLE specialty (
  specialty_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name         VARCHAR(100) NOT NULL,
  description  VARCHAR(250),
  active       BOOLEAN NOT NULL DEFAULT TRUE
) ENGINE=InnoDB;
 
CREATE TABLE professional_specialty (
  professional_id BIGINT NOT NULL,
  specialty_id    BIGINT NOT NULL,
  PRIMARY KEY (professional_id, specialty_id),
  CONSTRAINT fk_ps_prof FOREIGN KEY (professional_id) REFERENCES healthcare_professional(professional_id),
  CONSTRAINT fk_ps_spec FOREIGN KEY (specialty_id) REFERENCES specialty(specialty_id)
) ENGINE=InnoDB;
 
-- ============================ 3. SEGURIDAD ============================
CREATE TABLE user_account (
  user_id       BIGINT AUTO_INCREMENT PRIMARY KEY,
  person_id     BIGINT NOT NULL UNIQUE,
  username      VARCHAR(100) NOT NULL UNIQUE,
  password_hash VARCHAR(255) NOT NULL,
  active        BOOLEAN NOT NULL DEFAULT TRUE,
  created_at    DATETIME DEFAULT CURRENT_TIMESTAMP,
  last_login    DATETIME,
  CONSTRAINT fk_user_person FOREIGN KEY (person_id) REFERENCES person(person_id)
) ENGINE=InnoDB;
 
CREATE TABLE role (
  role_id     BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(100) NOT NULL UNIQUE,
  description VARCHAR(250),
  active      BOOLEAN NOT NULL DEFAULT TRUE
) ENGINE=InnoDB;
 
CREATE TABLE permission (
  permission_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name          VARCHAR(100) NOT NULL UNIQUE,
  description   VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE user_role (
  user_id BIGINT NOT NULL,
  role_id BIGINT NOT NULL,
  PRIMARY KEY (user_id, role_id),
  CONSTRAINT fk_ur_user FOREIGN KEY (user_id) REFERENCES user_account(user_id),
  CONSTRAINT fk_ur_role FOREIGN KEY (role_id) REFERENCES role(role_id)
) ENGINE=InnoDB;
 
CREATE TABLE role_permission (
  role_id       BIGINT NOT NULL,
  permission_id BIGINT NOT NULL,
  PRIMARY KEY (role_id, permission_id),
  CONSTRAINT fk_rp_role FOREIGN KEY (role_id) REFERENCES role(role_id),
  CONSTRAINT fk_rp_perm FOREIGN KEY (permission_id) REFERENCES permission(permission_id)
) ENGINE=InnoDB;
 
-- ========================= 4. AGENDA Y CITAS ==========================
CREATE TABLE professional_schedule (
  schedule_id     BIGINT AUTO_INCREMENT PRIMARY KEY,
  professional_id BIGINT NOT NULL,
  room_id         BIGINT NOT NULL,
  day_of_week     SMALLINT NOT NULL,
  start_time      TIME NOT NULL,
  end_time        TIME NOT NULL,
  active          BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT ck_sched_day  CHECK (day_of_week BETWEEN 1 AND 7),
  CONSTRAINT ck_sched_time CHECK (end_time > start_time),
  CONSTRAINT fk_sched_prof FOREIGN KEY (professional_id) REFERENCES healthcare_professional(professional_id),
  CONSTRAINT fk_sched_room FOREIGN KEY (room_id) REFERENCES room(room_id)
) ENGINE=InnoDB;
 
CREATE TABLE schedule_exception (
  exception_id   BIGINT AUTO_INCREMENT PRIMARY KEY,
  schedule_id    BIGINT NOT NULL,
  exception_date DATE NOT NULL,
  reason         VARCHAR(250),
  available      BOOLEAN NOT NULL DEFAULT FALSE,
  CONSTRAINT fk_exc_sched FOREIGN KEY (schedule_id) REFERENCES professional_schedule(schedule_id)
) ENGINE=InnoDB;
 
CREATE TABLE appointment_status (
  appointment_status_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(80) NOT NULL UNIQUE,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE appointment_type (
  appointment_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name             VARCHAR(100) NOT NULL,
  description      VARCHAR(250),
  duration_minutes INT
) ENGINE=InnoDB;
 
CREATE TABLE appointment_reason (
  appointment_reason_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(150) NOT NULL,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE appointment (
  appointment_id        BIGINT AUTO_INCREMENT PRIMARY KEY,
  patient_id            BIGINT NOT NULL,
  professional_id       BIGINT NOT NULL,
  room_id               BIGINT NOT NULL,
  appointment_type_id   BIGINT NOT NULL,
  appointment_status_id BIGINT NOT NULL,
  appointment_reason_id BIGINT NOT NULL,
  created_by            BIGINT NOT NULL,
  scheduled_start       DATETIME NOT NULL,
  scheduled_end         DATETIME NOT NULL,
  notes                 TEXT,
  created_at            DATETIME DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT ck_appt_time CHECK (scheduled_end > scheduled_start),
  CONSTRAINT fk_appt_patient FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
  CONSTRAINT fk_appt_prof    FOREIGN KEY (professional_id) REFERENCES healthcare_professional(professional_id),
  CONSTRAINT fk_appt_room    FOREIGN KEY (room_id) REFERENCES room(room_id),
  CONSTRAINT fk_appt_type    FOREIGN KEY (appointment_type_id) REFERENCES appointment_type(appointment_type_id),
  CONSTRAINT fk_appt_status  FOREIGN KEY (appointment_status_id) REFERENCES appointment_status(appointment_status_id),
  CONSTRAINT fk_appt_reason  FOREIGN KEY (appointment_reason_id) REFERENCES appointment_reason(appointment_reason_id),
  CONSTRAINT fk_appt_user    FOREIGN KEY (created_by) REFERENCES user_account(user_id),
  INDEX idx_appt_prof_start (professional_id, scheduled_start),
  INDEX idx_appt_patient (patient_id, scheduled_start)
) ENGINE=InnoDB;
 
CREATE TABLE appointment_status_history (
  status_history_id     BIGINT AUTO_INCREMENT PRIMARY KEY,
  appointment_id        BIGINT NOT NULL,
  appointment_status_id BIGINT NOT NULL,
  changed_by            BIGINT NOT NULL,
  changed_at            DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  comments              VARCHAR(500),
  CONSTRAINT fk_ash_appt   FOREIGN KEY (appointment_id) REFERENCES appointment(appointment_id),
  CONSTRAINT fk_ash_status FOREIGN KEY (appointment_status_id) REFERENCES appointment_status(appointment_status_id),
  CONSTRAINT fk_ash_user   FOREIGN KEY (changed_by) REFERENCES user_account(user_id)
) ENGINE=InnoDB;
 
CREATE TABLE visit_type (
  visit_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(100) NOT NULL,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
-- ======================== 5. HISTORIA CLÍNICA =========================
CREATE TABLE clinical_history (
  clinical_history_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  patient_id     BIGINT NOT NULL UNIQUE,
  history_number VARCHAR(50) UNIQUE,
  created_at     DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at     DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  CONSTRAINT fk_ch_patient FOREIGN KEY (patient_id) REFERENCES patient(patient_id)
) ENGINE=InnoDB;
 
CREATE TABLE medical_visit (
  visit_id            BIGINT AUTO_INCREMENT PRIMARY KEY,
  clinical_history_id BIGINT NOT NULL,
  appointment_id      BIGINT UNIQUE,
  professional_id     BIGINT NOT NULL,
  visit_type_id       BIGINT NOT NULL,
  visit_date          DATETIME DEFAULT CURRENT_TIMESTAMP,
  reason              TEXT,
  observations        TEXT,
  CONSTRAINT fk_mv_history FOREIGN KEY (clinical_history_id) REFERENCES clinical_history(clinical_history_id),
  CONSTRAINT fk_mv_appt    FOREIGN KEY (appointment_id) REFERENCES appointment(appointment_id),
  CONSTRAINT fk_mv_prof    FOREIGN KEY (professional_id) REFERENCES healthcare_professional(professional_id),
  CONSTRAINT fk_mv_type    FOREIGN KEY (visit_type_id) REFERENCES visit_type(visit_type_id),
  INDEX idx_mv_history_date (clinical_history_id, visit_date)
) ENGINE=InnoDB;
 
CREATE TABLE background_type (
  background_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(100) NOT NULL,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE patient_background (
  patient_background_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  patient_id         BIGINT NOT NULL,
  background_type_id BIGINT NOT NULL,
  description        TEXT,
  start_date         DATE,
  end_date           DATE,
  active             BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT fk_pb_patient FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
  CONSTRAINT fk_pb_type    FOREIGN KEY (background_type_id) REFERENCES background_type(background_type_id)
) ENGINE=InnoDB;
 
CREATE TABLE allergy (
  allergy_id  BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(150) NOT NULL,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE patient_allergy (
  patient_id   BIGINT NOT NULL,
  allergy_id   BIGINT NOT NULL,
  reaction     VARCHAR(250),
  severity     VARCHAR(50),
  observations TEXT,
  PRIMARY KEY (patient_id, allergy_id),
  CONSTRAINT fk_pa_patient FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
  CONSTRAINT fk_pa_allergy FOREIGN KEY (allergy_id) REFERENCES allergy(allergy_id)
) ENGINE=InnoDB;
 
-- ================= 6. DIAGNÓSTICO Y TRATAMIENTO ======================
CREATE TABLE diagnosis (
  diagnosis_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  code         VARCHAR(30) NOT NULL UNIQUE,
  name         VARCHAR(200) NOT NULL,
  description  VARCHAR(500),
  active       BOOLEAN NOT NULL DEFAULT TRUE
) ENGINE=InnoDB;
 
CREATE TABLE visit_diagnosis (
  visit_id       BIGINT NOT NULL,
  diagnosis_id   BIGINT NOT NULL,
  diagnosis_type VARCHAR(50),
  observations   TEXT,
  PRIMARY KEY (visit_id, diagnosis_id),
  CONSTRAINT fk_vd_visit FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id),
  CONSTRAINT fk_vd_diag  FOREIGN KEY (diagnosis_id) REFERENCES diagnosis(diagnosis_id)
) ENGINE=InnoDB;
 
CREATE TABLE treatment_status (
  treatment_status_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(80) NOT NULL UNIQUE,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE treatment (
  treatment_id        BIGINT AUTO_INCREMENT PRIMARY KEY,
  visit_id            BIGINT NOT NULL,
  treatment_status_id BIGINT NOT NULL,
  description         TEXT,
  start_date          DATE,
  end_date            DATE,
  observations        TEXT,
  CONSTRAINT fk_tr_visit  FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id),
  CONSTRAINT fk_tr_status FOREIGN KEY (treatment_status_id) REFERENCES treatment_status(treatment_status_id)
) ENGINE=InnoDB;
 
CREATE TABLE medication (
  medication_id     BIGINT AUTO_INCREMENT PRIMARY KEY,
  name              VARCHAR(150) NOT NULL,
  active_ingredient VARCHAR(200),
  concentration     VARCHAR(100),
  presentation      VARCHAR(100)
) ENGINE=InnoDB;
 
CREATE TABLE treatment_medication (
  treatment_id  BIGINT NOT NULL,
  medication_id BIGINT NOT NULL,
  dosage        VARCHAR(100),
  frequency     VARCHAR(100),
  duration      VARCHAR(100),
  instructions  TEXT,
  PRIMARY KEY (treatment_id, medication_id),
  CONSTRAINT fk_tm_treatment  FOREIGN KEY (treatment_id) REFERENCES treatment(treatment_id),
  CONSTRAINT fk_tm_medication FOREIGN KEY (medication_id) REFERENCES medication(medication_id)
) ENGINE=InnoDB;
 
CREATE TABLE medical_procedure (
  procedure_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name         VARCHAR(150) NOT NULL,
  description  VARCHAR(500),
  active       BOOLEAN NOT NULL DEFAULT TRUE
) ENGINE=InnoDB;
 
-- ============================ 7. EXÁMENES =============================
CREATE TABLE eye (
  eye_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  code   VARCHAR(20) NOT NULL UNIQUE,
  name   VARCHAR(50) NOT NULL
) ENGINE=InnoDB;
 
CREATE TABLE visit_procedure (
  visit_procedure_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  visit_id           BIGINT NOT NULL,
  procedure_id       BIGINT NOT NULL,
  professional_id    BIGINT NOT NULL,
  eye_id             BIGINT,
  performed_at       DATETIME,
  observations       TEXT,
  CONSTRAINT fk_vp_visit FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id),
  CONSTRAINT fk_vp_proc  FOREIGN KEY (procedure_id) REFERENCES medical_procedure(procedure_id),
  CONSTRAINT fk_vp_prof  FOREIGN KEY (professional_id) REFERENCES healthcare_professional(professional_id),
  CONSTRAINT fk_vp_eye   FOREIGN KEY (eye_id) REFERENCES eye(eye_id)
) ENGINE=InnoDB;
 
CREATE TABLE exam_type (
  exam_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name         VARCHAR(150) NOT NULL,
  description  VARCHAR(500),
  active       BOOLEAN NOT NULL DEFAULT TRUE
) ENGINE=InnoDB;
 
CREATE TABLE unit_of_measure (
  unit_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name    VARCHAR(100) NOT NULL,
  symbol  VARCHAR(20)
) ENGINE=InnoDB;
 
CREATE TABLE exam_parameter (
  parameter_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  exam_type_id BIGINT NOT NULL,
  unit_id      BIGINT,
  name         VARCHAR(150) NOT NULL,
  data_type    VARCHAR(30),
  description  VARCHAR(500),
  required     BOOLEAN NOT NULL DEFAULT FALSE,
  CONSTRAINT fk_ep_exam FOREIGN KEY (exam_type_id) REFERENCES exam_type(exam_type_id),
  CONSTRAINT fk_ep_unit FOREIGN KEY (unit_id) REFERENCES unit_of_measure(unit_id)
) ENGINE=InnoDB;
 
CREATE TABLE exam_parameter_option (
  option_id    BIGINT AUTO_INCREMENT PRIMARY KEY,
  parameter_id BIGINT NOT NULL,
  value        VARCHAR(150) NOT NULL,
  description  VARCHAR(250),
  CONSTRAINT fk_epo_param FOREIGN KEY (parameter_id) REFERENCES exam_parameter(parameter_id)
) ENGINE=InnoDB;
 
CREATE TABLE clinical_exam (
  clinical_exam_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  visit_id         BIGINT NOT NULL,
  exam_type_id     BIGINT NOT NULL,
  professional_id  BIGINT NOT NULL,
  eye_id           BIGINT,
  exam_date        DATETIME,
  observations     TEXT,
  CONSTRAINT fk_ce_visit FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id),
  CONSTRAINT fk_ce_type  FOREIGN KEY (exam_type_id) REFERENCES exam_type(exam_type_id),
  CONSTRAINT fk_ce_prof  FOREIGN KEY (professional_id) REFERENCES healthcare_professional(professional_id),
  CONSTRAINT fk_ce_eye   FOREIGN KEY (eye_id) REFERENCES eye(eye_id)
) ENGINE=InnoDB;
 
CREATE TABLE exam_result (
  clinical_exam_id BIGINT NOT NULL,
  parameter_id     BIGINT NOT NULL,
  value_text       TEXT,
  value_numeric    DECIMAL(12,4),
  value_boolean    BOOLEAN,
  value_date       DATE,
  PRIMARY KEY (clinical_exam_id, parameter_id),
  CONSTRAINT fk_er_exam  FOREIGN KEY (clinical_exam_id) REFERENCES clinical_exam(clinical_exam_id),
  CONSTRAINT fk_er_param FOREIGN KEY (parameter_id) REFERENCES exam_parameter(parameter_id)
) ENGINE=InnoDB;
 
-- ======================= 8. GLAUCOMA Y PRESIÓN ========================
CREATE TABLE glaucoma_type (
  glaucoma_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(100) NOT NULL,
  description VARCHAR(500)
) ENGINE=InnoDB;
 
CREATE TABLE glaucoma_record (
  glaucoma_record_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  patient_id         BIGINT NOT NULL,
  eye_id             BIGINT NOT NULL,
  glaucoma_type_id   BIGINT NOT NULL,
  diagnosis_date     DATE,
  observations       TEXT,
  active             BOOLEAN NOT NULL DEFAULT TRUE,
  CONSTRAINT fk_gr_patient FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
  CONSTRAINT fk_gr_eye     FOREIGN KEY (eye_id) REFERENCES eye(eye_id),
  CONSTRAINT fk_gr_type    FOREIGN KEY (glaucoma_type_id) REFERENCES glaucoma_type(glaucoma_type_id)
) ENGINE=InnoDB;
 
CREATE TABLE glaucoma_control (
  glaucoma_control_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  glaucoma_record_id  BIGINT NOT NULL,
  visit_id            BIGINT NOT NULL,
  control_date        DATE,
  observations        TEXT,
  CONSTRAINT fk_gc_record FOREIGN KEY (glaucoma_record_id) REFERENCES glaucoma_record(glaucoma_record_id),
  CONSTRAINT fk_gc_visit  FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id)
) ENGINE=InnoDB;
 
CREATE TABLE intraocular_pressure (
  pressure_id    BIGINT AUTO_INCREMENT PRIMARY KEY,
  visit_id       BIGINT NOT NULL,
  eye_id         BIGINT NOT NULL,
  measured_at    DATETIME,
  pressure_value DECIMAL(6,2),
  unit           VARCHAR(20) DEFAULT 'mmHg',
  method         VARCHAR(100),
  CONSTRAINT ck_iop_value CHECK (pressure_value IS NULL OR pressure_value >= 0),
  CONSTRAINT fk_iop_visit FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id),
  CONSTRAINT fk_iop_eye   FOREIGN KEY (eye_id) REFERENCES eye(eye_id)
) ENGINE=InnoDB;
 
-- ==================== 9. DOCUMENTOS Y AUDITORÍA =======================
CREATE TABLE document_type (
  document_type_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name        VARCHAR(100) NOT NULL,
  description VARCHAR(250)
) ENGINE=InnoDB;
 
CREATE TABLE clinical_document (
  document_id      BIGINT AUTO_INCREMENT PRIMARY KEY,
  visit_id         BIGINT NOT NULL,
  document_type_id BIGINT NOT NULL,
  uploaded_by      BIGINT NOT NULL,
  deleted_by       BIGINT,
  file_name        VARCHAR(255),
  file_path        VARCHAR(500),
  mime_type        VARCHAR(100),
  uploaded_at      DATETIME DEFAULT CURRENT_TIMESTAMP,
  deleted_at       DATETIME,
  CONSTRAINT fk_cd_visit    FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id),
  CONSTRAINT fk_cd_type     FOREIGN KEY (document_type_id) REFERENCES document_type(document_type_id),
  CONSTRAINT fk_cd_uploader FOREIGN KEY (uploaded_by) REFERENCES user_account(user_id),
  CONSTRAINT fk_cd_deleter  FOREIGN KEY (deleted_by) REFERENCES user_account(user_id)
) ENGINE=InnoDB;
 
CREATE TABLE audit_log (
  audit_log_id BIGINT AUTO_INCREMENT PRIMARY KEY,
  user_id      BIGINT NOT NULL,
  action       VARCHAR(100),
  table_name   VARCHAR(100),
  record_id    BIGINT,
  old_values   TEXT,
  new_values   TEXT,
  created_at   DATETIME DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_al_user FOREIGN KEY (user_id) REFERENCES user_account(user_id),
  INDEX idx_audit_table_record (table_name, record_id)
) ENGINE=InnoDB;
 
CREATE TABLE alert (
  alert_id    BIGINT AUTO_INCREMENT PRIMARY KEY,
  patient_id  BIGINT NOT NULL,
  created_by  BIGINT NOT NULL,
  visit_id    BIGINT,
  title       VARCHAR(150),
  message     TEXT,
  alert_type  VARCHAR(50),
  created_at  DATETIME DEFAULT CURRENT_TIMESTAMP,
  resolved_at DATETIME,
  CONSTRAINT fk_alert_patient FOREIGN KEY (patient_id) REFERENCES patient(patient_id),
  CONSTRAINT fk_alert_user    FOREIGN KEY (created_by) REFERENCES user_account(user_id),
  CONSTRAINT fk_alert_visit   FOREIGN KEY (visit_id) REFERENCES medical_visit(visit_id)
) ENGINE=InnoDB;
 
SET FOREIGN_KEY_CHECKS = 1;
```



## Insertacion de datos:

```sql
USE historia_clinica_oftalmologica;

SET FOREIGN_KEY_CHECKS = 0;

-- ============================================================
-- 1. CLÍNICA
-- ============================================================

INSERT INTO clinic
(clinic_id, name, address, phone, email, active)
VALUES
(1, 'Clínica Oftalmológica Visión Clara', 'Calle 100 # 15-20, Bogotá', '6012345678', 'contacto@visionclara.co', TRUE);

-- ============================================================
-- 2. CIUDADES
-- ============================================================

INSERT INTO city
(city_id, name, department, country)
VALUES
(1, 'Bogotá', 'Cundinamarca', 'Colombia'),
(2, 'Bucaramanga', 'Santander', 'Colombia'),
(3, 'Floridablanca', 'Santander', 'Colombia'),
(4, 'Girón', 'Santander', 'Colombia'),
(5, 'Medellín', 'Antioquia', 'Colombia');

-- ============================================================
-- 3. TIPOS DE IDENTIFICACIÓN
-- ============================================================

INSERT INTO identification_type
(identification_type_id, name, description)
VALUES
(1, 'CC', 'Cédula de ciudadanía'),
(2, 'TI', 'Tarjeta de identidad');

-- ============================================================
-- 4. UBICACIONES
-- ============================================================

INSERT INTO location
(location_id, clinic_id, name, address, active)
VALUES
(1, 1, 'Sede Principal', 'Calle 100 # 15-20, Bogotá', TRUE),
(2, 1, 'Sede Diagnóstico', 'Carrera 15 # 90-10, Bogotá', TRUE);

-- ============================================================
-- 5. CONSULTORIOS
-- ============================================================

INSERT INTO room
(room_id, location_id, name, floor, active)
VALUES
(1, 1, 'Consultorio 101', 'Piso 1', TRUE),
(2, 1, 'Consultorio 102', 'Piso 1', TRUE),
(3, 1, 'Consultorio 201', 'Piso 2', TRUE),
(4, 2, 'Sala de Diagnóstico 1', 'Piso 1', TRUE);

-- ============================================================
-- 6. PERSONAS
-- ============================================================

INSERT INTO person
(person_id, identification_type_id, identification_number, first_name,
 middle_name, last_name, second_last_name, birth_date, gender,
 phone, email, address, city_id)
VALUES
(1, 1, '79111222', 'Ricardo', 'Alonso', 'Beltrán', 'Ospina',
 '1975-04-12', 'Masculino', '3101112233',
 'rbeltran@visionclara.co', 'Calle 80 # 20-11', 1),

(2, 1, '52333444', 'Claudia', 'Marcela', 'Duarte', 'Lozano',
 '1980-09-30', 'Femenino', '3102223344',
 'cduarte@visionclara.co', 'Carrera 15 # 90-05', 1),

(3, 1, '80555666', 'Felipe', 'Esteban', 'Quintero', 'Mejía',
 '1978-01-25', 'Masculino', '3103334455',
 'fquintero@visionclara.co', 'Calle 53 # 10-30', 1),

(4, 1, '1019777888', 'Natalia', 'Andrea', 'Pardo', 'Ríos',
 '1989-06-18', 'Femenino', '3104445566',
 'npardo@visionclara.co', 'Carrera 30 # 45-12', 1),

(5, 1, '1098765432', 'Carlos', 'Andrés', 'Gómez', 'Ramírez',
 '1965-02-10', 'Masculino', '3005556677',
 'cgomez@gmail.com', 'Calle 45 # 20-10', 2),

(6, 1, '63345678', 'María', 'Fernanda', 'Rodríguez', 'Sánchez',
 '1970-07-22', 'Femenino', '3016667788',
 'mrodriguez@gmail.com', 'Carrera 27 # 35-15', 2),

(7, 1, '1098123456', 'Juan', 'David', 'Martínez', 'Torres',
 '1995-11-05', 'Masculino', '3027778899',
 'jmartinez@gmail.com', 'Calle 60 # 12-25', 3),

(8, 1, '63456789', 'Laura', 'Sofía', 'Hernández', 'Vargas',
 '1988-03-14', 'Femenino', '3038889900',
 'lhernandez@gmail.com', 'Carrera 8 # 20-18', 4),

(9, 1, '1001234567', 'Andrés', 'Felipe', 'Moreno', 'Castro',
 '2002-09-17', 'Masculino', '3041112233',
 'amoreno@gmail.com', 'Calle 10 # 8-20', 5),

(10, 1, '1002345678', 'Paula', 'Andrea', 'Rojas', 'Mendoza',
 '2001-05-21', 'Femenino', '3052223344',
 'projas@gmail.com', 'Carrera 12 # 30-40', 1),

(11, 1, '1003456789', 'Diego', 'Alejandro', 'Suárez', 'López',
 '1999-12-03', 'Masculino', '3063334455',
 'dsuarez@gmail.com', 'Calle 25 # 15-30', 2),

(12, 1, '1004567890', 'Valentina', 'Isabel', 'Mora', 'Gutiérrez',
 '2003-08-29', 'Femenino', '3074445566',
 'vmora@gmail.com', 'Carrera 20 # 40-15', 3);

-- ============================================================
-- 7. PACIENTES
-- ============================================================

INSERT INTO patient
(patient_id, person_id, admission_date, active)
VALUES
(1, 5, '2026-01-10', TRUE),
(2, 6, '2026-01-15', TRUE),
(3, 7, '2026-02-03', TRUE),
(4, 8, '2026-02-10', TRUE),
(5, 9, '2026-03-01', TRUE),
(6, 10, '2026-03-12', TRUE),
(7, 11, '2026-04-05', TRUE),
(8, 12, '2026-04-18', TRUE);

-- ============================================================
-- 8. PROFESIONALES
-- ============================================================

INSERT INTO healthcare_professional
(professional_id, person_id, professional_license, active)
VALUES
(1, 1, 'RM-458721', TRUE),
(2, 2, 'RM-563214', TRUE),
(3, 3, 'RM-674321', TRUE),
(4, 4, 'RM-785432', TRUE);

-- ============================================================
-- 9. ESPECIALIDADES
-- ============================================================

INSERT INTO specialty
(specialty_id, name, description, active)
VALUES
(1, 'Oftalmología', 'Atención integral de enfermedades oculares', TRUE),
(2, 'Glaucoma', 'Diagnóstico y tratamiento del glaucoma', TRUE),
(3, 'Retina', 'Diagnóstico y tratamiento de enfermedades de retina', TRUE),
(4, 'Córnea', 'Diagnóstico y tratamiento de enfermedades de córnea', TRUE);

-- ============================================================
-- 10. PROFESIONAL - ESPECIALIDAD
-- ============================================================

INSERT INTO professional_specialty
(professional_id, specialty_id)
VALUES
(1, 1),
(1, 2),
(2, 1),
(2, 3),
(3, 1),
(3, 4),
(4, 1),
(4, 2);

-- ============================================================
-- 11. ROLES
-- ============================================================

INSERT INTO role
(role_id, name, description, active)
VALUES
(1, 'Administrador', 'Administrador general del sistema', TRUE),
(2, 'Oftalmólogo', 'Profesional médico oftalmólogo', TRUE),
(3, 'Recepcionista', 'Personal encargado de agenda y atención', TRUE);

-- ============================================================
-- 12. PERMISOS
-- ============================================================

INSERT INTO permission
(permission_id, name, description)
VALUES
(1, 'GESTIONAR_USUARIOS', 'Crear y administrar usuarios'),
(2, 'GESTIONAR_PACIENTES', 'Gestionar información de pacientes'),
(3, 'GESTIONAR_CITAS', 'Crear y administrar citas'),
(4, 'GESTIONAR_HISTORIAS', 'Gestionar historias clínicas'),
(5, 'GESTIONAR_EXAMENES', 'Gestionar exámenes oftalmológicos'),
(6, 'VER_REPORTES', 'Consultar reportes del sistema');

-- ============================================================
-- 13. CUENTAS DE USUARIO
-- ============================================================

INSERT INTO user_account
(user_id, person_id, username, password_hash, active)
VALUES
(1, 1, 'rbeltran', '$2b$10$DemoHashAdministrador123456789', TRUE),
(2, 2, 'cduarte', '$2b$10$DemoHashOftalmologo123456789', TRUE),
(3, 3, 'fquintero', '$2b$10$DemoHashOftalmologo223456789', TRUE),
(4, 4, 'npardo', '$2b$10$DemoHashRecepcion123456789', TRUE);

-- ============================================================
-- 14. USUARIOS - ROLES
-- ============================================================

INSERT INTO user_role
(user_id, role_id)
VALUES
(1, 1),
(2, 2),
(3, 2),
(4, 3);

-- ============================================================
-- 15. ROLES - PERMISOS
-- ============================================================

INSERT INTO role_permission
(role_id, permission_id)
VALUES
(1, 1),
(1, 2),
(1, 3),
(1, 4),
(1, 5),
(1, 6),
(2, 2),
(2, 4),
(2, 5),
(2, 6),
(3, 2),
(3, 3);

-- ============================================================
-- 16. HORARIOS
-- ============================================================

INSERT INTO professional_schedule
(schedule_id, professional_id, room_id, day_of_week,
 start_time, end_time, active)
VALUES
(1, 1, 1, 1, '08:00:00', '12:00:00', TRUE),
(2, 1, 1, 3, '14:00:00', '18:00:00', TRUE),
(3, 2, 2, 2, '08:00:00', '12:00:00', TRUE),
(4, 2, 2, 4, '14:00:00', '18:00:00', TRUE),
(5, 3, 3, 1, '08:00:00', '12:00:00', TRUE),
(6, 4, 4, 5, '08:00:00', '16:00:00', TRUE);

-- ============================================================
-- 17. EXCEPCIONES DE HORARIO
-- ============================================================

INSERT INTO schedule_exception
(exception_id, schedule_id, exception_date, reason, available)
VALUES
(1, 1, '2026-06-15', 'Día no laboral', FALSE),
(2, 3, '2026-06-22', 'Capacitación médica', FALSE),
(3, 6, '2026-07-03', 'Mantenimiento de equipos', FALSE);

-- ============================================================
-- 18. ESTADOS DE CITA
-- ============================================================

INSERT INTO appointment_status
(appointment_status_id, name, description)
VALUES
(1, 'Programada', 'Cita programada'),
(2, 'Confirmada', 'Cita confirmada por el paciente'),
(3, 'Atendida', 'Cita atendida'),
(4, 'Cancelada', 'Cita cancelada'),
(5, 'No asistió', 'Paciente no asistió');

-- ============================================================
-- 19. TIPOS DE CITA
-- ============================================================

INSERT INTO appointment_type
(appointment_type_id, name, description, duration_minutes)
VALUES
(1, 'Consulta general', 'Consulta oftalmológica general', 30),
(2, 'Control de glaucoma', 'Control especializado de glaucoma', 45),
(3, 'Control de retina', 'Control especializado de retina', 45),
(4, 'Valoración prequirúrgica', 'Valoración previa a procedimiento quirúrgico', 60);

-- ============================================================
-- 20. MOTIVOS DE CITA
-- ============================================================

INSERT INTO appointment_reason
(appointment_reason_id, name, description)
VALUES
(1, 'Dolor ocular', 'Paciente presenta dolor ocular'),
(2, 'Disminución de visión', 'Paciente reporta disminución de agudeza visual'),
(3, 'Control periódico', 'Control oftalmológico rutinario'),
(4, 'Seguimiento glaucoma', 'Seguimiento de diagnóstico de glaucoma'),
(5, 'Valoración', 'Valoración oftalmológica inicial');

-- ============================================================
-- 21. CITAS
-- ============================================================

INSERT INTO appointment
(appointment_id, patient_id, professional_id, room_id,
 appointment_type_id, appointment_status_id, appointment_reason_id,
 created_by, scheduled_start, scheduled_end, notes)
VALUES
(1, 1, 1, 1, 1, 3, 2, 4, '2026-05-04 08:00:00', '2026-05-04 08:30:00', 'Consulta inicial'),
(2, 2, 2, 2, 2, 3, 4, 4, '2026-05-05 08:00:00', '2026-05-05 08:45:00', 'Control de glaucoma'),
(3, 3, 3, 3, 1, 3, 3, 4, '2026-05-06 08:00:00', '2026-05-06 08:30:00', 'Control general'),
(4, 4, 4, 4, 3, 2, 3, 4, '2026-06-10 08:00:00', '2026-06-10 08:45:00', 'Control de retina'),
(5, 5, 1, 1, 1, 1, 1, 4, '2026-06-15 09:00:00', '2026-06-15 09:30:00', 'Consulta por dolor ocular'),
(6, 6, 2, 2, 2, 2, 4, 4, '2026-06-16 10:00:00', '2026-06-16 10:45:00', 'Seguimiento glaucoma'),
(7, 7, 3, 3, 1, 1, 2, 4, '2026-06-17 11:00:00', '2026-06-17 11:30:00', 'Disminución visual'),
(8, 8, 4, 4, 4, 1, 5, 4, '2026-06-18 14:00:00', '2026-06-18 15:00:00', 'Valoración prequirúrgica');

-- ============================================================
-- 22. HISTORIAL DE ESTADOS DE CITAS
-- ============================================================

INSERT INTO appointment_status_history
(status_history_id, appointment_id, appointment_status_id,
 changed_by, changed_at, comments)
VALUES
(1, 1, 1, 4, '2026-04-25 09:00:00', 'Cita creada'),
(2, 1, 2, 4, '2026-04-28 10:00:00', 'Cita confirmada'),
(3, 1, 3, 4, '2026-05-04 08:35:00', 'Paciente atendido'),
(4, 2, 1, 4, '2026-04-26 11:00:00', 'Cita creada'),
(5, 2, 2, 4, '2026-05-01 09:00:00', 'Cita confirmada'),
(6, 2, 3, 4, '2026-05-05 08:50:00', 'Paciente atendido');

-- ============================================================
-- 23. TIPOS DE VISITA
-- ============================================================

INSERT INTO visit_type
(visit_type_id, name, description)
VALUES
(1, 'Consulta inicial', 'Primera consulta del paciente'),
(2, 'Consulta de control', 'Consulta de seguimiento'),
(3, 'Urgencia oftalmológica', 'Atención por urgencia ocular'),
(4, 'Postoperatorio', 'Control posterior a procedimiento');

-- ============================================================
-- 24. HISTORIAS CLÍNICAS
-- ============================================================

INSERT INTO clinical_history
(clinical_history_id, patient_id, history_number)
VALUES
(1, 1, 'HC-000001'),
(2, 2, 'HC-000002'),
(3, 3, 'HC-000003'),
(4, 4, 'HC-000004'),
(5, 5, 'HC-000005'),
(6, 6, 'HC-000006'),
(7, 7, 'HC-000007'),
(8, 8, 'HC-000008');

-- ============================================================
-- 25. VISITAS MÉDICAS
-- ============================================================

INSERT INTO medical_visit
(visit_id, clinical_history_id, appointment_id, professional_id,
 visit_type_id, visit_date, reason, observations)
VALUES
(1, 1, 1, 1, 1, '2026-05-04 08:05:00',
 'Disminución de visión',
 'Paciente refiere visión borrosa de cerca.'),

(2, 2, 2, 2, 2, '2026-05-05 08:05:00',
 'Seguimiento de glaucoma',
 'Control estable.'),

(3, 3, 3, 3, 2, '2026-05-06 08:05:00',
 'Control oftalmológico',
 'Sin cambios significativos.'),

(4, 4, 4, 4, 2, '2026-06-10 08:05:00',
 'Control de retina',
 'Se recomienda seguimiento.'),

(5, 5, NULL, 1, 3, '2026-05-20 10:00:00',
 'Dolor ocular',
 'Paciente presenta dolor ocular leve.'),

(6, 6, NULL, 2, 2, '2026-06-01 09:00:00',
 'Seguimiento glaucoma',
 'Presión intraocular controlada.'),

(7, 7, NULL, 3, 1, '2026-06-03 11:00:00',
 'Disminución visual',
 'Se realiza valoración general.'),

(8, 8, NULL, 4, 4, '2026-06-05 14:00:00',
 'Valoración prequirúrgica',
 'Paciente apta para valoración quirúrgica.');

-- ============================================================
-- 26. TIPOS DE ANTECEDENTES
-- ============================================================

INSERT INTO background_type
(background_type_id, name, description)
VALUES
(1, 'Hipertensión', 'Antecedente de hipertensión arterial'),
(2, 'Diabetes', 'Antecedente de diabetes mellitus'),
(3, 'Cirugía ocular', 'Antecedente de cirugía ocular'),
(4, 'Antecedente familiar', 'Antecedente familiar de enfermedad ocular');

-- ============================================================
-- 27. ANTECEDENTES DE PACIENTES
-- ============================================================

INSERT INTO patient_background
(patient_background_id, patient_id, background_type_id,
 description, start_date, active)
VALUES
(1, 1, 1, 'Hipertensión arterial controlada', '2018-01-01', TRUE),
(2, 2, 2, 'Diabetes mellitus tipo 2', '2019-05-10', TRUE),
(3, 2, 4, 'Madre con glaucoma', '2000-01-01', TRUE),
(4, 4, 3, 'Cirugía de catarata previa', '2023-08-15', TRUE),
(5, 6, 1, 'Hipertensión controlada', '2020-03-01', TRUE);

-- ============================================================
-- 28. ALERGIAS
-- ============================================================

INSERT INTO allergy
(allergy_id, name, description)
VALUES
(1, 'Penicilina', 'Alergia conocida a penicilina'),
(2, 'Ibuprofeno', 'Reacción adversa a ibuprofeno'),
(3, 'Látex', 'Alergia al látex'),
(4, 'Polen', 'Alergia ambiental');

-- ============================================================
-- 29. ALERGIAS DE PACIENTES
-- ============================================================

INSERT INTO patient_allergy
(patient_id, allergy_id, reaction, severity, observations)
VALUES
(1, 1, 'Erupción cutánea', 'Moderada', 'Evitar medicamentos con penicilina'),
(3, 4, 'Estornudos', 'Leve', 'Alergia estacional'),
(5, 2, 'Dolor abdominal', 'Moderada', 'Evitar ibuprofeno'),
(7, 3, 'Irritación cutánea', 'Leve', 'Precaución con material de látex');

-- ============================================================
-- 30. DIAGNÓSTICOS
-- ============================================================

INSERT INTO diagnosis
(diagnosis_id, code, name, description, active)
VALUES
(1, 'H40.1', 'Glaucoma primario de ángulo abierto', 'Glaucoma crónico de ángulo abierto', TRUE),
(2, 'H25.9', 'Catarata no especificada', 'Opacidad del cristalino', TRUE),
(3, 'H52.4', 'Presbicia', 'Alteración de la visión cercana relacionada con la edad', TRUE),
(4, 'H35.3', 'Degeneración macular', 'Alteración degenerativa de la mácula', TRUE),
(5, 'H04.1', 'Síndrome de ojo seco', 'Alteración de la película lagrimal', TRUE),
(6, 'H53.8', 'Otros trastornos visuales', 'Alteración visual no especificada', TRUE);

-- ============================================================
-- 31. DIAGNÓSTICOS POR VISITA
-- ============================================================

INSERT INTO visit_diagnosis
(visit_id, diagnosis_id, diagnosis_type, observations)
VALUES
(1, 3, 'Principal', 'Presbicia relacionada con edad'),
(2, 1, 'Principal', 'Glaucoma en seguimiento'),
(3, 5, 'Principal', 'Síntomas compatibles con ojo seco'),
(4, 4, 'Principal', 'Control de degeneración macular'),
(5, 5, 'Principal', 'Ojo seco asociado a molestias'),
(6, 1, 'Principal', 'Seguimiento de glaucoma'),
(7, 6, 'Principal', 'Alteración visual'),
(8, 2, 'Principal', 'Catarata en valoración');

-- ============================================================
-- 32. ESTADOS DE TRATAMIENTO
-- ============================================================

INSERT INTO treatment_status
(treatment_status_id, name, description)
VALUES
(1, 'Activo', 'Tratamiento actualmente activo'),
(2, 'Finalizado', 'Tratamiento terminado'),
(3, 'Suspendido', 'Tratamiento suspendido');

-- ============================================================
-- 33. TRATAMIENTOS
-- ============================================================

INSERT INTO treatment
(treatment_id, visit_id, treatment_status_id, description,
 start_date, end_date, observations)
VALUES
(1, 2, 1, 'Tratamiento para control de presión intraocular',
 '2026-05-05', NULL, 'Continuar tratamiento actual'),

(2, 3, 1, 'Lubricación ocular',
 '2026-05-06', '2026-06-06', 'Aplicar según indicación'),

(3, 4, 1, 'Seguimiento especializado de retina',
 '2026-06-10', NULL, 'Control periódico'),

(4, 5, 2, 'Lubricación ocular',
 '2026-05-20', '2026-06-20', 'Tratamiento completado'),

(5, 6, 1, 'Control farmacológico de glaucoma',
 '2026-06-01', NULL, 'Continuar medicación'),

(6, 8, 1, 'Manejo de catarata',
 '2026-06-05', NULL, 'Valoración quirúrgica');

-- ============================================================
-- 34. MEDICAMENTOS
-- ============================================================

INSERT INTO medication
(medication_id, name, active_ingredient, concentration, presentation)
VALUES
(1, 'Timolol', 'Timolol maleato', '0.5%', 'Gotas oftálmicas'),
(2, 'Latanoprost', 'Latanoprost', '0.005%', 'Gotas oftálmicas'),
(3, 'Lágrimas artificiales', 'Carboximetilcelulosa', '0.5%', 'Gotas oftálmicas'),
(4, 'Dorzolamida', 'Dorzolamida', '2%', 'Gotas oftálmicas'),
(5, 'Hialuronato de sodio', 'Hialuronato de sodio', '0.18%', 'Gotas oftálmicas');

-- ============================================================
-- 35. MEDICAMENTOS POR TRATAMIENTO
-- ============================================================

INSERT INTO treatment_medication
(treatment_id, medication_id, dosage, frequency, duration, instructions)
VALUES
(1, 1, '1 gota', 'Cada 12 horas', '30 días', 'Aplicar en ojo afectado'),
(1, 2, '1 gota', 'Cada 24 horas', '30 días', 'Aplicar en la noche'),
(2, 3, '1 gota', 'Cada 6 horas', '30 días', 'Aplicar según síntomas'),
(5, 2, '1 gota', 'Cada 24 horas', 'Indefinido', 'Aplicar en la noche'),
(5, 4, '1 gota', 'Cada 8 horas', '30 días', 'Aplicar según indicación'),
(4, 5, '1 gota', 'Cada 8 horas', '30 días', 'Lubricación ocular');

-- ============================================================
-- 36. PROCEDIMIENTOS
-- ============================================================

INSERT INTO medical_procedure
(procedure_id, name, description, active)
VALUES
(1, 'Tonometría', 'Medición de presión intraocular', TRUE),
(2, 'Oftalmoscopia', 'Evaluación del fondo de ojo', TRUE),
(3, 'Campimetría', 'Evaluación del campo visual', TRUE),
(4, 'Gonioscopia', 'Evaluación del ángulo iridocorneal', TRUE),
(5, 'Biometría ocular', 'Medición de parámetros anatómicos del ojo', TRUE);

-- ============================================================
-- 37. OJOS
-- ============================================================

INSERT INTO eye
(eye_id, code, name)
VALUES
(1, 'OD', 'Ojo derecho'),
(2, 'OS', 'Ojo izquierdo'),
(3, 'OU', 'Ambos ojos');

-- ============================================================
-- 38. PROCEDIMIENTOS REALIZADOS
-- ============================================================

INSERT INTO visit_procedure
(visit_procedure_id, visit_id, procedure_id, professional_id,
 eye_id, performed_at, observations)
VALUES
(1, 1, 1, 1, 3, '2026-05-04 08:20:00', 'Presión intraocular medida'),
(2, 2, 1, 2, 3, '2026-05-05 08:20:00', 'Control de presión'),
(3, 2, 3, 2, 3, '2026-05-05 08:35:00', 'Campimetría de control'),
(4, 4, 2, 4, 2, '2026-06-10 08:20:00', 'Evaluación de retina'),
(5, 6, 1, 2, 3, '2026-06-01 09:20:00', 'Tonometría de seguimiento'),
(6, 8, 5, 4, 3, '2026-06-05 14:30:00', 'Biometría ocular');

-- ============================================================
-- 39. TIPOS DE EXAMEN
-- ============================================================

INSERT INTO exam_type
(exam_type_id, name, description, active)
VALUES
(1, 'Agudeza visual', 'Evaluación de agudeza visual', TRUE),
(2, 'Campimetría visual', 'Evaluación del campo visual', TRUE),
(3, 'Paquimetría corneal', 'Medición del espesor corneal', TRUE);

-- ============================================================
-- 40. UNIDADES DE MEDIDA
-- ============================================================

INSERT INTO unit_of_measure
(unit_id, name, symbol)
VALUES
(1, 'Decibelios', 'dB'),
(2, 'Micrómetros', 'um'),
(3, 'Dioptrías', 'D'),
(4, 'Milímetros de mercurio', 'mmHg');

-- ============================================================
-- 41. PARÁMETROS DE EXAMEN
-- ============================================================

INSERT INTO exam_parameter
(parameter_id, exam_type_id, unit_id, name, data_type, description, required)
VALUES
(1, 1, 3, 'Agudeza visual OD', 'TEXT', 'Agudeza visual del ojo derecho', TRUE),
(2, 1, 3, 'Agudeza visual OS', 'TEXT', 'Agudeza visual del ojo izquierdo', TRUE),
(3, 2, 1, 'Sensibilidad media', 'NUMERIC', 'Sensibilidad media del campo visual', FALSE),
(4, 2, 1, 'Desviación media', 'NUMERIC', 'Desviación media del campo visual', FALSE),
(5, 3, 2, 'Espesor corneal OD', 'NUMERIC', 'Paquimetría del ojo derecho', TRUE),
(6, 3, 2, 'Espesor corneal OS', 'NUMERIC', 'Paquimetría del ojo izquierdo', TRUE);

-- ============================================================
-- 42. OPCIONES DE PARÁMETROS
-- ============================================================

INSERT INTO exam_parameter_option
(option_id, parameter_id, value, description)
VALUES
(1, 1, '20/20', 'Agudeza visual normal'),
(2, 1, '20/40', 'Disminución leve'),
(3, 1, '20/60', 'Disminución moderada'),
(4, 2, '20/20', 'Agudeza visual normal'),
(5, 2, '20/40', 'Disminución leve'),
(6, 2, '20/60', 'Disminución moderada');

-- ============================================================
-- 43. EXÁMENES CLÍNICOS
-- ============================================================

INSERT INTO clinical_exam
(clinical_exam_id, visit_id, exam_type_id, professional_id,
 eye_id, exam_date, observations)
VALUES
(1, 1, 1, 1, 3, '2026-05-04 08:15:00', 'Agudeza visual evaluada'),
(2, 2, 2, 2, 3, '2026-05-05 08:25:00', 'Campimetría de seguimiento'),
(3, 3, 1, 3, 3, '2026-05-06 08:15:00', 'Agudeza visual estable'),
(4, 4, 3, 4, 3, '2026-06-10 08:25:00', 'Paquimetría realizada'),
(5, 6, 2, 2, 3, '2026-06-01 09:25:00', 'Campo visual de control'),
(6, 8, 3, 4, 3, '2026-06-05 14:40:00', 'Medición prequirúrgica');

-- ============================================================
-- 44. RESULTADOS DE EXÁMENES
-- ============================================================

INSERT INTO exam_result
(clinical_exam_id, parameter_id, value_text, value_numeric,
 value_boolean, value_date)
VALUES
(1, 1, '20/40', NULL, NULL, NULL),
(1, 2, '20/30', NULL, NULL, NULL),
(2, 3, NULL, 28.5000, NULL, NULL),
(2, 4, NULL, -2.3000, NULL, NULL),
(3, 1, '20/30', NULL, NULL, NULL),
(3, 2, '20/25', NULL, NULL, NULL),
(4, 5, NULL, 545.0000, NULL, NULL),
(4, 6, NULL, 548.0000, NULL, NULL),
(5, 3, NULL, 27.8000, NULL, NULL),
(5, 4, NULL, -1.8000, NULL, NULL),
(6, 5, NULL, 550.0000, NULL, NULL),
(6, 6, NULL, 552.0000, NULL, NULL);

-- ============================================================
-- 45. TIPOS DE GLAUCOMA
-- ============================================================

INSERT INTO glaucoma_type
(glaucoma_type_id, name, description)
VALUES
(1, 'Glaucoma primario de ángulo abierto', 'Glaucoma crónico de ángulo abierto'),
(2, 'Glaucoma de ángulo cerrado', 'Glaucoma asociado al cierre del ángulo'),
(3, 'Glaucoma secundario', 'Glaucoma producido por otra condición');

-- ============================================================
-- 46. REGISTROS DE GLAUCOMA
-- ============================================================

INSERT INTO glaucoma_record
(glaucoma_record_id, patient_id, eye_id, glaucoma_type_id,
 diagnosis_date, observations, active)
VALUES
(1, 2, 1, 1, '2024-05-10', 'Glaucoma controlado', TRUE),
(2, 2, 2, 1, '2024-05-10', 'Glaucoma controlado', TRUE),
(3, 6, 1, 1, '2025-03-15', 'Seguimiento periódico', TRUE),
(4, 6, 2, 1, '2025-03-15', 'Seguimiento periódico', TRUE);

-- ============================================================
-- 47. CONTROLES DE GLAUCOMA
-- ============================================================

INSERT INTO glaucoma_control
(glaucoma_control_id, glaucoma_record_id, visit_id,
 control_date, observations)
VALUES
(1, 1, 2, '2026-05-05', 'Control estable'),
(2, 2, 2, '2026-05-05', 'Control estable'),
(3, 3, 6, '2026-06-01', 'Presión controlada'),
(4, 4, 6, '2026-06-01', 'Presión controlada');

-- ============================================================
-- 48. PRESIÓN INTRAOCULAR
-- ============================================================

INSERT INTO intraocular_pressure
(pressure_id, visit_id, eye_id, measured_at,
 pressure_value, unit, method)
VALUES
(1, 1, 1, '2026-05-04 08:20:00', 16.00, 'mmHg', 'Tonómetro de aplanación'),
(2, 1, 2, '2026-05-04 08:21:00', 17.00, 'mmHg', 'Tonómetro de aplanación'),
(3, 2, 1, '2026-05-05 08:20:00', 14.00, 'mmHg', 'Tonómetro de aplanación'),
(4, 2, 2, '2026-05-05 08:21:00', 15.00, 'mmHg', 'Tonómetro de aplanación'),
(5, 6, 1, '2026-06-01 09:20:00', 13.00, 'mmHg', 'Tonómetro de aplanación'),
(6, 6, 2, '2026-06-01 09:21:00', 14.00, 'mmHg', 'Tonómetro de aplanación');

-- ============================================================
-- 49. TIPOS DE DOCUMENTO
-- ============================================================

INSERT INTO document_type
(document_type_id, name, description)
VALUES
(1, 'Historia clínica', 'Documento de historia clínica'),
(2, 'Resultado de examen', 'Resultado de examen oftalmológico'),
(3, 'Consentimiento informado', 'Documento de consentimiento informado'),
(4, 'Orden médica', 'Orden o fórmula médica');

-- ============================================================
-- 50. DOCUMENTOS CLÍNICOS
-- ============================================================

INSERT INTO clinical_document
(document_id, visit_id, document_type_id, uploaded_by,
 file_name, file_path, mime_type)
VALUES
(1, 1, 1, 2, 'historia_HC000001.pdf',
 '/documentos/historias/historia_HC000001.pdf',
 'application/pdf'),

(2, 2, 2, 2, 'campimetria_HC000002.pdf',
 '/documentos/examenes/campimetria_HC000002.pdf',
 'application/pdf'),

(3, 4, 2, 4, 'paquimetria_HC000004.pdf',
 '/documentos/examenes/paquimetria_HC000004.pdf',
 'application/pdf'),

(4, 8, 3, 4, 'consentimiento_HC000008.pdf',
 '/documentos/consentimientos/consentimiento_HC000008.pdf',
 'application/pdf');

-- ============================================================
-- 51. AUDITORÍA
-- ============================================================

INSERT INTO audit_log
(audit_log_id, user_id, action, table_name, record_id,
 old_values, new_values)
VALUES
(1, 1, 'INSERT', 'patient', 1, NULL, 'Paciente creado'),
(2, 4, 'INSERT', 'appointment', 1, NULL, 'Cita creada'),
(3, 2, 'UPDATE', 'medical_visit', 2, 'Estado pendiente', 'Atendido'),
(4, 2, 'INSERT', 'clinical_exam', 2, NULL, 'Examen registrado'),
(5, 1, 'INSERT', 'user_account', 4, NULL, 'Usuario creado');

-- ============================================================
-- 52. ALERTAS
-- ============================================================

INSERT INTO alert
(alert_id, patient_id, created_by, visit_id,
 title, message, alert_type)
VALUES
(1, 2, 2, 2,
 'Control de glaucoma',
 'Paciente requiere seguimiento periódico de presión intraocular.',
 'CLINICA'),

(2, 6, 2, 6,
 'Seguimiento glaucoma',
 'Verificar presión intraocular en próxima consulta.',
 'CLINICA'),

(3, 4, 4, 4,
 'Control de retina',
 'Programar próxima valoración especializada.',
 'SEGUIMIENTO'),

(4, 8, 4, 8,
 'Valoración quirúrgica',
 'Revisar resultados de estudios prequirúrgicos.',
 'QUIRURGICA');

SET FOREIGN_KEY_CHECKS = 1;

-- ============================================================
-- VERIFICACIÓN
-- ============================================================

SELECT 'clinic' AS tabla, COUNT(*) AS registros FROM clinic
UNION ALL
SELECT 'location', COUNT(*) FROM location
UNION ALL
SELECT 'room', COUNT(*) FROM room
UNION ALL
SELECT 'city', COUNT(*) FROM city
UNION ALL
SELECT 'identification_type', COUNT(*) FROM identification_type
UNION ALL
SELECT 'person', COUNT(*) FROM person
UNION ALL
SELECT 'patient', COUNT(*) FROM patient
UNION ALL
SELECT 'healthcare_professional', COUNT(*) FROM healthcare_professional
UNION ALL
SELECT 'specialty', COUNT(*) FROM specialty
UNION ALL
SELECT 'professional_specialty', COUNT(*) FROM professional_specialty
UNION ALL
SELECT 'user_account', COUNT(*) FROM user_account
UNION ALL
SELECT 'role', COUNT(*) FROM role
UNION ALL
SELECT 'permission', COUNT(*) FROM permission
UNION ALL
SELECT 'user_role', COUNT(*) FROM user_role
UNION ALL
SELECT 'role_permission', COUNT(*) FROM role_permission
UNION ALL
SELECT 'professional_schedule', COUNT(*) FROM professional_schedule
UNION ALL
SELECT 'schedule_exception', COUNT(*) FROM schedule_exception
UNION ALL
SELECT 'appointment_status', COUNT(*) FROM appointment_status
UNION ALL
SELECT 'appointment_type', COUNT(*) FROM appointment_type
UNION ALL
SELECT 'appointment_reason', COUNT(*) FROM appointment_reason
UNION ALL
SELECT 'appointment', COUNT(*) FROM appointment
UNION ALL
SELECT 'appointment_status_history', COUNT(*) FROM appointment_status_history
UNION ALL
SELECT 'visit_type', COUNT(*) FROM visit_type
UNION ALL
SELECT 'clinical_history', COUNT(*) FROM clinical_history
UNION ALL
SELECT 'medical_visit', COUNT(*) FROM medical_visit
UNION ALL
SELECT 'background_type', COUNT(*) FROM background_type
UNION ALL
SELECT 'patient_background', COUNT(*) FROM patient_background
UNION ALL
SELECT 'allergy', COUNT(*) FROM allergy
UNION ALL
SELECT 'patient_allergy', COUNT(*) FROM patient_allergy
UNION ALL
SELECT 'diagnosis', COUNT(*) FROM diagnosis
UNION ALL
SELECT 'visit_diagnosis', COUNT(*) FROM visit_diagnosis
UNION ALL
SELECT 'treatment_status', COUNT(*) FROM treatment_status
UNION ALL
SELECT 'treatment', COUNT(*) FROM treatment
UNION ALL
SELECT 'medication', COUNT(*) FROM medication
UNION ALL
SELECT 'treatment_medication', COUNT(*) FROM treatment_medication
UNION ALL
SELECT 'medical_procedure', COUNT(*) FROM medical_procedure
UNION ALL
SELECT 'eye', COUNT(*) FROM eye
UNION ALL
SELECT 'visit_procedure', COUNT(*) FROM visit_procedure
UNION ALL
SELECT 'exam_type', COUNT(*) FROM exam_type
UNION ALL
SELECT 'unit_of_measure', COUNT(*) FROM unit_of_measure
UNION ALL
SELECT 'exam_parameter', COUNT(*) FROM exam_parameter
UNION ALL
SELECT 'exam_parameter_option', COUNT(*) FROM exam_parameter_option
UNION ALL
SELECT 'clinical_exam', COUNT(*) FROM clinical_exam
UNION ALL
SELECT 'exam_result', COUNT(*) FROM exam_result
UNION ALL
SELECT 'glaucoma_type', COUNT(*) FROM glaucoma_type
UNION ALL
SELECT 'glaucoma_record', COUNT(*) FROM glaucoma_record
UNION ALL
SELECT 'glaucoma_control', COUNT(*) FROM glaucoma_control
UNION ALL
SELECT 'intraocular_pressure', COUNT(*) FROM intraocular_pressure
UNION ALL
SELECT 'document_type', COUNT(*) FROM document_type
UNION ALL
SELECT 'clinical_document', COUNT(*) FROM clinical_document
UNION ALL
SELECT 'audit_log', COUNT(*) FROM audit_log
UNION ALL
SELECT 'alert', COUNT(*) FROM alert;
```



# PARTE I — 50 EJERCICIOS DE CONSULTAS SQL

## Nivel básico

### 1.

Mostrar todos los pacientes registrados en la base de datos.

```sql
SELECT
    pa.patient_id,
    pe.person_id,
    pe.identification_number,
    pe.first_name,
    pe.middle_name,
    pe.last_name,
    pe.second_last_name,
    pe.birth_date,
    pe.gender,
    pe.phone,
    pe.email,
    pe.address,
    pa.admission_date,
    pa.active
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id;
```

![](C:\Users\johan\Downloads\consulra1.1.png)

### 2.

Mostrar únicamente el número de documento, nombres y apellidos de todos los pacientes.

```sql
SELECT
    pe.identification_number AS documento,
    pe.first_name AS nombres,
    pe.middle_name AS segundo_nombre,
    pe.last_name AS apellido,
    pe.second_last_name AS segundo_apellido
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id;
```

![image-20261007120708835](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007120708835.png)

### 3.

Listar todos los profesionales de salud registrados.

```sql
SELECT
    hp.professional_id,
    pe.identification_number,
    pe.first_name,
    pe.middle_name,
    pe.last_name,
    pe.second_last_name,
    hp.professional_license,
    hp.active
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id;
```

![image-20261007120819522](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007120819522.png)

### 4.

Mostrar todos los diagnósticos disponibles en el catálogo.

```sql
SELECT
    diagnosis_id,
    code,
    name,
    description,
    active
FROM diagnosis
ORDER BY name;
```

![image-20261008110021769](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008110021769.png)

### 5.

Consultar todas las historias clínicas registradas.

```sql
SELECT
    ch.clinical_history_id,
    ch.history_number,
    ch.patient_id,
    ch.created_at,
    ch.updated_at
FROM clinical_history ch
ORDER BY ch.clinical_history_id;
```

![image-20261008110054190](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008110054190.png)

### 6.

Mostrar todos los pacientes ordenados alfabéticamente por apellido.

```sql
SELECT
    pa.patient_id,
    pe.identification_number,
    pe.first_name,
    pe.last_name
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id
ORDER BY
    pe.last_name ASC,
    pe.first_name ASC;
```

![image-20261007121056218](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007121056218.png)

### 7.

Mostrar los pacientes ordenados por fecha de nacimiento desde el más joven hasta el de mayor edad.

```sql
SELECT
    pa.patient_id,
    pe.first_name,
    pe.last_name,
    pe.birth_date
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id
WHERE pe.birth_date IS NOT NULL
ORDER BY pe.birth_date DESC;
```

![image-20261007121224395](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007121224395.png)

### 8.

Consultar los pacientes cuyo apellido sea `Gómez`.

```sql
SELECT
    pa.patient_id,
    pe.identification_number,
    pe.first_name,
    pe.last_name
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id
WHERE pe.last_name = 'Gómez';
```

![image-20261007121350727](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007121350727.png)

### 9.

Mostrar los pacientes cuyo número de documento comience por `10`.

```sql
SELECT
    pa.patient_id,
    pe.identification_number,
    pe.first_name,
    pe.last_name
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id
WHERE pe.identification_number LIKE '10%';
```

![image-20261007121443293](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007121443293.png)

### 10.

Consultar los pacientes cuyo correo electrónico pertenezca al dominio `gmail.com`.

```sql
SELECT
    pa.patient_id,
    pe.first_name,
    pe.last_name,
    pe.email
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id
WHERE pe.email LIKE '%@gmail.com';
```

![image-20261007121535312](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007121535312.png)

### 11.

Mostrar los pacientes que no tengan correo electrónico registrado.

```sql
SELECT
    pa.patient_id,
    pe.identification_number,
    pe.first_name,
    pe.last_name
FROM patient pa
INNER JOIN person pe
    ON pe.person_id = pa.person_id
WHERE pe.email IS NULL;
```

![image-20261007122917271](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007122917271.png)

### 12.

Mostrar los profesionales cuya especialidad sea Oftalmología.

```sql
SELECT
    hp.professional_id,
    pe.first_name,
    pe.last_name,
    s.name AS specialty
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
INNER JOIN professional_specialty ps
    ON ps.professional_id = hp.professional_id
INNER JOIN specialty s
    ON s.specialty_id = ps.specialty_id
WHERE s.name = 'Oftalmología';
```

![image-20261007123356217](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261007123356217.png)

### 13.

Consultar todas las consultas médicas realizadas durante el año 2026.

```sql
SELECT
    mv.visit_id,
    mv.visit_date,
    mv.reason,
    mv.observations
FROM medical_visit mv
WHERE mv.visit_date >= '2026-01-01'
  AND mv.visit_date < '2027-01-01'
ORDER BY mv.visit_date;
```

![image-20261008110122536](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008110122536.png)

### 14.

Mostrar las consultas realizadas durante un mes determinado.

```sql
SELECT *
FROM medical_visit
WHERE visit_date >= '2024-05-01'
AND visit_date < '2024-06-01';
```

### 15.

Consultar las mediciones de presión intraocular superiores a 20 mmHg.

```sql
SELECT
    pressure_id,
    visit_id,
    eye_id,
    measured_at,
    pressure_value,
    unit,
    method
FROM intraocular_pressure
WHERE pressure_value > 20
ORDER BY pressure_value DESC;
```



### 16.

Mostrar las mediciones de presión intraocular correspondientes únicamente al ojo derecho.

```sql
SELECT
    iop.pressure_id,
    iop.visit_id,
    iop.measured_at,
    iop.pressure_value,
    iop.unit,
    iop.method
FROM intraocular_pressure iop
INNER JOIN eye e
    ON e.eye_id = iop.eye_id
WHERE e.code = 'OD'
ORDER BY iop.measured_at;
```

![image-20261008110455476](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008110455476.png)

### 17.

Mostrar las mediciones correspondientes únicamente al ojo izquierdo.

```sql
SELECT
    iop.pressure_id,
    iop.visit_id,
    iop.measured_at,
    iop.pressure_value,
    iop.unit,
    iop.method
FROM intraocular_pressure iop
INNER JOIN eye e
    ON e.eye_id = iop.eye_id
WHERE e.code = 'OI'
ORDER BY iop.measured_at;
```



### 18.

Consultar todos los tratamientos que se encuentren activos.

```sql
SELECT
    t.treatment_id,
    t.visit_id,
    ts.name AS status,
    t.description,
    t.start_date,
    t.end_date,
    t.observations
FROM treatment t
INNER JOIN treatment_status ts
    ON ts.treatment_status_id = t.treatment_status_id
WHERE ts.name = 'Activo';
```

![image-20261008110555217](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008110555217.png)

### 19.

Mostrar todos los tratamientos que hayan finalizado.

```sql
SELECT
    t.treatment_id,
    t.visit_id,
    ts.name AS status,
    t.description,
    t.start_date,
    t.end_date
FROM treatment t
INNER JOIN treatment_status ts
    ON ts.treatment_status_id = t.treatment_status_id
WHERE ts.name = 'Finalizado';
```

![image-20261008111328250](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111328250.png)

### 20.

Consultar los procedimientos realizados después de una fecha determinada.

```sql
SELECT
    vp.visit_procedure_id,
    vp.visit_id,
    mp.name AS procedure_name,
    vp.performed_at,
    vp.observations
FROM visit_procedure vp
INNER JOIN medical_procedure mp
    ON mp.procedure_id = vp.procedure_id
WHERE vp.performed_at > '2026-01-01'
ORDER BY vp.performed_at;
```

![image-20261008111426786](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111426786.png)

## Nivel intermedio

### 21.

Mostrar cada paciente junto con el número de su historia clínica.

```sql
SELECT
    p.patient_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    ch.clinical_history_id,
    ch.history_number
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch
    ON ch.patient_id = p.patient_id;
```

![image-20261008111529733](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111529733.png)

### 22.

Mostrar cada consulta indicando el nombre completo del paciente.

```sql
SELECT
    mv.visit_id,
    mv.visit_date,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    mv.reason
FROM medical_visit mv
INNER JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p
    ON p.patient_id = ch.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
ORDER BY mv.visit_date;
```

![image-20261008111610274](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111610274.png)

### 23.

Mostrar cada consulta junto con el nombre del profesional que la realizó.

```sql
SELECT
    mv.visit_id,
    mv.visit_date,
    CONCAT(pe.first_name, ' ', pe.last_name) AS professional
FROM medical_visit mv
INNER JOIN healthcare_professional hp
    ON hp.professional_id = mv.professional_id
INNER JOIN person pe
    ON pe.person_id = hp.person_id
ORDER BY mv.visit_date;
```

![image-20261008111700277](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111700277.png)

### 24.

Listar todos los pacientes junto con la fecha de sus consultas.

```sql
SELECT
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    mv.visit_date
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv
    ON mv.clinical_history_id = ch.clinical_history_id
ORDER BY patient, mv.visit_date;
```

![image-20261008111745491](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111745491.png)

### 25.

Mostrar los diagnósticos asociados a cada consulta.

```sql
SELECT
    mv.visit_id,
    mv.visit_date,
    d.code,
    d.name AS diagnosis
FROM medical_visit mv
INNER JOIN visit_diagnosis vd
    ON vd.visit_id = mv.visit_id
INNER JOIN diagnosis d
    ON d.diagnosis_id = vd.diagnosis_id
ORDER BY mv.visit_date;
```

![image-20261008111817978](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111817978.png)

### 26.

Mostrar nombre del paciente, fecha de consulta y diagnóstico correspondiente.

```sql
SELECT
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    mv.visit_date,
    d.name AS diagnosis
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv
    ON mv.clinical_history_id = ch.clinical_history_id
INNER JOIN visit_diagnosis vd
    ON vd.visit_id = mv.visit_id
INNER JOIN diagnosis d
    ON d.diagnosis_id = vd.diagnosis_id
ORDER BY patient, mv.visit_date;
```

![image-20261008111942461](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008111942461.png)

### 27.

Consultar todos los pacientes que tengan diagnóstico de glaucoma.

```sql
SELECT DISTINCT
    p.patient_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN glaucoma_record gr
    ON gr.patient_id = p.patient_id
INNER JOIN glaucoma_type gt
    ON gt.glaucoma_type_id = gr.glaucoma_type_id;
```

![image-20261008112329940](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008112329940.png)

### 28.

Mostrar todos los controles de glaucoma indicando el paciente correspondiente.

```
SELECT
    gc.glaucoma_control_id,
    gc.control_date,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    gt.name AS glaucoma_type,
    gc.observations
FROM glaucoma_control gc
INNER JOIN glaucoma_record gr
    ON gr.glaucoma_record_id = gc.glaucoma_record_id
INNER JOIN patient p
    ON p.patient_id = gr.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN glaucoma_type gt
    ON gt.glaucoma_type_id = gr.glaucoma_type_id
ORDER BY gc.control_date;
```

![image-20261008112402291](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008112402291.png)

### 29.

Mostrar cada medición de presión intraocular junto con nombre del paciente, fecha y ojo.

```sql
SELECT
    iop.pressure_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    iop.measured_at,
    e.code AS eye,
    iop.pressure_value,
    iop.unit,
    iop.method
FROM intraocular_pressure iop
INNER JOIN medical_visit mv
    ON mv.visit_id = iop.visit_id
INNER JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p
    ON p.patient_id = ch.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN eye e
    ON e.eye_id = iop.eye_id
ORDER BY iop.measured_at;
```

![image-20261008112445330](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008112445330.png)

### 30.

Mostrar los estudios OCT realizados indicando paciente, ojo y fecha.

```sql
SELECT
    ce.clinical_exam_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    e.code AS eye,
    ce.exam_date,
    et.name AS exam_type
FROM clinical_exam ce
INNER JOIN exam_type et
    ON et.exam_type_id = ce.exam_type_id
INNER JOIN medical_visit mv
    ON mv.visit_id = ce.visit_id
INNER JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p
    ON p.patient_id = ch.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
LEFT JOIN eye e
    ON e.eye_id = ce.eye_id
WHERE et.name LIKE '%OCT%';
```



### 31.

Mostrar los campos visuales registrados indicando paciente, ojo, MD, PSD y VFI.

```sql
SELECT
    ce.clinical_exam_id,
    ce.exam_date,
    ep.name AS parametro,
    er.value_numeric
FROM clinical_exam ce
JOIN exam_result er
    ON er.clinical_exam_id = ce.clinical_exam_id
JOIN exam_parameter ep
    ON ep.parameter_id = er.parameter_id
ORDER BY ce.exam_date;
```

![image-20261008120413719](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008120413719.png)

### 32.

Mostrar las paquimetrías realizadas junto con el paciente y el espesor corneal registrado.

```sql
SELECT
    ce.clinical_exam_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    ce.exam_date,
    e.code AS eye,
    ep.name AS parameter,
    er.value_numeric AS value
FROM clinical_exam ce
INNER JOIN exam_type et
    ON et.exam_type_id = ce.exam_type_id
INNER JOIN medical_visit mv
    ON mv.visit_id = ce.visit_id
INNER JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p
    ON p.patient_id = ch.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
LEFT JOIN eye e
    ON e.eye_id = ce.eye_id
INNER JOIN exam_result er
    ON er.clinical_exam_id = ce.clinical_exam_id
INNER JOIN exam_parameter ep
    ON ep.parameter_id = er.parameter_id
WHERE et.name LIKE '%Paquimetra corneal%';
```

![image-20261008120749798](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008120749798.png)

### 33.

Mostrar los tratamientos activos incluyendo nombre del paciente y medicamento.

```sql
SELECT
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    t.treatment_id,
    m.name AS medication,
    tm.dosage,
    tm.frequency,
    tm.duration
FROM treatment t
INNER JOIN treatment_status ts
    ON ts.treatment_status_id = t.treatment_status_id
INNER JOIN medical_visit mv
    ON mv.visit_id = t.visit_id
INNER JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p
    ON p.patient_id = ch.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN treatment_medication tm
    ON tm.treatment_id = t.treatment_id
INNER JOIN medication m
    ON m.medication_id = tm.medication_id
WHERE ts.name = 'Activo';
```

![image-20261008121243711](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008121243711.png)

### 34.

Mostrar cada medicamento y la cantidad de tratamientos en los que ha sido utilizado.

```sql
SELECT
    m.medication_id,
    m.name,
    COUNT(DISTINCT tm.treatment_id) AS total_treatments
FROM medication m
LEFT JOIN treatment_medication tm
    ON tm.medication_id = m.medication_id
GROUP BY
    m.medication_id,
    m.name
ORDER BY total_treatments DESC;
```

![image-20261008121620846](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008121620846.png)

### 35.

Mostrar la cantidad total de pacientes registrados.

```sql
SELECT COUNT(*) AS total_patients
FROM patient;
```

![image-20261008121720988](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008121720988.png)

### 36.

Mostrar la cantidad de consultas realizadas.

```sql
SELECT COUNT(*) AS total_visits
FROM medical_visit;
```

![image-20261008121802014](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008121802014.png)

### 37.

Mostrar la cantidad de pacientes por sexo.

```sql
SELECT
    pe.gender,
    COUNT(*) AS total_patients
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
GROUP BY pe.gender;
```

![image-20261008121842297](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008121842297.png)

### 38.

Mostrar la cantidad de pacientes atendidos por cada profesional.

```sql
SELECT
    hp.professional_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS professional,
    COUNT(DISTINCT ch.patient_id) AS total_patients
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
LEFT JOIN medical_visit mv
    ON mv.professional_id = hp.professional_id
LEFT JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
GROUP BY
    hp.professional_id,
    pe.first_name,
    pe.last_name
ORDER BY total_patients DESC;
```

![image-20261008121926656](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008121926656.png)

### 39.

Calcular el promedio general de presión intraocular.

```sql
SELECT
    AVG(pressure_value) AS average_pressure
FROM intraocular_pressure;
```

![image-20261008122303528](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008122303528.png)

### 40.

Calcular la presión intraocular mínima y máxima registrada.

```sql
SELECT
    MIN(pressure_value) AS minimum_pressure,
    MAX(pressure_value) AS maximum_pressure
FROM intraocular_pressure;
```

![image-20261008122344979](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008122344979.png)

## Nivel avanzado

### 41.

Calcular la presión intraocular promedio para OD y OI por separado.

```sql
SELECT
    e.code AS eye,
    AVG(iop.pressure_value) AS average_pressure
FROM intraocular_pressure iop
INNER JOIN eye e
    ON e.eye_id = iop.eye_id
WHERE e.code IN ('OD', 'OI')
GROUP BY e.code;
```

![image-20261008122501588](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008122501588.png)

### 42.

Mostrar la cantidad de consultas realizadas por cada paciente.

```sql
SELECT
    p.patient_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    COUNT(mv.visit_id) AS total_visits
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv
    ON mv.clinical_history_id = ch.clinical_history_id
GROUP BY
    p.patient_id,
    pe.first_name,
    pe.last_name
ORDER BY total_visits DESC;
```

![image-20261008123015425](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008123015425.png)

### 43.

Mostrar únicamente los pacientes que tengan tres o más consultas.

```sql
SELECT
    p.patient_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS patient,
    COUNT(mv.visit_id) AS total_visits
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv
    ON mv.clinical_history_id = ch.clinical_history_id
GROUP BY
    p.patient_id,
    pe.first_name,
    pe.last_name
HAVING COUNT(mv.visit_id) >= 3;
```



### ![image-20261008125519773](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008125519773.png)

### 44.

Mostrar cada profesional junto con la cantidad de consultas realizadas.

```sql
SELECT
    hp.professional_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS professional,
    COUNT(mv.visit_id) AS total_visits
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
LEFT JOIN medical_visit mv
    ON mv.professional_id = hp.professional_id
GROUP BY
    hp.professional_id,
    pe.first_name,
    pe.last_name
ORDER BY total_visits DESC;
```

![image-20261008125644036](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008125644036.png)

### 45.

Mostrar los profesionales que hayan realizado más de 20 consultas.

```sql
SELECT
    hp.professional_id,
    CONCAT(pe.first_name, ' ', pe.last_name) AS professional,
    COUNT(mv.visit_id) AS total_visits
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
INNER JOIN medical_visit mv
    ON mv.professional_id = hp.professional_id
GROUP BY
    hp.professional_id,
    pe.first_name,
    pe.last_name
HAVING COUNT(mv.visit_id) > 20;
```

![image-20261008125730816](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008125730816.png)

### 46.

Calcular la cantidad de diagnósticos registrados por tipo de diagnóstico.

```sql
SELECT
    d.diagnosis_id,
    d.name,
    COUNT(vd.visit_id) AS total
FROM diagnosis d
LEFT JOIN visit_diagnosis vd
    ON vd.diagnosis_id = d.diagnosis_id
GROUP BY
    d.diagnosis_id,
    d.name
ORDER BY total DESC;
```

![image-20261008125809604](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008125809604.png)

### 47.

Mostrar los cinco diagnósticos más frecuentes.

```sql
SELECT
    d.diagnosis_id,
    d.name,
    COUNT(vd.visit_id) AS total
FROM diagnosis d
INNER JOIN visit_diagnosis vd
    ON vd.diagnosis_id = d.diagnosis_id
GROUP BY
    d.diagnosis_id,
    d.name
ORDER BY total DESC
LIMIT 5;
```

![image-20261008125940595](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008125940595.png)

### 48.

Mostrar la cantidad de estudios OCT realizados por mes.

```sql
SELECT
    YEAR(ce.exam_date) AS year,
    MONTH(ce.exam_date) AS month,
    COUNT(*) AS total_oct
FROM clinical_exam ce
INNER JOIN exam_type et
    ON et.exam_type_id = ce.exam_type_id
WHERE et.name LIKE '%OCT%'
GROUP BY
    YEAR(ce.exam_date),
    MONTH(ce.exam_date)
ORDER BY
    year,
    month;
```



### 49.

Mostrar la cantidad de campos visuales realizados por año.

```sql
SELECT
    YEAR(ce.exam_date) AS year,
    COUNT(*) AS total_visual_fields
FROM clinical_exam ce
INNER JOIN exam_type et
    ON et.exam_type_id = ce.exam_type_id
WHERE et.name LIKE '%Campo visual%'
GROUP BY YEAR(ce.exam_date)
ORDER BY year;
```



### 50.

Generar un reporte que muestre por paciente: nombre completo, número de consultas, cantidad de controles de glaucoma, promedio de PIO y fecha de última consulta.

```sql
SELECT
    p.patient_id,

    CONCAT(
        pe.first_name, ' ',
        pe.last_name
    ) AS patient,

    COUNT(DISTINCT mv.visit_id) AS total_visits,

    COUNT(DISTINCT gc.glaucoma_control_id)
        AS glaucoma_controls,

    AVG(iop.pressure_value)
        AS average_iop,

    MAX(mv.visit_date)
        AS last_visit

FROM patient p

INNER JOIN person pe
    ON pe.person_id = p.person_id

LEFT JOIN clinical_history ch
    ON ch.patient_id = p.patient_id

LEFT JOIN medical_visit mv
    ON mv.clinical_history_id = ch.clinical_history_id

LEFT JOIN glaucoma_record gr
    ON gr.patient_id = p.patient_id

LEFT JOIN glaucoma_control gc
    ON gc.glaucoma_record_id = gr.glaucoma_record_id

LEFT JOIN intraocular_pressure iop
    ON iop.visit_id = mv.visit_id

GROUP BY
    p.patient_id,
    pe.first_name,
    pe.last_name

ORDER BY patient;
```

![image-20261008130132478](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008130132478.png)

# PARTE II — 50 EJERCICIOS DE SUBCONSULTAS

## Subconsultas escalares

### 1.

Mostrar los pacientes cuya edad sea superior a la edad promedio de todos los pacientes.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    pe.birth_date,
    TIMESTAMPDIFF(YEAR, pe.birth_date, CURDATE()) AS age
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE pe.birth_date IS NOT NULL
  AND TIMESTAMPDIFF(YEAR, pe.birth_date, CURDATE()) > (
      SELECT AVG(TIMESTAMPDIFF(YEAR, pe_sub.birth_date, CURDATE()))
      FROM patient p_sub
      INNER JOIN person pe_sub
          ON pe_sub.person_id = p_sub.person_id
      WHERE pe_sub.birth_date IS NOT NULL
  )
ORDER BY age DESC;
```



### ![image-20261008135151356](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008135151356.png)

### 2.

Mostrar los pacientes cuya edad sea inferior a la edad promedio.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    pe.birth_date,
    TIMESTAMPDIFF(YEAR, pe.birth_date, CURDATE()) AS age
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE pe.birth_date IS NOT NULL
  AND TIMESTAMPDIFF(YEAR, pe.birth_date, CURDATE()) < (
      SELECT AVG(TIMESTAMPDIFF(YEAR, pe_sub.birth_date, CURDATE()))
      FROM patient p_sub
      INNER JOIN person pe_sub
          ON pe_sub.person_id = p_sub.person_id
      WHERE pe_sub.birth_date IS NOT NULL
  )
ORDER BY age ASC;
```

### ![image-20261008135332272](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008135332272.png)

### 3.

Consultar la medición de presión intraocular más alta registrada.

```sql
SELECT
    iop.pressure_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    iop.visit_id,
    e.code AS eye,
    iop.measured_at,
    iop.pressure_value,
    iop.unit,
    iop.method
FROM intraocular_pressure iop
INNER JOIN medical_visit mv
    ON mv.visit_id = iop.visit_id
INNER JOIN clinical_history ch
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p
    ON p.patient_id = ch.patient_id
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN eye e
    ON e.eye_id = iop.eye_id
WHERE iop.pressure_value = (
    SELECT MAX(pressure_value)
    FROM intraocular_pressure
);
```

![image-20261008135449383](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008135449383.png)

### 4.

Mostrar todas las mediciones que tengan el mismo valor que la presión máxima registrada.

```sql
SELECT
    pressure_id,
    visit_id,
    eye_id,
    measured_at,
    pressure_value,
    unit,
    method
FROM intraocular_pressure
WHERE pressure_value = (
    SELECT MAX(pressure_value)
    FROM intraocular_pressure
);
```



### ![image-20261008135859767](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008135859767.png)5.

Mostrar la presión intraocular mínima registrada.

```sql
SELECT
    pressure_id,
    visit_id,
    eye_id,
    measured_at,
    pressure_value,
    unit,
    method
FROM intraocular_pressure
WHERE pressure_value = (
    SELECT MIN(pressure_value)
    FROM intraocular_pressure
);
```

![image-20261008140151882](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008140151882.png)

### 6.

Mostrar los estudios OCT cuyo RNFL sea inferior al promedio general.

```sql
SELECT
    ce.clinical_exam_id,
    ce.visit_id,
    ce.professional_id,
    ce.eye_id,
    ce.exam_date,
    ep.name AS parameter_name,
    er.value_numeric AS rnfl_value
FROM clinical_exam ce
INNER JOIN exam_type et
    ON et.exam_type_id = ce.exam_type_id
INNER JOIN exam_result er
    ON er.clinical_exam_id = ce.clinical_exam_id
INNER JOIN exam_parameter ep
    ON ep.parameter_id = er.parameter_id
WHERE et.name LIKE '%OCT%'
  AND ep.name LIKE '%RNFL%'
  AND er.value_numeric < (
      SELECT AVG(er_sub.value_numeric)
      FROM clinical_exam ce_sub
      INNER JOIN exam_type et_sub
          ON et_sub.exam_type_id = ce_sub.exam_type_id
      INNER JOIN exam_result er_sub
          ON er_sub.clinical_exam_id = ce_sub.clinical_exam_id
      INNER JOIN exam_parameter ep_sub
          ON ep_sub.parameter_id = er_sub.parameter_id
      WHERE et_sub.name LIKE '%OCT%'
        AND ep_sub.name LIKE '%RNFL%'
  );
```

![image-20261008140926562](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008140926562.png)

### 7.

Mostrar los estudios OCT cuyo RNFL sea superior al promedio general.

```sql
SELECT
    ce.clinical_exam_id,
    ce.visit_id,
    ce.professional_id,
    ce.eye_id,
    ce.exam_date,
    ep.name AS parameter_name,
    er.value_numeric AS rnfl_value
FROM clinical_exam ce
INNER JOIN exam_type et
    ON et.exam_type_id = ce.exam_type_id
INNER JOIN exam_result er
    ON er.clinical_exam_id = ce.clinical_exam_id
INNER JOIN exam_parameter ep
    ON ep.parameter_id = er.parameter_id
WHERE et.name LIKE '%OCT%'
  AND ep.name LIKE '%RNFL%'
  AND er.value_numeric > (
      SELECT AVG(er_sub.value_numeric)
      FROM clinical_exam ce_sub
      INNER JOIN exam_type et_sub
          ON et_sub.exam_type_id = ce_sub.exam_type_id
      INNER JOIN exam_result er_sub
          ON er_sub.clinical_exam_id = ce_sub.clinical_exam_id
      INNER JOIN exam_parameter ep_sub
          ON ep_sub.parameter_id = er_sub.parameter_id
      WHERE et_sub.name LIKE '%OCT%'
        AND ep_sub.name LIKE '%RNFL%'
  );
```

![image-20261008141237062](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008141237062.png)

### 8.

Consultar pacientes cuya cantidad de consultas sea mayor que el promedio de consultas por paciente.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    COUNT(mv.visit_id) AS total_visits
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv
    ON mv.clinical_history_id = ch.clinical_history_id
GROUP BY
    p.patient_id,
    pe.identification_number,
    pe.first_name,
    pe.middle_name,
    pe.last_name,
    pe.second_last_name
HAVING COUNT(mv.visit_id) > (
    SELECT AVG(total_paciente)
    FROM (
        SELECT COUNT(mv_sub.visit_id) AS total_paciente
        FROM patient p_sub
        INNER JOIN clinical_history ch_sub
            ON ch_sub.patient_id = p_sub.patient_id
        INNER JOIN medical_visit mv_sub
            ON mv_sub.clinical_history_id = ch_sub.clinical_history_id
        GROUP BY p_sub.patient_id
    ) AS resumen_consultas
);
```

![image-20261008141536983](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008141536983.png)

### 9.

Mostrar profesionales cuya cantidad de consultas sea superior al promedio por profesional.

```sql
SELECT
    hp.professional_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS professional_name,
    COUNT(mv.visit_id) AS total_visits
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
INNER JOIN medical_visit mv
    ON mv.professional_id = hp.professional_id
GROUP BY
    hp.professional_id,
    pe.identification_number,
    pe.first_name,
    pe.middle_name,
    pe.last_name,
    pe.second_last_name
HAVING COUNT(mv.visit_id) > (
    SELECT AVG(total_profesional)
    FROM (
        SELECT COUNT(mv_sub.visit_id) AS total_profesional
        FROM healthcare_professional hp_sub
        INNER JOIN medical_visit mv_sub
            ON mv_sub.professional_id = hp_sub.professional_id
        GROUP BY hp_sub.professional_id
    ) AS resumen_profesionales
);
```



### ![image-20261008141634942](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008141634942.png)

### 10.

Consultar pacientes cuya última presión intraocular sea superior al promedio general.

```sql
SELECT 
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    iop.measured_at AS ultima_fecha_medicion,
    e.code AS eye,
    iop.pressure_value AS ultima_presion
FROM patient p
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch 
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv 
    ON mv.clinical_history_id = ch.clinical_history_id
INNER JOIN intraocular_pressure iop 
    ON iop.visit_id = mv.visit_id
INNER JOIN eye e 
    ON e.eye_id = iop.eye_id
WHERE iop.measured_at = (
    -- Subconsulta 1: Obtiene la fecha/hora de la última medición de PIO de este paciente específico
    SELECT MAX(iop_sub.measured_at)
    FROM intraocular_pressure iop_sub
    INNER JOIN medical_visit mv_sub 
        ON mv_sub.visit_id = iop_sub.visit_id
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
)
AND iop.pressure_value > (
    -- Subconsulta 2: Calcula el promedio general de todas las presiones registradas
    SELECT AVG(pressure_value)
    FROM intraocular_pressure
);
```

### ![image-20261008141759938](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008141759938.png)Subconsultas con IN

### 11.

Mostrar pacientes que tengan al menos una consulta registrada.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
);
```

![image-20261008142303780](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142303780.png)

### 12.

Mostrar pacientes que tengan diagnóstico de glaucoma.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT gr.patient_id
    FROM glaucoma_record gr
    UNION
    SELECT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN visit_diagnosis vd
        ON vd.visit_id = mv.visit_id
    INNER JOIN diagnosis d
        ON d.diagnosis_id = vd.diagnosis_id
    WHERE d.name LIKE '%Glaucoma%' OR d.code LIKE 'H40%'
);
```

![image-20261008142409008](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142409008.png)

### 13.

Mostrar pacientes que hayan recibido tratamiento farmacológico.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN treatment t
        ON t.visit_id = mv.visit_id
    INNER JOIN treatment_medication tm
        ON tm.treatment_id = t.treatment_id
);
```

![image-20261008142504190](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142504190.png)

### 14.

Mostrar pacientes que tengan estudios OCT registrados.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN clinical_exam ce
        ON ce.visit_id = mv.visit_id
    INNER JOIN exam_type et
        ON et.exam_type_id = ce.exam_type_id
    WHERE et.name LIKE '%OCT%'
);
```

![image-20261008142538495](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142538495.png)

### 15.

Mostrar pacientes que tengan campos visuales registrados.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN clinical_exam ce
        ON ce.visit_id = mv.visit_id
    INNER JOIN exam_type et
        ON et.exam_type_id = ce.exam_type_id
    WHERE et.name LIKE '%Campimetría%' OR et.name LIKE '%Campo visual%'
);
```



### 16.

Mostrar medicamentos que hayan sido utilizados en al menos un tratamiento.

```sql
SELECT
    medication_id,
    name,
    active_ingredient,
    concentration,
    presentation
FROM medication
WHERE medication_id IN (
    SELECT DISTINCT medication_id
    FROM treatment_medication
);
```

![image-20261008142658524](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142658524.png)

### 17.

Mostrar profesionales que hayan atendido pacientes con glaucoma.

```sql
SELECT
    hp.professional_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS professional_name
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
WHERE hp.professional_id IN (
    SELECT DISTINCT mv.professional_id
    FROM medical_visit mv
    INNER JOIN visit_diagnosis vd
        ON vd.visit_id = mv.visit_id
    INNER JOIN diagnosis d
        ON d.diagnosis_id = vd.diagnosis_id
    WHERE d.name LIKE '%Glaucoma%' OR d.code LIKE 'H40%'
);
```

![image-20261008142739517](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142739517.png)

### 18.

Mostrar diagnósticos utilizados en alguna consulta.

```sql
SELECT
    diagnosis_id,
    code,
    name,
    description
FROM diagnosis
WHERE diagnosis_id IN (
    SELECT DISTINCT diagnosis_id
    FROM visit_diagnosis
);
```

![image-20261008142819959](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142819959.png)

### 19.

Mostrar pacientes que hayan tenido algún procedimiento quirúrgico.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN visit_procedure vp
        ON vp.visit_id = mv.visit_id
);
```

![image-20261008142856954](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142856954.png)

### 20.

Mostrar pacientes que tengan registros de paquimetría.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN clinical_exam ce
        ON ce.visit_id = mv.visit_id
    INNER JOIN exam_type et
        ON et.exam_type_id = ce.exam_type_id
    WHERE et.name LIKE '%Paquimetría%'
);
```



## Subconsultas con NOT IN / NOT EXISTS

### 21.

Mostrar pacientes que nunca hayan tenido una consulta.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
);
```

![image-20261008142022711](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142022711.png)

### 22.

Mostrar pacientes que nunca hayan tenido un control de glaucoma.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id IN (
    SELECT gr.patient_id
    FROM glaucoma_record gr
    UNION
    SELECT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN visit_diagnosis vd
        ON vd.visit_id = mv.visit_id
    INNER JOIN diagnosis d
        ON d.diagnosis_id = vd.diagnosis_id
    WHERE d.name LIKE '%Glaucoma%' OR d.code LIKE 'H40%'
);
```

![image-20261008142113118](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008142113118.png)

### 23.

Mostrar pacientes que no tengan estudios OCT.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id NOT IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN clinical_exam ce
        ON ce.visit_id = mv.visit_id
    INNER JOIN exam_type et
        ON et.exam_type_id = ce.exam_type_id
    WHERE et.name LIKE '%OCT%'
);
```

![image-20261008143855177](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008143855177.png)

### 24.

Mostrar pacientes que no tengan campos visuales.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id NOT IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN clinical_exam ce
        ON ce.visit_id = mv.visit_id
    INNER JOIN exam_type et
        ON et.exam_type_id = ce.exam_type_id
    WHERE et.name LIKE '%Campimetría%' OR et.name LIKE '%Campo visual%'
);
```

![image-20261008143939951](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008143939951.png)

### 25.

Mostrar medicamentos que nunca hayan sido utilizados.

```sql
SELECT
    medication_id,
    name,
    active_ingredient,
    concentration,
    presentation
FROM medication
WHERE medication_id NOT IN (
    SELECT DISTINCT medication_id
    FROM treatment_medication
);
```

![image-20261008144048063](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144048063.png)

### 26.

Mostrar profesionales que todavía no hayan registrado consultas.

```sql
SELECT
    hp.professional_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS professional_name
FROM healthcare_professional hp
INNER JOIN person pe
    ON pe.person_id = hp.person_id
WHERE hp.professional_id NOT IN (
    SELECT DISTINCT professional_id
    FROM medical_visit
);
```

![image-20261008144127325](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144127325.png)

### 27.

Mostrar diagnósticos que nunca hayan sido asociados a una consulta.

```sql
SELECT
    diagnosis_id,
    code,
    name,
    description
FROM diagnosis
WHERE diagnosis_id NOT IN (
    SELECT DISTINCT diagnosis_id
    FROM visit_diagnosis
);
```

![image-20261008144201970](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144201970.png)

### 28.

Mostrar pacientes que no tengan tratamientos activos.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id NOT IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN treatment t
        ON t.visit_id = mv.visit_id
    INNER JOIN treatment_status ts
        ON ts.treatment_status_id = t.treatment_status_id
    WHERE ts.name = 'Activo'
);
```

![image-20261008144237827](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144237827.png)

### 29.

Mostrar pacientes que nunca hayan tenido procedimientos.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id NOT IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN visit_procedure vp
        ON vp.visit_id = mv.visit_id
);
```

![image-20261008144324303](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144324303.png)

### 30.

Mostrar pacientes sin mediciones de presión intraocular.

```sql
SELECT
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe
    ON pe.person_id = p.person_id
WHERE p.patient_id NOT IN (
    SELECT DISTINCT ch.patient_id
    FROM clinical_history ch
    INNER JOIN medical_visit mv
        ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN intraocular_pressure iop
        ON iop.visit_id = mv.visit_id
);
```

![image-20261008144407411](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144407411.png)

## Subconsultas correlacionadas

### 31.

Mostrar las mediciones de PIO superiores al promedio del mismo paciente.

```sql
SELECT
    iop.pressure_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    iop.measured_at,
    e.code AS eye,
    iop.pressure_value,
    iop.unit
FROM intraocular_pressure iop
INNER JOIN medical_visit mv 
    ON mv.visit_id = iop.visit_id
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN eye e 
    ON e.eye_id = iop.eye_id
WHERE iop.pressure_value > (
    SELECT AVG(iop_sub.pressure_value)
    FROM intraocular_pressure iop_sub
    INNER JOIN medical_visit mv_sub 
        ON mv_sub.visit_id = iop_sub.visit_id
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
);
```



### ![image-20261008144804683](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144804683.png)32.

Mostrar los estudios OCT cuyo RNFL sea inferior al promedio del mismo paciente.

```sql
SELECT
    ce.clinical_exam_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    ce.exam_date,
    ep.name AS parameter_name,
    er.value_numeric AS rnfl_value
FROM clinical_exam ce
INNER JOIN exam_type et 
    ON et.exam_type_id = ce.exam_type_id
INNER JOIN exam_result er 
    ON er.clinical_exam_id = ce.clinical_exam_id
INNER JOIN exam_parameter ep 
    ON ep.parameter_id = er.parameter_id
INNER JOIN medical_visit mv 
    ON mv.visit_id = ce.visit_id
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
WHERE et.name LIKE '%OCT%'
  AND ep.name LIKE '%RNFL%'
  AND er.value_numeric < (
      SELECT AVG(er_sub.value_numeric)
      FROM clinical_exam ce_sub
      INNER JOIN exam_type et_sub 
          ON et_sub.exam_type_id = ce_sub.exam_type_id
      INNER JOIN exam_result er_sub 
          ON er_sub.clinical_exam_id = ce_sub.clinical_exam_id
      INNER JOIN exam_parameter ep_sub 
          ON ep_sub.parameter_id = er_sub.parameter_id
      INNER JOIN medical_visit mv_sub 
          ON mv_sub.visit_id = ce_sub.visit_id
      INNER JOIN clinical_history ch_sub 
          ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
      WHERE ch_sub.patient_id = p.patient_id
        AND et_sub.name LIKE '%OCT%'
        AND ep_sub.name LIKE '%RNFL%'
  );
```

### ![image-20261008144852256](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144852256.png)33.

Mostrar las consultas posteriores a la primera consulta de cada paciente.

```sql
SELECT
    mv.visit_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    mv.visit_date,
    mv.reason
FROM medical_visit mv
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
WHERE mv.visit_date > (
    SELECT MIN(mv_sub.visit_date)
    FROM medical_visit mv_sub
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
)
ORDER BY p.patient_id, mv.visit_date;
```

### ![image-20261008144939391](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008144939391.png)34.

Mostrar la última consulta de cada paciente utilizando una subconsulta correlacionada.

```sql
SELECT
    mv.visit_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    mv.visit_date,
    mv.reason,
    mv.observations
FROM medical_visit mv
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
WHERE mv.visit_date = (
    SELECT MAX(mv_sub.visit_date)
    FROM medical_visit mv_sub
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
);
```

![image-20261008145026023](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008145026023.png)

### 35.

Mostrar la primera medición de PIO de cada paciente.

```sql
SELECT
    iop.pressure_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    iop.measured_at,
    e.code AS eye,
    iop.pressure_value,
    iop.unit
FROM intraocular_pressure iop
INNER JOIN medical_visit mv 
    ON mv.visit_id = iop.visit_id
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN eye e 
    ON e.eye_id = iop.eye_id
WHERE iop.measured_at = (
    SELECT MIN(iop_sub.measured_at)
    FROM intraocular_pressure iop_sub
    INNER JOIN medical_visit mv_sub 
        ON mv_sub.visit_id = iop_sub.visit_id
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
);
```

![image-20261008145249394](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008145249394.png)

### 36.

Mostrar la última medición de presión intraocular de cada paciente y ojo.

```sql
SELECT
    iop.pressure_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    e.code AS eye,
    iop.measured_at,
    iop.pressure_value,
    iop.unit
FROM intraocular_pressure iop
INNER JOIN medical_visit mv 
    ON mv.visit_id = iop.visit_id
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN eye e 
    ON e.eye_id = iop.eye_id
WHERE iop.measured_at = (
    SELECT MAX(iop_sub.measured_at)
    FROM intraocular_pressure iop_sub
    INNER JOIN medical_visit mv_sub 
        ON mv_sub.visit_id = iop_sub.visit_id
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
      AND iop_sub.eye_id = iop.eye_id
);
```

![image-20261008145400142](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008145400142.png)

### 37.

Mostrar los tratamientos cuya fecha de inicio sea posterior a la primera consulta del paciente.

```sql
SELECT
    t.treatment_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    t.description,
    t.start_date,
    t.end_date
FROM treatment t
INNER JOIN medical_visit mv 
    ON mv.visit_id = t.visit_id
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
WHERE t.start_date > (
    SELECT MIN(DATE(mv_sub.visit_date))
    FROM medical_visit mv_sub
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
    WHERE ch_sub.patient_id = p.patient_id
);
```

![image-20261008145822759](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008145822759.png)

### 38.

Mostrar pacientes cuyo número de consultas sea mayor que el de todos los demás pacientes de su misma ciudad.

```sql
SELECT
    p.patient_id,
    c.name AS city_name,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    COUNT(mv.visit_id) AS total_visits
FROM patient p
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN city c 
    ON c.city_id = pe.city_id
INNER JOIN clinical_history ch 
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv 
    ON mv.clinical_history_id = ch.clinical_history_id
GROUP BY
    p.patient_id,
    c.city_id,
    c.name,
    pe.first_name,
    pe.middle_name,
    pe.last_name,
    pe.second_last_name
HAVING COUNT(mv.visit_id) > ALL (
    SELECT COUNT(mv_sub.visit_id)
    FROM patient p_sub
    INNER JOIN person pe_sub 
        ON pe_sub.person_id = p_sub.person_id
    INNER JOIN clinical_history ch_sub 
        ON ch_sub.patient_id = p_sub.patient_id
    INNER JOIN medical_visit mv_sub 
        ON mv_sub.clinical_history_id = ch_sub.clinical_history_id
    WHERE pe_sub.city_id = pe.city_id
      AND p_sub.patient_id <> p.patient_id
    GROUP BY p_sub.patient_id
);
```



### 39.

Mostrar profesionales cuya cantidad de consultas sea superior al promedio de los profesionales de su especialidad.

```sql
SELECT
    hp.professional_id,
    s.name AS specialty_name,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS professional_name,
    COUNT(mv.visit_id) AS total_visits
FROM healthcare_professional hp
INNER JOIN person pe 
    ON pe.person_id = hp.person_id
INNER JOIN professional_specialty ps 
    ON ps.professional_id = hp.professional_id
INNER JOIN specialty s 
    ON s.specialty_id = ps.specialty_id
INNER JOIN medical_visit mv 
    ON mv.professional_id = hp.professional_id
GROUP BY
    hp.professional_id,
    s.specialty_id,
    s.name,
    pe.first_name,
    pe.middle_name,
    pe.last_name,
    pe.second_last_name
HAVING COUNT(mv.visit_id) > (
    SELECT AVG(total_sub)
    FROM (
        SELECT COUNT(mv_sub.visit_id) AS total_sub
        FROM healthcare_professional hp_sub
        INNER JOIN professional_specialty ps_sub 
            ON ps_sub.professional_id = hp_sub.professional_id
        INNER JOIN medical_visit mv_sub 
            ON mv_sub.professional_id = hp_sub.professional_id
        WHERE ps_sub.specialty_id = s.specialty_id
        GROUP BY hp_sub.professional_id
    ) AS promedio_especialidad
);
```

![image-20261008150634478](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008150634478.png)

### 40.

Mostrar el estudio OCT más reciente de cada paciente.

```sql
SELECT
    ce.clinical_exam_id,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    ce.exam_date,
    et.name AS exam_type,
    ce.observations
FROM clinical_exam ce
INNER JOIN exam_type et 
    ON et.exam_type_id = ce.exam_type_id
INNER JOIN medical_visit mv 
    ON mv.visit_id = ce.visit_id
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
WHERE et.name LIKE '%OCT%'
  AND ce.exam_date = (
      SELECT MAX(ce_sub.exam_date)
      FROM clinical_exam ce_sub
      INNER JOIN exam_type et_sub 
          ON et_sub.exam_type_id = ce_sub.exam_type_id
      INNER JOIN medical_visit mv_sub 
          ON mv_sub.visit_id = ce_sub.visit_id
      INNER JOIN clinical_history ch_sub 
          ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
      WHERE ch_sub.patient_id = p.patient_id
        AND et_sub.name LIKE '%OCT%'
  );
```

![image-20261008150711053](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008150711053.png)

## Subconsultas avanzadas

### 41.

Mostrar pacientes cuya presión intraocular máxima sea mayor que la presión máxima promedio de todos los pacientes.

```sql
SELECT 
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    MAX(iop.pressure_value) AS pio_maxima
FROM patient p
INNER JOIN person pe ON pe.person_id = p.person_id
INNER JOIN clinical_history ch ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
INNER JOIN intraocular_pressure iop ON iop.visit_id = mv.visit_id
GROUP BY p.patient_id, pe.first_name, pe.middle_name, pe.last_name, pe.second_last_name
HAVING MAX(iop.pressure_value) > (
    SELECT AVG(max_pio_paciente)
    FROM (
        SELECT MAX(iop_sub.pressure_value) AS max_pio_paciente
        FROM patient p_sub
        INNER JOIN clinical_history ch_sub ON ch_sub.patient_id = p_sub.patient_id
        INNER JOIN medical_visit mv_sub ON mv_sub.clinical_history_id = ch_sub.clinical_history_id
        INNER JOIN intraocular_pressure iop_sub ON iop_sub.visit_id = mv_sub.visit_id
        GROUP BY p_sub.patient_id
    ) AS tabla_max_pios
);
```



### 42.

Mostrar pacientes cuya cantidad de diagnósticos diferentes sea superior al promedio.

```sql
SELECT 
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    COUNT(DISTINCT vd.diagnosis_id) AS total_diagnosticos_diferentes
FROM patient p
INNER JOIN person pe ON pe.person_id = p.person_id
INNER JOIN clinical_history ch ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
INNER JOIN visit_diagnosis vd ON vd.visit_id = mv.visit_id
GROUP BY p.patient_id, pe.first_name, pe.middle_name, pe.last_name, pe.second_last_name
HAVING COUNT(DISTINCT vd.diagnosis_id) > (
    SELECT AVG(diag_count)
    FROM (
        SELECT COUNT(DISTINCT vd_sub.diagnosis_id) AS diag_count
        FROM patient p_sub
        INNER JOIN clinical_history ch_sub ON ch_sub.patient_id = p_sub.patient_id
        INNER JOIN medical_visit mv_sub ON mv_sub.clinical_history_id = ch_sub.clinical_history_id
        INNER JOIN visit_diagnosis vd_sub ON vd_sub.visit_id = mv_sub.visit_id
        GROUP BY p_sub.patient_id
    ) AS resumen_diag
);
```



### 43.

Mostrar los pacientes que tengan más tratamientos activos que el promedio de tratamientos activos por paciente.

```sql
SELECT 
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    COUNT(t.treatment_id) AS total_tratamientos_activos
FROM patient p
INNER JOIN person pe ON pe.person_id = p.person_id
INNER JOIN clinical_history ch ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
INNER JOIN treatment t ON t.visit_id = mv.visit_id
INNER JOIN treatment_status ts ON ts.treatment_status_id = t.treatment_status_id
WHERE ts.name = 'Activo'
GROUP BY p.patient_id, pe.first_name, pe.middle_name, pe.last_name, pe.second_last_name
HAVING COUNT(t.treatment_id) > (
    SELECT AVG(activos_count)
    FROM (
        SELECT COUNT(t_sub.treatment_id) AS activos_count
        FROM patient p_sub
        INNER JOIN clinical_history ch_sub ON ch_sub.patient_id = p_sub.patient_id
        INNER JOIN medical_visit mv_sub ON mv_sub.clinical_history_id = ch_sub.clinical_history_id
        INNER JOIN treatment t_sub ON t_sub.visit_id = mv_sub.visit_id
        INNER JOIN treatment_status ts_sub ON ts_sub.treatment_status_id = t_sub.treatment_status_id
        WHERE ts_sub.name = 'Activo'
        GROUP BY p_sub.patient_id
    ) AS resumen_activos
);
```



### 44.

Mostrar el medicamento más utilizado en tratamientos.

```sql
SELECT 
    m.medication_id,
    m.name,
    m.active_ingredient,
    COUNT(*) AS veces_recetado
FROM medication m
INNER JOIN treatment_medication tm 
    ON tm.medication_id = m.medication_id
GROUP BY 
    m.medication_id, 
    m.name, 
    m.active_ingredient
HAVING COUNT(*) = (
    SELECT MAX(conteo_med)
    FROM (
        SELECT COUNT(*) AS conteo_med
        FROM treatment_medication
        GROUP BY medication_id
    ) AS resumen_meds
);
```

![image-20261008151802550](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008151802550.png)

### 45.

Mostrar el diagnóstico más frecuente utilizando subconsultas.

```sql
SELECT 
    d.diagnosis_id,
    d.code,
    d.name,
    COUNT(*) AS frecuencia
FROM diagnosis d
INNER JOIN visit_diagnosis vd 
    ON vd.diagnosis_id = d.diagnosis_id
GROUP BY 
    d.diagnosis_id, 
    d.code, 
    d.name
HAVING COUNT(*) = (
    SELECT MAX(frecuencia_diag)
    FROM (
        SELECT COUNT(*) AS frecuencia_diag
        FROM visit_diagnosis
        GROUP BY diagnosis_id
    ) AS resumen_frecuencia
);
```

![image-20261008151949996](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008151949996.png)

### 46.

Mostrar los pacientes cuya última PIO sea inferior a su primera PIO.

```sql
SELECT 
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    primera.pressure_value AS primera_pio,
    ultima.pressure_value AS ultima_pio
FROM patient p
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN (
    SELECT ch.patient_id, iop.pressure_value
    FROM intraocular_pressure iop
    INNER JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    INNER JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE iop.measured_at = (
        SELECT MIN(iop_sub.measured_at)
        FROM intraocular_pressure iop_sub
        INNER JOIN medical_visit mv_sub ON mv_sub.visit_id = iop_sub.visit_id
        INNER JOIN clinical_history ch_sub ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
        WHERE ch_sub.patient_id = ch.patient_id
    )
    GROUP BY ch.patient_id, iop.pressure_value
) AS primera ON primera.patient_id = p.patient_id
INNER JOIN (
    SELECT ch.patient_id, iop.pressure_value
    FROM intraocular_pressure iop
    INNER JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    INNER JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE iop.measured_at = (
        SELECT MAX(iop_sub.measured_at)
        FROM intraocular_pressure iop_sub
        INNER JOIN medical_visit mv_sub ON mv_sub.visit_id = iop_sub.visit_id
        INNER JOIN clinical_history ch_sub ON ch_sub.clinical_history_id = mv_sub.clinical_history_id
        WHERE ch_sub.patient_id = ch.patient_id
    )
    GROUP BY ch.patient_id, iop.pressure_value
) AS ultima ON ultima.patient_id = p.patient_id
WHERE ultima.pressure_value < primera.pressure_value;
```

![image-20261008152119222](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008152119222.png)

### 47.

Mostrar pacientes cuya presión promedio del ojo derecho sea mayor que la del ojo izquierdo.

```sql
SELECT 
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    AVG(CASE WHEN e.code = 'OD' THEN iop.pressure_value END) AS promedio_od,
    AVG(CASE WHEN e.code IN ('OI', 'OS') THEN iop.pressure_value END) AS promedio_oi
FROM patient p
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN clinical_history ch 
    ON ch.patient_id = p.patient_id
INNER JOIN medical_visit mv 
    ON mv.clinical_history_id = ch.clinical_history_id
INNER JOIN intraocular_pressure iop 
    ON iop.visit_id = mv.visit_id
INNER JOIN eye e 
    ON e.eye_id = iop.eye_id
GROUP BY 
    p.patient_id, 
    pe.first_name, 
    pe.middle_name, 
    pe.last_name, 
    pe.second_last_name
HAVING AVG(CASE WHEN e.code = 'OD' THEN iop.pressure_value END) > 
       AVG(CASE WHEN e.code IN ('OI', 'OS') THEN iop.pressure_value END);
```

![image-20261008152200513](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008152200513.png)

### 48.

Mostrar los pacientes con mayor cantidad de controles de glaucoma que el promedio general.

```sql
SELECT 
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    COUNT(*) AS total_controles
FROM patient p
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN glaucoma_record gr 
    ON gr.patient_id = p.patient_id
INNER JOIN glaucoma_control gc 
    ON gc.glaucoma_record_id = gr.glaucoma_record_id
GROUP BY 
    p.patient_id, 
    pe.first_name, 
    pe.middle_name, 
    pe.last_name, 
    pe.second_last_name
HAVING COUNT(*) > (
    SELECT AVG(controles_paciente)
    FROM (
        SELECT COUNT(*) AS controles_paciente
        FROM glaucoma_record gr_sub
        INNER JOIN glaucoma_control gc_sub 
            ON gc_sub.glaucoma_record_id = gr_sub.glaucoma_record_id
        GROUP BY gr_sub.patient_id
    ) AS resumen_controles
);
```



### 49.

Mostrar las consultas que tengan más diagnósticos asociados que el promedio de diagnósticos por consulta.

```sql
SELECT 
    mv.visit_id,
    mv.visit_date,
    p.patient_id,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name,
    COUNT(*) AS total_diagnosticos
FROM medical_visit mv
INNER JOIN clinical_history ch 
    ON ch.clinical_history_id = mv.clinical_history_id
INNER JOIN patient p 
    ON p.patient_id = ch.patient_id
INNER JOIN person pe 
    ON pe.person_id = p.person_id
INNER JOIN visit_diagnosis vd 
    ON vd.visit_id = mv.visit_id
GROUP BY 
    mv.visit_id, 
    mv.visit_date, 
    p.patient_id, 
    pe.first_name, 
    pe.middle_name, 
    pe.last_name, 
    pe.second_last_name
HAVING COUNT(*) > (
    SELECT AVG(diag_por_consulta)
    FROM (
        SELECT COUNT(*) AS diag_por_consulta
        FROM visit_diagnosis
        GROUP BY visit_id
    ) AS resumen_consultas
);
```



### 50.

Mostrar los pacientes que tengan simultáneamente OCT, campo visual, paquimetría y control de glaucoma registrados.

```sql
SELECT 
    p.patient_id,
    pe.identification_number,
    CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS patient_name
FROM patient p
INNER JOIN person pe 
    ON pe.person_id = p.person_id
WHERE 
    -- 1. Tiene OCT
    p.patient_id IN (
        SELECT DISTINCT ch.patient_id
        FROM clinical_history ch
        INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
        INNER JOIN clinical_exam ce ON ce.visit_id = mv.visit_id
        INNER JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
        WHERE et.name LIKE '%OCT%'
    )
    -- 2. Tiene Campo Visual / Campimetría
    AND p.patient_id IN (
        SELECT DISTINCT ch.patient_id
        FROM clinical_history ch
        INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
        INNER JOIN clinical_exam ce ON ce.visit_id = mv.visit_id
        INNER JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
        WHERE et.name LIKE '%Campimetría%' OR et.name LIKE '%Campo visual%'
    )
    -- 3. Tiene Paquimetría
    AND p.patient_id IN (
        SELECT DISTINCT ch.patient_id
        FROM clinical_history ch
        INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
        INNER JOIN clinical_exam ce ON ce.visit_id = mv.visit_id
        INNER JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
        WHERE et.name LIKE '%Paquimetría%'
    )
    -- 4. Tiene Control de Glaucoma registrado
    AND p.patient_id IN (
        SELECT DISTINCT gr.patient_id
        FROM glaucoma_record gr
        INNER JOIN glaucoma_control gc ON gc.glaucoma_record_id = gr.glaucoma_record_id
    );
```



# PARTE III — 50 EJERCICIOS DE PROCEDIMIENTOS ALMACENADOS

## Procedimientos básicos

### 1.

Crear un procedimiento que liste todos los pacientes.

```sql
DROP PROCEDURE IF EXISTS sp_list_all_patients$$
CREATE PROCEDURE sp_list_all_patients()
BEGIN
    SELECT 
        p.patient_id,
        pe.identification_number,
        CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS full_name,
        pe.birth_date,
        pe.gender,
        c.name AS city_name,
        p.admission_date,
        p.active
    FROM patient p
    INNER JOIN person pe ON pe.person_id = p.person_id
    LEFT JOIN city c ON c.city_id = pe.city_id;
END$$
```

![image-20261008152824381](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008152824381.png)

### 2.

Crear un procedimiento que reciba el ID de un paciente y muestre sus datos.

```sql
DROP PROCEDURE IF EXISTS sp_get_patient_by_id$$
CREATE PROCEDURE sp_get_patient_by_id(
    IN p_patient_id INT
)
BEGIN
    SELECT 
        p.patient_id,
        pe.identification_number,
        CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS full_name,
        pe.birth_date,
        pe.gender,
        c.name AS city_name,
        p.admission_date,
        p.active
    FROM patient p
    INNER JOIN person pe ON pe.person_id = p.person_id
    LEFT JOIN city c ON c.city_id = pe.city_id
    WHERE p.patient_id = p_patient_id;
END$$
```

![image-20261008152954456](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008152954456.png)

### 3.

Crear un procedimiento que busque un paciente por número de documento.

```sql
DROP PROCEDURE IF EXISTS sp_get_patient_by_document$$
CREATE PROCEDURE sp_get_patient_by_document(
    IN p_doc_number VARCHAR(50)
)
BEGIN
    SELECT 
        p.patient_id,
        pe.identification_number,
        CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS full_name,
        pe.birth_date,
        pe.gender,
        c.name AS city_name,
        p.admission_date,
        p.active
    FROM patient p
    INNER JOIN person pe ON pe.person_id = p.person_id
    LEFT JOIN city c ON c.city_id = pe.city_id
    WHERE pe.identification_number = p_doc_number;
END$$
```



### 4.

Crear un procedimiento que liste todas las consultas de un paciente.

```sql
DROP PROCEDURE IF EXISTS sp_list_patient_visits$$
CREATE PROCEDURE sp_list_patient_visits(
    IN p_patient_id INT
)
BEGIN
    SELECT 
        mv.visit_id,
        mv.visit_date,
        mv.reason,
        mv.observations,
        CONCAT(pe_prof.first_name, ' ', pe_prof.last_name) AS professional_name
    FROM medical_visit mv
    INNER JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    INNER JOIN healthcare_professional hp ON hp.professional_id = mv.professional_id
    INNER JOIN person pe_prof ON pe_prof.person_id = hp.person_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY mv.visit_date DESC;
END$$
```

![image-20261008153152162](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008153152162.png)

### 5.

Crear un procedimiento que muestre todos los profesionales.

```sql
DROP PROCEDURE IF EXISTS sp_list_all_professionals$$
CREATE PROCEDURE sp_list_all_professionals()
BEGIN
    SELECT 
        hp.professional_id,
        pe.identification_number,
        CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS professional_name,
        hp.professional_license,
        hp.active
    FROM healthcare_professional hp
    INNER JOIN person pe ON pe.person_id = hp.person_id;
END$$
```

![image-20261008153404684](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008153404684.png)

### 6.

Crear un procedimiento que reciba una especialidad y muestre sus profesionales.

```sql
DROP PROCEDURE IF EXISTS sp_get_professionals_by_specialty$$
CREATE PROCEDURE sp_get_professionals_by_specialty(
    IN p_specialty_name VARCHAR(100)
)
BEGIN
    SELECT 
        hp.professional_id,
        CONCAT(pe.first_name, ' ', IFNULL(CONCAT(pe.middle_name, ' '), ''), pe.last_name, ' ', IFNULL(pe.second_last_name, '')) AS professional_name,
        s.name AS specialty_name,
        hp.professional_license
    FROM healthcare_professional hp
    INNER JOIN person pe ON pe.person_id = hp.person_id
    INNER JOIN professional_specialty ps ON ps.professional_id = hp.professional_id
    INNER JOIN specialty s ON s.specialty_id = ps.specialty_id
    WHERE s.name LIKE CONCAT('%', p_specialty_name, '%');
END$$
```



### 7.

Crear un procedimiento que liste diagnósticos.

```sql
DROP PROCEDURE IF EXISTS sp_list_diagnoses$$
CREATE PROCEDURE sp_list_diagnoses()
BEGIN
    SELECT 
        diagnosis_id,
        code,
        name,
        description,
        active
    FROM diagnosis
    ORDER BY code ASC;
END$$
```



### ![image-20261008153608942](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008153608942.png)8.

Crear un procedimiento que muestre medicamentos activos.

```sql
DROP PROCEDURE IF EXISTS sp_list_active_medications$$
CREATE PROCEDURE sp_list_active_medications()
BEGIN
    SELECT 
        medication_id,
        name,
        active_ingredient,
        concentration,
        presentation
    FROM medication;
END$$
```

![image-20261008153716815](C:\Users\johan\AppData\Roaming\Typora\typora-user-images\image-20261008153716815.png)

### 9.

Crear un procedimiento que liste procedimientos clínicos realizados a un paciente.

```sql
DROP PROCEDURE IF EXISTS sp_list_patient_procedures$$
CREATE PROCEDURE sp_list_patient_procedures(
    IN p_patient_id INT
)
BEGIN
    SELECT 
        vp.visit_procedure_id,
        vp.performed_at,
        p_cat.code AS procedure_code,
        p_cat.name AS procedure_name,
        e.code AS eye,
        vp.observations
    FROM visit_procedure vp
    INNER JOIN medical_visit mv ON mv.visit_id = vp.visit_id
    INNER JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    INNER JOIN procedure_catalog p_cat ON p_cat.procedure_id = vp.procedure_id
    LEFT JOIN eye e ON e.eye_id = vp.eye_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY vp.performed_at DESC;
END$$
```



### 10.

Crear un procedimiento para consultar todos los controles de glaucoma de un paciente.

```sql
DROP PROCEDURE IF EXISTS sp_list_patient_glaucoma_controls$$
CREATE PROCEDURE sp_list_patient_glaucoma_controls(
    IN p_patient_id INT
)
BEGIN
    SELECT 
        gc.control_id,
        gr.glaucoma_type,
        gc.control_date,
        gc.target_pressure_reached,
        gc.cup_disk_ratio_od,
        gc.cup_disk_ratio_os,
        gc.observations
    FROM glaucoma_control gc
    INNER JOIN glaucoma_record gr ON gr.glaucoma_record_id = gc.glaucoma_record_id
    WHERE gr.patient_id = p_patient_id
    ORDER BY gc.control_date DESC;
END$$
```



## Procedimientos de inserción

### 11.

Crear un procedimiento para registrar un nuevo paciente.

```sql
DROP PROCEDURE IF EXISTS sp_register_patient$$
CREATE PROCEDURE sp_register_patient(
    IN p_identification_type_id INT,
    IN p_identification_number VARCHAR(50),
    IN p_first_name VARCHAR(100),
    IN p_middle_name VARCHAR(100),
    IN p_last_name VARCHAR(100),
    IN p_second_last_name VARCHAR(100),
    IN p_birth_date DATE,
    IN p_gender VARCHAR(20),
    IN p_city_id INT,
    IN p_admission_date DATE,
    OUT p_new_patient_id INT
)
BEGIN
    DECLARE v_person_id INT;

    INSERT INTO person (
        identification_type_id, identification_number, first_name, middle_name,
        last_name, second_last_name, birth_date, gender, city_id
    )
    VALUES (
        p_identification_type_id, p_identification_number, p_first_name, p_middle_name,
        p_last_name, p_second_last_name, p_birth_date, p_gender, p_city_id
    );

    SET v_person_id = LAST_INSERT_ID();

    INSERT INTO patient (person_id, admission_date, active)
    VALUES (v_person_id, IFNULL(p_admission_date, CURDATE()), TRUE);

    SET p_new_patient_id = LAST_INSERT_ID();
END$$
```



### 12.

Crear un procedimiento para crear una historia clínica.

```sql
DROP PROCEDURE IF EXISTS sp_create_clinical_history;
DELIMITER $$
CREATE PROCEDURE sp_create_clinical_history(
    IN p_patient_id BIGINT,
    IN p_history_number VARCHAR(50),
    OUT p_clinical_history_id BIGINT
)
BEGIN
    INSERT INTO clinical_history (patient_id, history_number, created_at)
    VALUES (p_patient_id, p_history_number, NOW());
    
    SET p_clinical_history_id = LAST_INSERT_ID();
END $$
DELIMITER ;
```

### 13.

Crear un procedimiento para registrar una consulta médica.

```sql
DROP PROCEDURE IF EXISTS sp_register_medical_visit;
DELIMITER $$
CREATE PROCEDURE sp_register_medical_visit(
    IN p_clinical_history_id BIGINT,
    IN p_appointment_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_visit_type_id BIGINT,
    IN p_reason TEXT,
    IN p_observations TEXT,
    OUT p_visit_id BIGINT
)
BEGIN
    INSERT INTO medical_visit (
        clinical_history_id, appointment_id, professional_id,
        visit_type_id, visit_date, reason, observations
    )
    VALUES (
        p_clinical_history_id, p_appointment_id, p_professional_id,
        p_visit_type_id, NOW(), p_reason, p_observations
    );
    
    SET p_visit_id = LAST_INSERT_ID();
END $$
DELIMITER ;
```

### 14.

Crear un procedimiento para registrar un diagnóstico asociado a una consulta.

```sql
DROP PROCEDURE IF EXISTS sp_register_visit_diagnosis;
DELIMITER $$
CREATE PROCEDURE sp_register_visit_diagnosis(
    IN p_visit_id BIGINT,
    IN p_diagnosis_id BIGINT,
    IN p_diagnosis_type VARCHAR(50),
    IN p_observations TEXT
)
BEGIN
    INSERT INTO visit_diagnosis (visit_id, diagnosis_id, diagnosis_type, observations)
    VALUES (p_visit_id, p_diagnosis_id, p_diagnosis_type, p_observations);
END $$
DELIMITER ;
```

### 15.

Crear un procedimiento para registrar una medición de PIO.

```sql
DROP PROCEDURE IF EXISTS sp_register_intraocular_pressure;
DELIMITER $$
CREATE PROCEDURE sp_register_intraocular_pressure(
    IN p_visit_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_pressure_value DECIMAL(6,2),
    IN p_method VARCHAR(100),
    OUT p_pressure_id BIGINT
)
BEGIN
    INSERT INTO intraocular_pressure (visit_id, eye_id, measured_at, pressure_value, unit, method)
    VALUES (p_visit_id, p_eye_id, NOW(), p_pressure_value, 'mmHg', p_method);
    
    SET p_pressure_id = LAST_INSERT_ID();
END $$
DELIMITER ;
```

### 16.

Crear un procedimiento para registrar un control de glaucoma.

```sql
DROP PROCEDURE IF EXISTS sp_register_glaucoma_control;
DELIMITER $$
CREATE PROCEDURE sp_register_glaucoma_control(
    IN p_glaucoma_record_id BIGINT,
    IN p_visit_id BIGINT,
    IN p_control_date DATE,
    IN p_observations TEXT,
    OUT p_control_id BIGINT
)
BEGIN
    INSERT INTO glaucoma_control (glaucoma_record_id, visit_id, control_date, observations)
    VALUES (p_glaucoma_record_id, p_visit_id, IFNULL(p_control_date, CURDATE()), p_observations);
    
    SET p_control_id = LAST_INSERT_ID();
END $$
DELIMITER ;
```

### 17.

Crear un procedimiento para registrar un examen OCT.

```sql
DROP PROCEDURE IF EXISTS sp_register_oct_exam;
DELIMITER $$
CREATE PROCEDURE sp_register_oct_exam(
    IN p_visit_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_rnfl_value DECIMAL(12,4),
    IN p_observations TEXT,
    OUT p_exam_id BIGINT
)
BEGIN
    DECLARE v_exam_type_id BIGINT;
    DECLARE v_param_id BIGINT;

    SELECT exam_type_id INTO v_exam_type_id FROM exam_type WHERE name LIKE '%OCT%' LIMIT 1;
    IF v_exam_type_id IS NULL THEN
        SELECT exam_type_id INTO v_exam_type_id FROM exam_type LIMIT 1;
    END IF;

    INSERT INTO clinical_exam (visit_id, exam_type_id, professional_id, eye_id, exam_date, observations)
    VALUES (p_visit_id, v_exam_type_id, p_professional_id, p_eye_id, NOW(), p_observations);
    
    SET p_exam_id = LAST_INSERT_ID();

    SELECT parameter_id INTO v_param_id FROM exam_parameter WHERE exam_type_id = v_exam_type_id LIMIT 1;
    IF v_param_id IS NOT NULL THEN
        INSERT INTO exam_result (clinical_exam_id, parameter_id, value_numeric)
        VALUES (p_exam_id, v_param_id, p_rnfl_value);
    END IF;
END $$
DELIMITER ;
```

### 18.

Crear un procedimiento para registrar un campo visual.

```sql
DROP PROCEDURE IF EXISTS sp_register_visual_field;
DELIMITER $$
CREATE PROCEDURE sp_register_visual_field(
    IN p_visit_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_vfi_value DECIMAL(12,4),
    IN p_observations TEXT,
    OUT p_exam_id BIGINT
)
BEGIN
    DECLARE v_exam_type_id BIGINT;
    DECLARE v_param_id BIGINT;

    SELECT exam_type_id INTO v_exam_type_id FROM exam_type WHERE name LIKE '%Campimetría%' OR name LIKE '%Campo visual%' LIMIT 1;

    INSERT INTO clinical_exam (visit_id, exam_type_id, professional_id, eye_id, exam_date, observations)
    VALUES (p_visit_id, v_exam_type_id, p_professional_id, p_eye_id, NOW(), p_observations);
    
    SET p_exam_id = LAST_INSERT_ID();

    SELECT parameter_id INTO v_param_id FROM exam_parameter WHERE exam_type_id = v_exam_type_id LIMIT 1;
    IF v_param_id IS NOT NULL THEN
        INSERT INTO exam_result (clinical_exam_id, parameter_id, value_numeric)
        VALUES (p_exam_id, v_param_id, p_vfi_value);
    END IF;
END $$
DELIMITER ;
```

### 19.

Crear un procedimiento para registrar una paquimetría.

```sql
DROP PROCEDURE IF EXISTS sp_register_pachymetry;
DELIMITER $$
CREATE PROCEDURE sp_register_pachymetry(
    IN p_visit_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_thickness DECIMAL(12,4),
    IN p_observations TEXT,
    OUT p_exam_id BIGINT
)
BEGIN
    DECLARE v_exam_type_id BIGINT;
    DECLARE v_param_id BIGINT;

    SELECT exam_type_id INTO v_exam_type_id FROM exam_type WHERE name LIKE '%Paquimetría%' LIMIT 1;

    INSERT INTO clinical_exam (visit_id, exam_type_id, professional_id, eye_id, exam_date, observations)
    VALUES (p_visit_id, v_exam_type_id, p_professional_id, p_eye_id, NOW(), p_observations);
    
    SET p_exam_id = LAST_INSERT_ID();

    SELECT parameter_id INTO v_param_id FROM exam_parameter WHERE exam_type_id = v_exam_type_id LIMIT 1;
    IF v_param_id IS NOT NULL THEN
        INSERT INTO exam_result (clinical_exam_id, parameter_id, value_numeric)
        VALUES (p_exam_id, v_param_id, p_thickness);
    END IF;
END $$
DELIMITER ;
```

### 20.

Crear un procedimiento para registrar un tratamiento.

```sql
DROP PROCEDURE IF EXISTS sp_register_treatment;
DELIMITER $$
CREATE PROCEDURE sp_register_treatment(
    IN p_visit_id BIGINT,
    IN p_treatment_status_id BIGINT,
    IN p_description TEXT,
    IN p_start_date DATE,
    IN p_end_date DATE,
    IN p_observations TEXT,
    OUT p_treatment_id BIGINT
)
BEGIN
    INSERT INTO treatment (visit_id, treatment_status_id, description, start_date, end_date, observations)
    VALUES (p_visit_id, p_treatment_status_id, p_description, p_start_date, p_end_date, p_observations);
    
    SET p_treatment_id = LAST_INSERT_ID();
END $$
DELIMITER ;
```

## Procedimientos de modificación

### 21.

Crear un procedimiento para actualizar teléfono y correo de un paciente.

```sql
DROP PROCEDURE IF EXISTS sp_update_patient_contact;
DELIMITER $$
CREATE PROCEDURE sp_update_patient_contact(
    IN p_patient_id BIGINT,
    IN p_phone VARCHAR(30),
    IN p_email VARCHAR(150)
)
BEGIN
    UPDATE person pe
    INNER JOIN patient pa ON pa.person_id = pe.person_id
    SET pe.phone = p_phone,
        pe.email = p_email
    WHERE pa.patient_id = p_patient_id;
END $$
DELIMITER ;
```

### 22.

Crear un procedimiento para modificar el estado de una historia clínica.

```sql
DROP PROCEDURE IF EXISTS sp_update_patient_status;
DELIMITER $$
CREATE PROCEDURE sp_update_patient_status(
    IN p_patient_id BIGINT,
    IN p_active BOOLEAN
)
BEGIN
    UPDATE patient
    SET active = p_active
    WHERE patient_id = p_patient_id;
END $$
DELIMITER ;
```

### 23.

Crear un procedimiento para actualizar observaciones de una consulta.

```sql
DROP PROCEDURE IF EXISTS sp_update_visit_observations;
DELIMITER $$
CREATE PROCEDURE sp_update_visit_observations(
    IN p_visit_id BIGINT,
    IN p_observations TEXT
)
BEGIN
    UPDATE medical_visit
    SET observations = p_observations
    WHERE visit_id = p_visit_id;
END $$
DELIMITER ;
```

### 24.

Crear un procedimiento para modificar la presión objetivo de un paciente con glaucoma.

```sql
DROP PROCEDURE IF EXISTS sp_update_glaucoma_target_pressure;
DELIMITER $$
CREATE PROCEDURE sp_update_glaucoma_target_pressure(
    IN p_glaucoma_record_id BIGINT,
    IN p_observations TEXT
)
BEGIN
    UPDATE glaucoma_record
    SET observations = p_observations
    WHERE glaucoma_record_id = p_glaucoma_record_id;
END $$
DELIMITER ;
```

### 25.

Crear un procedimiento para finalizar un tratamiento.

```sql
DROP PROCEDURE IF EXISTS sp_finalize_treatment;
DELIMITER $$
CREATE PROCEDURE sp_finalize_treatment(
    IN p_treatment_id BIGINT
)
BEGIN
    DECLARE v_status_id BIGINT;
    SELECT treatment_status_id INTO v_status_id FROM treatment_status WHERE name = 'Finalizado' LIMIT 1;

    UPDATE treatment
    SET treatment_status_id = v_status_id,
        end_date = CURDATE()
    WHERE treatment_id = p_treatment_id;
END $$
DELIMITER ;
```

### 26.

Crear un procedimiento para cambiar el medicamento de un tratamiento.

```sql
DROP PROCEDURE IF EXISTS sp_change_treatment_medication;
DELIMITER $$
CREATE PROCEDURE sp_change_treatment_medication(
    IN p_treatment_id BIGINT,
    IN p_old_medication_id BIGINT,
    IN p_new_medication_id BIGINT,
    IN p_dosage VARCHAR(100),
    IN p_frequency VARCHAR(100)
)
BEGIN
    DELETE FROM treatment_medication
    WHERE treatment_id = p_treatment_id AND medication_id = p_old_medication_id;

    INSERT INTO treatment_medication (treatment_id, medication_id, dosage, frequency)
    VALUES (p_treatment_id, p_new_medication_id, p_dosage, p_frequency);
END $$
DELIMITER ;
```

### 27.

Crear un procedimiento para actualizar el estado clínico del glaucoma.

```sql
DROP PROCEDURE IF EXISTS sp_update_glaucoma_status;
DELIMITER $$
CREATE PROCEDURE sp_update_glaucoma_status(
    IN p_glaucoma_record_id BIGINT,
    IN p_active BOOLEAN,
    IN p_observations TEXT
)
BEGIN
    UPDATE glaucoma_record
    SET active = p_active,
        observations = p_observations
    WHERE glaucoma_record_id = p_glaucoma_record_id;
END $$
DELIMITER ;
```

### 28.

Crear un procedimiento para actualizar información de un profesional.

```sql
DROP PROCEDURE IF EXISTS sp_update_professional_info;
DELIMITER $$
CREATE PROCEDURE sp_update_professional_info(
    IN p_professional_id BIGINT,
    IN p_license VARCHAR(50),
    IN p_phone VARCHAR(30),
    IN p_email VARCHAR(150)
)
BEGIN
    UPDATE healthcare_professional hp
    INNER JOIN person pe ON pe.person_id = hp.person_id
    SET hp.professional_license = p_license,
        pe.phone = p_phone,
        pe.email = p_email
    WHERE hp.professional_id = p_professional_id;
END $$
DELIMITER ;
```

### 29.

Crear un procedimiento para modificar la interpretación de un OCT.

```sql
DROP PROCEDURE IF EXISTS sp_update_oct_interpretation;
DELIMITER $$
CREATE PROCEDURE sp_update_oct_interpretation(
    IN p_clinical_exam_id BIGINT,
    IN p_observations TEXT
)
BEGIN
    UPDATE clinical_exam
    SET observations = p_observations
    WHERE clinical_exam_id = p_clinical_exam_id;
END $$
DELIMITER ;
```

### 30.

Crear un procedimiento para actualizar la interpretación de un campo visual.

```sql
DROP PROCEDURE IF EXISTS sp_update_visual_field_interpretation;
DELIMITER $$
CREATE PROCEDURE sp_update_visual_field_interpretation(
    IN p_clinical_exam_id BIGINT,
    IN p_observations TEXT
)
BEGIN
    UPDATE clinical_exam
    SET observations = p_observations
    WHERE clinical_exam_id = p_clinical_exam_id;
END $$
DELIMITER ;
```

## Procedimientos con validaciones

### 31.

Crear un procedimiento que registre una PIO únicamente si el paciente existe.

```sql
DROP PROCEDURE IF EXISTS sp_register_pio_if_patient_exists;
DELIMITER $$
CREATE PROCEDURE sp_register_pio_if_patient_exists(
    IN p_patient_id BIGINT,
    IN p_visit_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_pressure_value DECIMAL(6,2)
)
BEGIN
    IF EXISTS (SELECT 1 FROM patient WHERE patient_id = p_patient_id) THEN
        INSERT INTO intraocular_pressure (visit_id, eye_id, measured_at, pressure_value, unit)
        VALUES (p_visit_id, p_eye_id, NOW(), p_pressure_value, 'mmHg');
    ELSE
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El paciente especificado no existe';
    END IF;
END $$
DELIMITER ;
```

### 32.

Crear un procedimiento que registre una consulta solo si existe la historia clínica.

```sql
DROP PROCEDURE IF EXISTS sp_register_visit_if_history_exists;
DELIMITER $$
CREATE PROCEDURE sp_register_visit_if_history_exists(
    IN p_clinical_history_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_visit_type_id BIGINT,
    IN p_reason TEXT
)
BEGIN
    IF EXISTS (SELECT 1 FROM clinical_history WHERE clinical_history_id = p_clinical_history_id) THEN
        INSERT INTO medical_visit (clinical_history_id, professional_id, visit_type_id, visit_date, reason)
        VALUES (p_clinical_history_id, p_professional_id, p_visit_type_id, NOW(), p_reason);
    ELSE
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La historia clínica especificada no existe';
    END IF;
END $$
DELIMITER ;
```

### 33.

Crear un procedimiento que impida registrar un tratamiento con fecha final anterior a la inicial.

```sql
DROP PROCEDURE IF EXISTS sp_register_treatment_validated;
DELIMITER $$
CREATE PROCEDURE sp_register_treatment_validated(
    IN p_visit_id BIGINT,
    IN p_treatment_status_id BIGINT,
    IN p_description TEXT,
    IN p_start_date DATE,
    IN p_end_date DATE
)
BEGIN
    IF p_end_date IS NOT NULL AND p_end_date < p_start_date THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La fecha final no puede ser anterior a la inicial';
    ELSE
        INSERT INTO treatment (visit_id, treatment_status_id, description, start_date, end_date)
        VALUES (p_visit_id, p_treatment_status_id, p_description, p_start_date, p_end_date);
    END IF;
END $$
DELIMITER ;
```

### 34.

Crear un procedimiento que impida registrar valores negativos de PIO.

```sql
DROP PROCEDURE IF EXISTS sp_register_pio_positive;
DELIMITER $$
CREATE PROCEDURE sp_register_pio_positive(
    IN p_visit_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_pressure_value DECIMAL(6,2)
)
BEGIN
    IF p_pressure_value < 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La presión intraocular no puede ser negativa';
    ELSE
        INSERT INTO intraocular_pressure (visit_id, eye_id, measured_at, pressure_value, unit)
        VALUES (p_visit_id, p_eye_id, NOW(), p_pressure_value, 'mmHg');
    END IF;
END $$
DELIMITER ;
```

### 35.

Crear un procedimiento que valide que el ojo recibido sea OD u OI.

```sql
DROP PROCEDURE IF EXISTS sp_register_pio_validate_eye;
DELIMITER $$
CREATE PROCEDURE sp_register_pio_validate_eye(
    IN p_visit_id BIGINT,
    IN p_eye_code VARCHAR(20),
    IN p_pressure_value DECIMAL(6,2)
)
BEGIN
    DECLARE v_eye_id BIGINT;
    
    IF p_eye_code NOT IN ('OD', 'OI', 'OS') THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El ojo debe ser OD u OI';
    ELSE
        SELECT eye_id INTO v_eye_id FROM eye WHERE code = p_eye_code LIMIT 1;
        INSERT INTO intraocular_pressure (visit_id, eye_id, measured_at, pressure_value, unit)
        VALUES (p_visit_id, v_eye_id, NOW(), p_pressure_value, 'mmHg');
    END IF;
END $$
DELIMITER ;
```

### 36.

Crear un procedimiento que impida crear dos historias clínicas para el mismo paciente.

```sql
DROP PROCEDURE IF EXISTS sp_create_clinical_history_unique;
DELIMITER $$
CREATE PROCEDURE sp_create_clinical_history_unique(
    IN p_patient_id BIGINT,
    IN p_history_number VARCHAR(50)
)
BEGIN
    IF EXISTS (SELECT 1 FROM clinical_history WHERE patient_id = p_patient_id) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El paciente ya posee una historia clínica';
    ELSE
        INSERT INTO clinical_history (patient_id, history_number, created_at)
        VALUES (p_patient_id, p_history_number, NOW());
    END IF;
END $$
DELIMITER ;
```

### 37.

Crear un procedimiento que registre un diagnóstico solo si existe en el catálogo.

```sql
DROP PROCEDURE IF EXISTS sp_register_diagnosis_validated;
DELIMITER $$
CREATE PROCEDURE sp_register_diagnosis_validated(
    IN p_visit_id BIGINT,
    IN p_diagnosis_id BIGINT,
    IN p_diagnosis_type VARCHAR(50)
)
BEGIN
    IF EXISTS (SELECT 1 FROM diagnosis WHERE diagnosis_id = p_diagnosis_id) THEN
        INSERT INTO visit_diagnosis (visit_id, diagnosis_id, diagnosis_type)
        VALUES (p_visit_id, p_diagnosis_id, p_diagnosis_type);
    ELSE
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El diagnóstico no existe en el catálogo';
    END IF;
END $$
DELIMITER ;
```

### 38.

Crear un procedimiento que valide que el profesional se encuentre activo antes de registrar una consulta.

```sql
DROP PROCEDURE IF EXISTS sp_register_visit_active_prof;
DELIMITER $$
CREATE PROCEDURE sp_register_visit_active_prof(
    IN p_clinical_history_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_visit_type_id BIGINT,
    IN p_reason TEXT
)
BEGIN
    IF EXISTS (SELECT 1 FROM healthcare_professional WHERE professional_id = p_professional_id AND active = TRUE) THEN
        INSERT INTO medical_visit (clinical_history_id, professional_id, visit_type_id, visit_date, reason)
        VALUES (p_clinical_history_id, p_professional_id, p_visit_type_id, NOW(), p_reason);
    ELSE
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El profesional no existe o no se encuentra activo';
    END IF;
END $$
DELIMITER ;
```

### 39.

Crear un procedimiento que registre un campo visual validando que VFI esté entre 0 y 100.

```sql
DROP PROCEDURE IF EXISTS sp_register_visual_field_vfi_check;
DELIMITER $$
CREATE PROCEDURE sp_register_visual_field_vfi_check(
    IN p_visit_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_vfi DECIMAL(12,4)
)
BEGIN
    DECLARE v_exam_id BIGINT;
    DECLARE v_exam_type_id BIGINT;
    DECLARE v_param_id BIGINT;

    IF p_vfi < 0 OR p_vfi > 100 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El VFI debe estar entre 0 y 100';
    ELSE
        SELECT exam_type_id INTO v_exam_type_id FROM exam_type WHERE name LIKE '%Campo visual%' OR name LIKE '%Campimetría%' LIMIT 1;
        INSERT INTO clinical_exam (visit_id, exam_type_id, professional_id, eye_id, exam_date)
        VALUES (p_visit_id, v_exam_type_id, p_professional_id, p_eye_id, NOW());
        
        SET v_exam_id = LAST_INSERT_ID();
        SELECT parameter_id INTO v_param_id FROM exam_parameter WHERE exam_type_id = v_exam_type_id LIMIT 1;
        
        IF v_param_id IS NOT NULL THEN
            INSERT INTO exam_result (clinical_exam_id, parameter_id, value_numeric)
            VALUES (v_exam_id, v_param_id, p_vfi);
        END IF;
    END IF;
END $$
DELIMITER ;
```

### 40.

Crear un procedimiento que registre una paquimetría validando que el valor sea positivo.

```sql
DROP PROCEDURE IF EXISTS sp_register_pachymetry_positive;
DELIMITER $$
CREATE PROCEDURE sp_register_pachymetry_positive(
    IN p_visit_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_thickness DECIMAL(12,4)
)
BEGIN
    DECLARE v_exam_id BIGINT;
    DECLARE v_exam_type_id BIGINT;
    DECLARE v_param_id BIGINT;

    IF p_thickness <= 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El valor de paquimetría debe ser positivo';
    ELSE
        SELECT exam_type_id INTO v_exam_type_id FROM exam_type WHERE name LIKE '%Paquimetría%' LIMIT 1;
        INSERT INTO clinical_exam (visit_id, exam_type_id, professional_id, eye_id, exam_date)
        VALUES (p_visit_id, v_exam_type_id, p_professional_id, p_eye_id, NOW());
        
        SET v_exam_id = LAST_INSERT_ID();
        SELECT parameter_id INTO v_param_id FROM exam_parameter WHERE exam_type_id = v_exam_type_id LIMIT 1;
        
        IF v_param_id IS NOT NULL THEN
            INSERT INTO exam_result (clinical_exam_id, parameter_id, value_numeric)
            VALUES (v_exam_id, v_param_id, p_thickness);
        END IF;
    END IF;
END $$
DELIMITER ;
```

## Procedimientos avanzados

### 41.

Crear un procedimiento que devuelva un resumen completo de la historia clínica de un paciente.

```sql
DROP PROCEDURE IF EXISTS sp_get_patient_summary;
DELIMITER $$
CREATE PROCEDURE sp_get_patient_summary(
    IN p_patient_id BIGINT
)
BEGIN
    SELECT 
        p.patient_id,
        CONCAT(pe.first_name, ' ', pe.last_name) AS paciente,
        pe.identification_number AS documento,
        ch.history_number AS historia,
        COUNT(DISTINCT mv.visit_id) AS total_consultas,
        COUNT(DISTINCT gr.glaucoma_record_id) AS registros_glaucoma,
        AVG(iop.pressure_value) AS pio_promedio
    FROM patient p
    INNER JOIN person pe ON pe.person_id = p.person_id
    LEFT JOIN clinical_history ch ON ch.patient_id = p.patient_id
    LEFT JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
    LEFT JOIN glaucoma_record gr ON gr.patient_id = p.patient_id
    LEFT JOIN intraocular_pressure iop ON iop.visit_id = mv.visit_id
    WHERE p.patient_id = p_patient_id
    GROUP BY p.patient_id, pe.first_name, pe.last_name, pe.identification_number, ch.history_number;
END $$
DELIMITER ;
```

### 42.

Crear un procedimiento que muestre la evolución de PIO de un paciente entre dos fechas.

```sql
DROP PROCEDURE IF EXISTS sp_get_pio_evolution;
DELIMITER $$
CREATE PROCEDURE sp_get_pio_evolution(
    IN p_patient_id BIGINT,
    IN p_start_date DATETIME,
    IN p_end_date DATETIME
)
BEGIN
    SELECT 
        iop.measured_at,
        e.code AS eye,
        iop.pressure_value,
        iop.method
    FROM intraocular_pressure iop
    INNER JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    INNER JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    INNER JOIN eye e ON e.eye_id = iop.eye_id
    WHERE ch.patient_id = p_patient_id
      AND iop.measured_at BETWEEN p_start_date AND p_end_date
    ORDER BY iop.measured_at ASC;
END $$
DELIMITER ;
```

### 43.

Crear un procedimiento que reciba paciente y ojo y muestre todas sus mediciones cronológicamente.

```sql
DROP PROCEDURE IF EXISTS sp_get_patient_eye_pio;
DELIMITER $$
CREATE PROCEDURE sp_get_patient_eye_pio(
    IN p_patient_id BIGINT,
    IN p_eye_code VARCHAR(20)
)
BEGIN
    SELECT 
        iop.pressure_id,
        iop.measured_at,
        iop.pressure_value,
        iop.method
    FROM intraocular_pressure iop
    INNER JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    INNER JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    INNER JOIN eye e ON e.eye_id = iop.eye_id
    WHERE ch.patient_id = p_patient_id
      AND e.code = p_eye_code
    ORDER BY iop.measured_at ASC;
END $$
DELIMITER ;
```

### 44.

Crear un procedimiento que genere estadísticas mensuales de consultas.

```sql
DROP PROCEDURE IF EXISTS sp_get_monthly_visit_stats;
DELIMITER $$
CREATE PROCEDURE sp_get_monthly_visit_stats(
    IN p_year INT
)
BEGIN
    SELECT 
        MONTH(visit_date) AS mes,
        COUNT(*) AS total_consultas
    FROM medical_visit
    WHERE YEAR(visit_date) = p_year
    GROUP BY MONTH(visit_date)
    ORDER BY mes ASC;
END $$
DELIMITER ;
```

### 45.

Crear un procedimiento que calcule la cantidad de pacientes atendidos por cada especialista.

```sql
DROP PROCEDURE IF EXISTS sp_get_patients_per_specialist;
DELIMITER $$
CREATE PROCEDURE sp_get_patients_per_specialist()
BEGIN
    SELECT 
        hp.professional_id,
        CONCAT(pe.first_name, ' ', pe.last_name) AS profesional,
        COUNT(DISTINCT ch.patient_id) AS total_pacientes
    FROM healthcare_professional hp
    INNER JOIN person pe ON pe.person_id = hp.person_id
    LEFT JOIN medical_visit mv ON mv.professional_id = hp.professional_id
    LEFT JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    GROUP BY hp.professional_id, pe.first_name, pe.last_name;
END $$
DELIMITER ;
```

### 46.

Crear un procedimiento que determine pacientes sin consulta durante un número de meses recibido como parámetro.

```sql
DROP PROCEDURE IF EXISTS sp_get_inactive_patients_months;
DELIMITER $$
CREATE PROCEDURE sp_get_inactive_patients_months(
    IN p_months INT
)
BEGIN
    SELECT 
        p.patient_id,
        CONCAT(pe.first_name, ' ', pe.last_name) AS paciente,
        MAX(mv.visit_date) AS ultima_consulta
    FROM patient p
    INNER JOIN person pe ON pe.person_id = p.person_id
    INNER JOIN clinical_history ch ON ch.patient_id = p.patient_id
    LEFT JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
    GROUP BY p.patient_id, pe.first_name, pe.last_name
    HAVING MAX(mv.visit_date) < DATE_SUB(CURDATE(), INTERVAL p_months MONTH)
        OR MAX(mv.visit_date) IS NULL;
END $$
DELIMITER ;
```

### 47.

Crear un procedimiento que genere un resumen de diagnósticos por paciente.

```sql
DROP PROCEDURE IF EXISTS sp_get_diagnoses_summary_by_patient;
DELIMITER $$
CREATE PROCEDURE sp_get_diagnoses_summary_by_patient(
    IN p_patient_id BIGINT
)
BEGIN
    SELECT 
        d.code,
        d.name AS diagnostico,
        COUNT(*) AS frecuencia,
        MAX(mv.visit_date) AS ultima_vez
    FROM patient p
    INNER JOIN clinical_history ch ON ch.patient_id = p.patient_id
    INNER JOIN medical_visit mv ON mv.clinical_history_id = ch.clinical_history_id
    INNER JOIN visit_diagnosis vd ON vd.visit_id = mv.visit_id
    INNER JOIN diagnosis d ON d.diagnosis_id = vd.diagnosis_id
    WHERE p.patient_id = p_patient_id
    GROUP BY d.code, d.name;
END $$
DELIMITER ;
```

### 48.

Crear un procedimiento que devuelva el último OCT, último campo visual y última PIO de un paciente.

```sql
DROP PROCEDURE IF EXISTS sp_get_latest_exams_and_pio;
DELIMITER $$
CREATE PROCEDURE sp_get_latest_exams_and_pio(
    IN p_patient_id BIGINT
)
BEGIN
    SELECT 
        (SELECT MAX(ce.exam_date) 
         FROM clinical_exam ce 
         JOIN exam_type et ON et.exam_type_id = ce.exam_type_id 
         JOIN medical_visit mv ON mv.visit_id = ce.visit_id 
         JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id 
         WHERE ch.patient_id = p_patient_id AND et.name LIKE '%OCT%') AS ultimo_oct,
         
        (SELECT MAX(ce.exam_date) 
         FROM clinical_exam ce 
         JOIN exam_type et ON et.exam_type_id = ce.exam_type_id 
         JOIN medical_visit mv ON mv.visit_id = ce.visit_id 
         JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id 
         WHERE ch.patient_id = p_patient_id AND (et.name LIKE '%Campo visual%' OR et.name LIKE '%Campimetría%')) AS ultimo_campo_visual,
         
        (SELECT MAX(iop.measured_at) 
         FROM intraocular_pressure iop 
         JOIN medical_visit mv ON mv.visit_id = iop.visit_id 
         JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id 
         WHERE ch.patient_id = p_patient_id) AS ultima_pio;
END $$
DELIMITER ;
```

### 49.

Crear un procedimiento que registre en una sola transacción una consulta, un diagnóstico y una medición de PIO.

```sql
DROP PROCEDURE IF EXISTS sp_register_visit_diag_pio_tx;
DELIMITER $$
CREATE PROCEDURE sp_register_visit_diag_pio_tx(
    IN p_clinical_history_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_visit_type_id BIGINT,
    IN p_reason TEXT,
    IN p_diagnosis_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_pressure_value DECIMAL(6,2)
)
BEGIN
    DECLARE v_visit_id BIGINT;

    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL;
    END;

    START TRANSACTION;

    INSERT INTO medical_visit (clinical_history_id, professional_id, visit_type_id, visit_date, reason)
    VALUES (p_clinical_history_id, p_professional_id, p_visit_type_id, NOW(), p_reason);
    SET v_visit_id = LAST_INSERT_ID();

    INSERT INTO visit_diagnosis (visit_id, diagnosis_id, diagnosis_type)
    VALUES (v_visit_id, p_diagnosis_id, 'Principal');

    INSERT INTO intraocular_pressure (visit_id, eye_id, measured_at, pressure_value, unit)
    VALUES (v_visit_id, p_eye_id, NOW(), p_pressure_value, 'mmHg');

    COMMIT;
END $$
DELIMITER ;
```

### 50.

Crear un procedimiento transaccional que registre un control completo de glaucoma y ejecute ROLLBACK si alguna operación falla.

```sql
DROP PROCEDURE IF EXISTS sp_register_full_glaucoma_control_tx;
DELIMITER $$
CREATE PROCEDURE sp_register_full_glaucoma_control_tx(
    IN p_glaucoma_record_id BIGINT,
    IN p_clinical_history_id BIGINT,
    IN p_professional_id BIGINT,
    IN p_visit_type_id BIGINT,
    IN p_eye_id BIGINT,
    IN p_pressure_value DECIMAL(6,2),
    IN p_observations TEXT
)
BEGIN
    DECLARE v_visit_id BIGINT;

    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        ROLLBACK;
        RESIGNAL;
    END;

    START TRANSACTION;

    INSERT INTO medical_visit (clinical_history_id, professional_id, visit_type_id, visit_date, reason)
    VALUES (p_clinical_history_id, p_professional_id, p_visit_type_id, NOW(), 'Control Glaucoma');
    SET v_visit_id = LAST_INSERT_ID();

    INSERT INTO glaucoma_control (glaucoma_record_id, visit_id, control_date, observations)
    VALUES (p_glaucoma_record_id, v_visit_id, CURDATE(), p_observations);

    INSERT INTO intraocular_pressure (visit_id, eye_id, measured_at, pressure_value, unit)
    VALUES (v_visit_id, p_eye_id, NOW(), p_pressure_value, 'mmHg');

    COMMIT;
END $$
DELIMITER ;
```

# PARTE IV — 50 EJERCICIOS DE TRIGGERS

## Before insert

### 1.

Crear un trigger que elimine espacios externos de los nombres de pacientes antes de insertarlos.

```sql
DROP TRIGGER IF EXISTS trg_person_before_insert_trim;
DELIMITER $$
CREATE TRIGGER trg_person_before_insert_trim
BEFORE INSERT ON person
FOR EACH ROW
BEGIN
    SET NEW.first_name = TRIM(NEW.first_name);
    IF NEW.middle_name IS NOT NULL THEN
        SET NEW.middle_name = TRIM(NEW.middle_name);
    END IF;
    SET NEW.last_name = TRIM(NEW.last_name);
    IF NEW.second_last_name IS NOT NULL THEN
        SET NEW.second_last_name = TRIM(NEW.second_last_name);
    END IF;
END $$
DELIMITER ;
```

### 2.

Convertir automáticamente el correo del paciente a minúsculas.

```sql
DROP TRIGGER IF EXISTS trg_person_before_insert_email_lower;
DELIMITER $$
CREATE TRIGGER trg_person_before_insert_email_lower
BEFORE INSERT ON person
FOR EACH ROW
BEGIN
    IF NEW.email IS NOT NULL THEN
        SET NEW.email = LOWER(TRIM(NEW.email));
    END IF;
END $$
DELIMITER ;
```

### 3.

Convertir el número de documento a mayúsculas cuando contenga caracteres.

```sql
DROP TRIGGER IF EXISTS trg_person_before_insert_doc_upper;
DELIMITER $$
CREATE TRIGGER trg_person_before_insert_doc_upper
BEFORE INSERT ON person
FOR EACH ROW
BEGIN
    IF NEW.identification_number IS NOT NULL THEN
        SET NEW.identification_number = UPPER(TRIM(NEW.identification_number));
    END IF;
END $$
DELIMITER ;
```

### 4.

Impedir registrar una fecha de nacimiento futura.

```sql
DROP TRIGGER IF EXISTS trg_person_before_insert_birthdate;
DELIMITER $$
CREATE TRIGGER trg_person_before_insert_birthdate
BEFORE INSERT ON person
FOR EACH ROW
BEGIN
    IF NEW.birth_date > CURDATE() THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La fecha de nacimiento no puede ser futura';
    END IF;
END $$
DELIMITER ;
```

### 5.

Impedir registrar una presión intraocular negativa.

```sql
DROP TRIGGER IF EXISTS trg_iop_before_insert_negative;
DELIMITER $$
CREATE TRIGGER trg_iop_before_insert_negative
BEFORE INSERT ON intraocular_pressure
FOR EACH ROW
BEGIN
    IF NEW.pressure_value < 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La presión intraocular no puede ser negativa';
    END IF;
END $$
DELIMITER ;
```

### 6.

Impedir registrar una PIO superior a un límite definido para datos plausibles.

```sql
DROP TRIGGER IF EXISTS trg_iop_before_insert_limit;
DELIMITER $$
CREATE TRIGGER trg_iop_before_insert_limit
BEFORE INSERT ON intraocular_pressure
FOR EACH ROW
BEGIN
    IF NEW.pressure_value > 80 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La presión intraocular supera el límite plausible (80 mmHg)';
    END IF;
END $$
DELIMITER ;
```

### 7.

Validar que el campo eye solo admita OD u OI.

```sql
DROP TRIGGER IF EXISTS trg_iop_before_insert_eye_check;
DELIMITER $$
CREATE TRIGGER trg_iop_before_insert_eye_check
BEFORE INSERT ON intraocular_pressure
FOR EACH ROW
BEGIN
    DECLARE v_eye_code VARCHAR(20);
    SELECT code INTO v_eye_code FROM eye WHERE eye_id = NEW.eye_id;
    IF v_eye_code NOT IN ('OD', 'OI', 'OS') THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El ojo solo permite OD u OI';
    END IF;
END $$
DELIMITER ;
```

### 8.

Impedir que un tratamiento tenga fecha final anterior a la inicial.

```sql
DROP TRIGGER IF EXISTS trg_treatment_before_insert_dates;
DELIMITER $$
CREATE TRIGGER trg_treatment_before_insert_dates
BEFORE INSERT ON treatment
FOR EACH ROW
BEGIN
    IF NEW.end_date IS NOT NULL AND NEW.end_date < NEW.start_date THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La fecha final no puede ser anterior a la inicial';
    END IF;
END $$
DELIMITER ;
```

### 9.

Validar que el VFI de un campo visual esté entre 0 y 100.

```sql
DROP TRIGGER IF EXISTS trg_exam_result_before_insert_vfi;
DELIMITER $$
CREATE TRIGGER trg_exam_result_before_insert_vfi
BEFORE INSERT ON exam_result
FOR EACH ROW
BEGIN
    DECLARE v_exam_type_name VARCHAR(150);
    SELECT et.name INTO v_exam_type_name
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    WHERE ce.clinical_exam_id = NEW.clinical_exam_id;

    IF (v_exam_type_name LIKE '%Campo visual%' OR v_exam_type_name LIKE '%Campimetría%') THEN
        IF NEW.value_numeric < 0 OR NEW.value_numeric > 100 THEN
            SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El valor VFI debe estar entre 0 y 100';
        END IF;
    END IF;
END $$
DELIMITER ;
```

### 10.

Validar que la paquimetría sea mayor que cero.

```sql
DROP TRIGGER IF EXISTS trg_exam_result_before_insert_pachymetry;
DELIMITER $$
CREATE TRIGGER trg_exam_result_before_insert_pachymetry
BEFORE INSERT ON exam_result
FOR EACH ROW
BEGIN
    DECLARE v_exam_type_name VARCHAR(150);
    SELECT et.name INTO v_exam_type_name
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    WHERE ce.clinical_exam_id = NEW.clinical_exam_id;

    IF v_exam_type_name LIKE '%Paquimetría%' THEN
        IF NEW.value_numeric <= 0 THEN
            SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La paquimetría debe ser mayor a cero';
        END IF;
    END IF;
END $$
DELIMITER ;
```

## After insert

### 11.

Registrar en auditoría la creación de un nuevo paciente.

```sql
DROP TRIGGER IF EXISTS trg_patient_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_patient_after_insert_audit
AFTER INSERT ON patient
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'patient', NEW.patient_id, CONCAT('Nuevo paciente ID: ', NEW.patient_id));
END $$
DELIMITER ;
```

### 12.

Registrar en auditoría la creación de una historia clínica.

```sql
DROP TRIGGER IF EXISTS trg_history_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_history_after_insert_audit
AFTER INSERT ON clinical_history
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'clinical_history', NEW.clinical_history_id, CONCAT('Número: ', NEW.history_number));
END $$
DELIMITER ;
```

### 13.

Registrar automáticamente en auditoría cada nueva consulta.

```sql
DROP TRIGGER IF EXISTS trg_visit_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_visit_after_insert_audit
AFTER INSERT ON medical_visit
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'medical_visit', NEW.visit_id, CONCAT('Consulta fecha: ', NEW.visit_date));
END $$
DELIMITER ;
```

### 14.

Registrar cada nuevo diagnóstico asociado a una consulta.

```sql
DROP TRIGGER IF EXISTS trg_visit_diag_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_visit_diag_after_insert_audit
AFTER INSERT ON visit_diagnosis
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'visit_diagnosis', NEW.visit_id, CONCAT('Diag ID: ', NEW.diagnosis_id));
END $$
DELIMITER ;
```

### 15.

Registrar cada nueva medición de presión intraocular.

```sql
DROP TRIGGER IF EXISTS trg_iop_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_iop_after_insert_audit
AFTER INSERT ON intraocular_pressure
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'intraocular_pressure', NEW.pressure_id, CONCAT('Valor: ', NEW.pressure_value));
END $$
DELIMITER ;
```

### 16.

Registrar cada nuevo tratamiento.

```sql
DROP TRIGGER IF EXISTS trg_treatment_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_treatment_after_insert_audit
AFTER INSERT ON treatment
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'treatment', NEW.treatment_id, CONCAT('Tratamiento inicio: ', NEW.start_date));
END $$
DELIMITER ;
```

### 17.

Registrar cada nuevo procedimiento.

```sql
DROP TRIGGER IF EXISTS trg_procedure_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_procedure_after_insert_audit
AFTER INSERT ON visit_procedure
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'visit_procedure', NEW.visit_procedure_id, CONCAT('Proc ID: ', NEW.procedure_id));
END $$
DELIMITER ;
```

### 18.

Registrar en auditoría cada nuevo estudio OCT.

```sql
DROP TRIGGER IF EXISTS trg_oct_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_oct_after_insert_audit
AFTER INSERT ON clinical_exam
FOR EACH ROW
BEGIN
    DECLARE v_exam_type_name VARCHAR(150);
    SELECT name INTO v_exam_type_name FROM exam_type WHERE exam_type_id = NEW.exam_type_id;
    IF v_exam_type_name LIKE '%OCT%' THEN
        INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
        VALUES (1, 'INSERT', 'clinical_exam_oct', NEW.clinical_exam_id, 'Nuevo examen OCT');
    END IF;
END $$
DELIMITER ;
```

### 19.

Registrar cada campo visual creado.

```sql
DROP TRIGGER IF EXISTS trg_visual_field_after_insert_audit;
DELIMITER $$
CREATE TRIGGER trg_visual_field_after_insert_audit
AFTER INSERT ON clinical_exam
FOR EACH ROW
BEGIN
    DECLARE v_exam_type_name VARCHAR(150);
    SELECT name INTO v_exam_type_name FROM exam_type WHERE exam_type_id = NEW.exam_type_id;
    IF v_exam_type_name LIKE '%Campo visual%' OR v_exam_type_name LIKE '%Campimetría%' THEN
        INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
        VALUES (1, 'INSERT', 'clinical_exam_vf', NEW.clinical_exam_id, 'Nuevo Campo Visual');
    END IF;
END $$
DELIMITER ;
```

### 20.

Crear una notificación interna cuando se registre una PIO mayor que un valor determinado.

```sql
DROP TRIGGER IF EXISTS trg_iop_high_alert;
DELIMITER $$
CREATE TRIGGER trg_iop_high_alert
AFTER INSERT ON intraocular_pressure
FOR EACH ROW
BEGIN
    DECLARE v_patient_id BIGINT;
    IF NEW.pressure_value > 21 THEN
        SELECT ch.patient_id INTO v_patient_id
        FROM medical_visit mv
        JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
        WHERE mv.visit_id = NEW.visit_id;

        INSERT INTO alert (patient_id, created_by, visit_id, title, message, alert_type)
        VALUES (v_patient_id, 1, NEW.visit_id, 'PIO ELEVADA', CONCAT('Presión intraocular elevada: ', NEW.pressure_value, ' mmHg'), 'ALERTA');
    END IF;
END $$
DELIMITER ;
```

## Before update

### 21.

Actualizar automáticamente updated_at antes de modificar un paciente.

```sql
DROP TRIGGER IF EXISTS trg_ch_before_update_timestamp;
DELIMITER $$
CREATE TRIGGER trg_ch_before_update_timestamp
BEFORE UPDATE ON clinical_history
FOR EACH ROW
BEGIN
    SET NEW.updated_at = NOW();
END $$
DELIMITER ;
```

### 22.

Actualizar updated_at antes de modificar una consulta.

```sql
DROP TRIGGER IF EXISTS trg_visit_before_update_timestamp;
DELIMITER $$
CREATE TRIGGER trg_visit_before_update_timestamp
BEFORE UPDATE ON medical_visit
FOR EACH ROW
BEGIN
    SET NEW.visit_date = NEW.visit_date;
END $$
DELIMITER ;
```

### 23.

Impedir modificar el número de documento una vez creada la historia clínica.

```sql
DROP TRIGGER IF EXISTS trg_person_before_update_doc;
DELIMITER $$
CREATE TRIGGER trg_person_before_update_doc
BEFORE UPDATE ON person
FOR EACH ROW
BEGIN
    IF OLD.identification_number <> NEW.identification_number THEN
        IF EXISTS (
            SELECT 1 FROM patient p
            JOIN clinical_history ch ON ch.patient_id = p.patient_id
            WHERE p.person_id = OLD.person_id
        ) THEN
            SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se puede modificar el documento de un paciente con historia clínica';
        END IF;
    END IF;
END $$
DELIMITER ;
```

### 24.

Impedir asignar una fecha de consulta futura no permitida.

```sql
DROP TRIGGER IF EXISTS trg_visit_before_update_date;
DELIMITER $$
CREATE TRIGGER trg_visit_before_update_date
BEFORE UPDATE ON medical_visit
FOR EACH ROW
BEGIN
    IF NEW.visit_date > NOW() THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se permiten fechas futuras para consultas';
    END IF;
END $$
DELIMITER ;
```

### 25.

Validar que una nueva presión objetivo sea positiva.

```sql
DROP TRIGGER IF EXISTS trg_glaucoma_before_update_target;
DELIMITER $$
CREATE TRIGGER trg_glaucoma_before_update_target
BEFORE UPDATE ON glaucoma_record
FOR EACH ROW
BEGIN
    IF NEW.observations LIKE '%objetivo:%' AND NEW.observations LIKE '%-%' THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La presión objetivo debe ser positiva';
    END IF;
END $$
DELIMITER ;
```

### 26.

Impedir establecer una fecha final de tratamiento anterior a su inicio.

```sql
DROP TRIGGER IF EXISTS trg_treatment_before_update_dates;
DELIMITER $$
CREATE TRIGGER trg_treatment_before_update_dates
BEFORE UPDATE ON treatment
FOR EACH ROW
BEGIN
    IF NEW.end_date IS NOT NULL AND NEW.end_date < NEW.start_date THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'La fecha final no puede ser anterior al inicio';
    END IF;
END $$
DELIMITER ;
```

### 27.

Evitar modificar un examen OCT que haya sido marcado como validado.

```sql
DROP TRIGGER IF EXISTS trg_exam_before_update_validated;
DELIMITER $$
CREATE TRIGGER trg_exam_before_update_validated
BEFORE UPDATE ON clinical_exam
FOR EACH ROW
BEGIN
    IF OLD.observations LIKE '%VALIDADO%' THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se puede modificar un examen marcado como VALIDADO';
    END IF;
END $$
DELIMITER ;
```

### 28.

Evitar modificar una consulta marcada como cerrada.

```sql
DROP TRIGGER IF EXISTS trg_visit_before_update_closed;
DELIMITER $$
CREATE TRIGGER trg_visit_before_update_closed
BEFORE UPDATE ON medical_visit
FOR EACH ROW
BEGIN
    IF OLD.observations LIKE '%CERRADA%' THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se puede modificar una consulta cerrada';
    END IF;
END $$
DELIMITER ;
```

### 29.

Validar valores del campo visual antes de una actualización.

```sql
DROP TRIGGER IF EXISTS trg_exam_result_before_update_vf;
DELIMITER $$
CREATE TRIGGER trg_exam_result_before_update_vf
BEFORE UPDATE ON exam_result
FOR EACH ROW
BEGIN
    IF NEW.value_numeric < 0 OR NEW.value_numeric > 100 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El valor del examen no es válido';
    END IF;
END $$
DELIMITER ;
```

### 30.

Normalizar observaciones eliminando espacios innecesarios antes de actualizar.

```sql
DROP TRIGGER IF EXISTS trg_visit_before_update_trim_obs;
DELIMITER $$
CREATE TRIGGER trg_visit_before_update_trim_obs
BEFORE UPDATE ON medical_visit
FOR EACH ROW
BEGIN
    IF NEW.observations IS NOT NULL THEN
        SET NEW.observations = TRIM(NEW.observations);
    END IF;
END $$
DELIMITER ;
```

## After update

### 31.

Registrar cambios de datos personales del paciente.

```sql
DROP TRIGGER IF EXISTS trg_person_after_update_audit;
DELIMITER $$
CREATE TRIGGER trg_person_after_update_audit
AFTER UPDATE ON person
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE', 'person', NEW.person_id,
            CONCAT('Tel: ', OLD.phone, ' Email: ', OLD.email),
            CONCAT('Tel: ', NEW.phone, ' Email: ', NEW.email));
END $$
DELIMITER ;
```

### 32.

Guardar valor anterior y nuevo del correo del paciente.

```sql
DROP TRIGGER IF EXISTS trg_person_after_update_email;
DELIMITER $$
CREATE TRIGGER trg_person_after_update_email
AFTER UPDATE ON person
FOR EACH ROW
BEGIN
    IF OLD.email <> NEW.email OR (OLD.email IS NULL AND NEW.email IS NOT NULL) THEN
        INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
        VALUES (1, 'UPDATE_EMAIL', 'person', NEW.person_id, OLD.email, NEW.email);
    END IF;
END $$
DELIMITER ;
```

### 33.

Registrar cambios en la presión objetivo.

```sql
DROP TRIGGER IF EXISTS trg_glaucoma_after_update_target;
DELIMITER $$
CREATE TRIGGER trg_glaucoma_after_update_target
AFTER UPDATE ON glaucoma_record
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE_GLAUCOMA', 'glaucoma_record', NEW.glaucoma_record_id, OLD.observations, NEW.observations);
END $$
DELIMITER ;
```

### 34.

Auditar cambios en el estado del glaucoma.

```sql
DROP TRIGGER IF EXISTS trg_glaucoma_after_update_status;
DELIMITER $$
CREATE TRIGGER trg_glaucoma_after_update_status
AFTER UPDATE ON glaucoma_record
FOR EACH ROW
BEGIN
    IF OLD.active <> NEW.active THEN
        INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
        VALUES (1, 'UPDATE_STATUS', 'glaucoma_record', NEW.glaucoma_record_id, CONCAT('Active: ', OLD.active), CONCAT('Active: ', NEW.active));
    END IF;
END $$
DELIMITER ;
```

### 35.

Registrar cambios en tratamientos.

```sql
DROP TRIGGER IF EXISTS trg_treatment_after_update_audit;
DELIMITER $$
CREATE TRIGGER trg_treatment_after_update_audit
AFTER UPDATE ON treatment
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE', 'treatment', NEW.treatment_id, OLD.description, NEW.description);
END $$
DELIMITER ;
```

### 36.

Registrar cambios en diagnósticos.

```sql
DROP TRIGGER IF EXISTS trg_diagnosis_after_update_audit;
DELIMITER $$
CREATE TRIGGER trg_diagnosis_after_update_audit
AFTER UPDATE ON diagnosis
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE', 'diagnosis', NEW.diagnosis_id, OLD.name, NEW.name);
END $$
DELIMITER ;
```

### 37.

Registrar cambios de interpretación de OCT.

```sql
DROP TRIGGER IF EXISTS trg_oct_after_update_interp;
DELIMITER $$
CREATE TRIGGER trg_oct_after_update_interp
AFTER UPDATE ON clinical_exam
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE_OCT', 'clinical_exam', NEW.clinical_exam_id, OLD.observations, NEW.observations);
END $$
DELIMITER ;
```

### 38.

Registrar modificaciones de campos visuales.

```sql
DROP TRIGGER IF EXISTS trg_vf_after_update_audit;
DELIMITER $$
CREATE TRIGGER trg_vf_after_update_audit
AFTER UPDATE ON exam_result
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE_RESULT', 'exam_result', NEW.clinical_exam_id,
            CONCAT('Old: ', OLD.value_numeric), CONCAT('New: ', NEW.value_numeric));
END $$
DELIMITER ;
```

### 39.

Generar una alerta cuando una PIO sea actualizada a un valor superior al objetivo.

```sql
DROP TRIGGER IF EXISTS trg_iop_after_update_alert;
DELIMITER $$
CREATE TRIGGER trg_iop_after_update_alert
AFTER UPDATE ON intraocular_pressure
FOR EACH ROW
BEGIN
    IF NEW.pressure_value > 21 THEN
        INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
        VALUES (1, 'ALERTA_PIO_UPDATE', 'intraocular_pressure', NEW.pressure_id, CONCAT('PIO actualizada superior al objetivo: ', NEW.pressure_value));
    END IF;
END $$
DELIMITER ;
```

### 40.

Registrar cuándo un tratamiento cambia de activo a finalizado.

```sql
DROP TRIGGER IF EXISTS trg_treatment_after_update_status;
DELIMITER $$
CREATE TRIGGER trg_treatment_after_update_status
AFTER UPDATE ON treatment
FOR EACH ROW
BEGIN
    IF OLD.treatment_status_id <> NEW.treatment_status_id THEN
        INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
        VALUES (1, 'STATUS_CHANGE', 'treatment', NEW.treatment_id,
                CONCAT('Old Status: ', OLD.treatment_status_id),
                CONCAT('New Status: ', NEW.treatment_status_id));
    END IF;
END $$
DELIMITER ;
```

## Delete y auditoría

### 41.

Guardar una copia de un paciente antes de eliminarlo.

```sql
DROP TRIGGER IF EXISTS trg_patient_before_delete_copy;
DELIMITER $$
CREATE TRIGGER trg_patient_before_delete_copy
BEFORE DELETE ON patient
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE', 'patient', OLD.patient_id, CONCAT('Person ID: ', OLD.person_id));
END $$
DELIMITER ;
```

### 42.

Guardar una copia de una consulta eliminada.

```sql
DROP TRIGGER IF EXISTS trg_visit_before_delete_copy;
DELIMITER $$
CREATE TRIGGER trg_visit_before_delete_copy
BEFORE DELETE ON medical_visit
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE', 'medical_visit', OLD.visit_id, CONCAT('Fecha: ', OLD.visit_date, ' Motivo: ', OLD.reason));
END $$
DELIMITER ;
```

### 43.

Guardar un histórico de un tratamiento eliminado.

```sql
DROP TRIGGER IF EXISTS trg_treatment_before_delete_history;
DELIMITER $$
CREATE TRIGGER trg_treatment_before_delete_history
BEFORE DELETE ON treatment
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE', 'treatment', OLD.treatment_id, CONCAT('Desc: ', OLD.description));
END $$
DELIMITER ;
```

### 44.

Registrar en auditoría la eliminación de un diagnóstico.

```sql
DROP TRIGGER IF EXISTS trg_diagnosis_before_delete_audit;
DELIMITER $$
CREATE TRIGGER trg_diagnosis_before_delete_audit
BEFORE DELETE ON diagnosis
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE', 'diagnosis', OLD.diagnosis_id, CONCAT('Code: ', OLD.code, ' Name: ', OLD.name));
END $$
DELIMITER ;
```

### 45.

Impedir eliminar pacientes que tengan historia clínica.

```sql
DROP TRIGGER IF EXISTS trg_patient_before_delete_check;
DELIMITER $$
CREATE TRIGGER trg_patient_before_delete_check
BEFORE DELETE ON patient
FOR EACH ROW
BEGIN
    IF EXISTS (SELECT 1 FROM clinical_history WHERE patient_id = OLD.patient_id) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se puede eliminar un paciente que posee historia clínica';
    END IF;
END $$
DELIMITER ;
```

### 46.

Impedir eliminar profesionales con consultas registradas.

```sql
DROP TRIGGER IF EXISTS trg_prof_before_delete_check;
DELIMITER $$
CREATE TRIGGER trg_prof_before_delete_check
BEFORE DELETE ON healthcare_professional
FOR EACH ROW
BEGIN
    IF EXISTS (SELECT 1 FROM medical_visit WHERE professional_id = OLD.professional_id) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se puede eliminar un profesional con consultas asociadas';
    END IF;
END $$
DELIMITER ;
```

### 47.

Impedir eliminar medicamentos actualmente utilizados en tratamientos activos.

```sql
DROP TRIGGER IF EXISTS trg_medication_before_delete_check;
DELIMITER $$
CREATE TRIGGER trg_medication_before_delete_check
BEFORE DELETE ON medication
FOR EACH ROW
BEGIN
    IF EXISTS (
        SELECT 1 FROM treatment_medication tm
        JOIN treatment t ON t.treatment_id = tm.treatment_id
        JOIN treatment_status ts ON ts.treatment_status_id = t.treatment_status_id
        WHERE tm.medication_id = OLD.medication_id AND ts.name = 'Activo'
    ) THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'No se puede eliminar un medicamento asociado a un tratamiento activo';
    END IF;
END $$
DELIMITER ;
```

### 48.

Registrar automáticamente la eliminación de un examen OCT.

```sql
DROP TRIGGER IF EXISTS trg_oct_before_delete_audit;
DELIMITER $$
CREATE TRIGGER trg_oct_before_delete_audit
BEFORE DELETE ON clinical_exam
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE', 'clinical_exam', OLD.clinical_exam_id, CONCAT('Examen eliminado fecha: ', OLD.exam_date));
END $$
DELIMITER ;
```

### 49.

Registrar quién eliminó un documento clínico.

```sql
DROP TRIGGER IF EXISTS trg_document_before_delete_audit;
DELIMITER $$
CREATE TRIGGER trg_document_before_delete_audit
BEFORE DELETE ON clinical_document
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE_DOC', 'clinical_document', OLD.document_id, CONCAT('Documento: ', OLD.file_name));
END $$
DELIMITER ;
```

### 50.

Implementar un esquema completo de auditoría mediante triggers para INSERT, UPDATE y DELETE sobre la tabla patients.

```sql
DROP TRIGGER IF EXISTS trg_patient_audit_insert;
DELIMITER $$
CREATE TRIGGER trg_patient_audit_insert
AFTER INSERT ON patient
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, new_values)
    VALUES (1, 'INSERT', 'patient', NEW.patient_id, CONCAT('Ingreso: ', NEW.admission_date));
END $$
DELIMITER ;

DROP TRIGGER IF EXISTS trg_patient_audit_update;
DELIMITER $$
CREATE TRIGGER trg_patient_audit_update
AFTER UPDATE ON patient
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values, new_values)
    VALUES (1, 'UPDATE', 'patient', NEW.patient_id,
            CONCAT('Active: ', OLD.active),
            CONCAT('Active: ', NEW.active));
END $$
DELIMITER ;

DROP TRIGGER IF EXISTS trg_patient_audit_delete;
DELIMITER $$
CREATE TRIGGER trg_patient_audit_delete
BEFORE DELETE ON patient
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (user_id, action, table_name, record_id, old_values)
    VALUES (1, 'DELETE', 'patient', OLD.patient_id, CONCAT('Person ID: ', OLD.person_id));
END $$
DELIMITER ;
```

# PARTE V — 50 EJERCICIOS DE FUNCIONES ALMACENADAS

## Funciones básicas

### 1.

Crear una función que calcule la edad de un paciente a partir de su fecha de nacimiento.

```sql
DROP FUNCTION IF EXISTS fn_calculate_age;
DELIMITER $$
CREATE FUNCTION fn_calculate_age(
    p_birth_date DATE
)
RETURNS INT
DETERMINISTIC
BEGIN
    IF p_birth_date IS NULL THEN
        RETURN NULL;
    END IF;
    RETURN TIMESTAMPDIFF(YEAR, p_birth_date, CURDATE());
END $$
DELIMITER ;
```

### 2.

Crear una función que reciba nombres y apellidos y retorne el nombre completo.

```sql
DROP FUNCTION IF EXISTS fn_get_full_name;
DELIMITER $$
CREATE FUNCTION fn_get_full_name(
    p_first_name VARCHAR(100),
    p_middle_name VARCHAR(100),
    p_last_name VARCHAR(100),
    p_second_last_name VARCHAR(100)
)
RETURNS VARCHAR(400)
DETERMINISTIC
BEGIN
    RETURN CONCAT(
        p_first_name, ' ',
        IFNULL(CONCAT(p_middle_name, ' '), ''),
        p_last_name,
        IFNULL(CONCAT(' ', p_second_last_name), '')
    );
END $$
DELIMITER ;
```

### 3.

Crear una función que reciba un ID de paciente y retorne su número de documento.

```sql
DROP FUNCTION IF EXISTS fn_get_patient_document;
DELIMITER $$
CREATE FUNCTION fn_get_patient_document(
    p_patient_id BIGINT
)
RETURNS VARCHAR(50)
READS SQL DATA
BEGIN
    DECLARE v_doc VARCHAR(50);
    SELECT pe.identification_number INTO v_doc
    FROM patient pa
    JOIN person pe ON pe.person_id = pa.person_id
    WHERE pa.patient_id = p_patient_id;
    RETURN v_doc;
END $$
DELIMITER ;
```

### 4.

Crear una función que reciba un ID de paciente y retorne su edad.

```sql
DROP FUNCTION IF EXISTS fn_get_patient_age;
DELIMITER $$
CREATE FUNCTION fn_get_patient_age(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_age INT;
    SELECT TIMESTAMPDIFF(YEAR, pe.birth_date, CURDATE()) INTO v_age
    FROM patient pa
    JOIN person pe ON pe.person_id = pa.person_id
    WHERE pa.patient_id = p_patient_id;
    RETURN v_age;
END $$
DELIMITER ;
```

### 5.

Crear una función que reciba el ID de una consulta y retorne su fecha.

```sql
DROP FUNCTION IF EXISTS fn_get_visit_date;
DELIMITER $$
CREATE FUNCTION fn_get_visit_date(
    p_visit_id BIGINT
)
RETURNS DATETIME
READS SQL DATA
BEGIN
    DECLARE v_date DATETIME;
    SELECT visit_date INTO v_date FROM medical_visit WHERE visit_id = p_visit_id;
    RETURN v_date;
END $$
DELIMITER ;
```

### 6.

Crear una función que determine cuántos años han pasado desde una fecha.

```sql
DROP FUNCTION IF EXISTS fn_years_since;
DELIMITER $$
CREATE FUNCTION fn_years_since(
    p_date DATE
)
RETURNS INT
DETERMINISTIC
BEGIN
    IF p_date IS NULL THEN
        RETURN 0;
    END IF;
    RETURN TIMESTAMPDIFF(YEAR, p_date, CURDATE());
END $$
DELIMITER ;
```

### 7.

Crear una función que reciba un valor de PIO y retorne un texto descriptivo.

```sql
DROP FUNCTION IF EXISTS fn_describe_pio;
DELIMITER $$
CREATE FUNCTION fn_describe_pio(
    p_value DECIMAL(6,2)
)
RETURNS VARCHAR(50)
DETERMINISTIC
BEGIN
    IF p_value IS NULL THEN RETURN 'Sin datos';
    ELSEIF p_value < 10 THEN RETURN 'Hipotonía';
    ELSEIF p_value <= 21 THEN RETURN 'Normal';
    ELSE RETURN 'Elevada';
    END IF;
END $$
DELIMITER ;
```

### 8.

Crear una función que reciba OD u OI y devuelva Ojo derecho u Ojo izquierdo.

```sql
DROP FUNCTION IF EXISTS fn_get_eye_description;
DELIMITER $$
CREATE FUNCTION fn_get_eye_description(
    p_code VARCHAR(20)
)
RETURNS VARCHAR(50)
DETERMINISTIC
BEGIN
    IF p_code = 'OD' THEN RETURN 'Ojo derecho';
    ELSEIF p_code IN ('OI', 'OS') THEN RETURN 'Ojo izquierdo';
    ELSEIF p_code = 'OU' THEN RETURN 'Ambos ojos';
    ELSE RETURN 'Desconocido';
    END IF;
END $$
DELIMITER ;
```

### 9.

Crear una función que reciba un booleano y retorne Activo o Inactivo.

```sql
DROP FUNCTION IF EXISTS fn_boolean_to_status;
DELIMITER $$
CREATE FUNCTION fn_boolean_to_status(
    p_active BOOLEAN
)
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
    IF p_active IS TRUE THEN RETURN 'Activo';
    ELSE RETURN 'Inactivo';
    END IF;
END $$
DELIMITER ;
```

### 10.

Crear una función que formatee un número de historia clínica.

```sql
DROP FUNCTION IF EXISTS fn_format_history_number;
DELIMITER $$
CREATE FUNCTION fn_format_history_number(
    p_number INT
)
RETURNS VARCHAR(50)
DETERMINISTIC
BEGIN
    RETURN CONCAT('HC-', LPAD(p_number, 6, '0'));
END $$
DELIMITER ;
```

## Funciones con consultas

### 11.

Crear una función que retorne la cantidad de consultas de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_count_patient_visits;
DELIMITER $$
CREATE FUNCTION fn_count_patient_visits(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(mv.visit_id) INTO v_count
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

### 12.

Crear una función que retorne la cantidad de diagnósticos de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_count_patient_diagnoses;
DELIMITER $$
CREATE FUNCTION fn_count_patient_diagnoses(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(vd.diagnosis_id) INTO v_count
    FROM visit_diagnosis vd
    JOIN medical_visit mv ON mv.visit_id = vd.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

### 13.

Crear una función que retorne la cantidad de controles de glaucoma de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_count_glaucoma_controls;
DELIMITER $$
CREATE FUNCTION fn_count_glaucoma_controls(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(gc.glaucoma_control_id) INTO v_count
    FROM glaucoma_control gc
    JOIN glaucoma_record gr ON gr.glaucoma_record_id = gc.glaucoma_record_id
    WHERE gr.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

### 14.

Crear una función que retorne la última fecha de consulta.

```sql
DROP FUNCTION IF EXISTS fn_get_last_visit_date;
DELIMITER $$
CREATE FUNCTION fn_get_last_visit_date(
    p_patient_id BIGINT
)
RETURNS DATETIME
READS SQL DATA
BEGIN
    DECLARE v_date DATETIME;
    SELECT MAX(mv.visit_date) INTO v_date
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN v_date;
END $$
DELIMITER ;
```

### 15.

Crear una función que retorne la primera fecha de consulta.

```sql
DROP FUNCTION IF EXISTS fn_get_first_visit_date;
DELIMITER $$
CREATE FUNCTION fn_get_first_visit_date(
    p_patient_id BIGINT
)
RETURNS DATETIME
READS SQL DATA
BEGIN
    DECLARE v_date DATETIME;
    SELECT MIN(mv.visit_date) INTO v_date
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN v_date;
END $$
DELIMITER ;
```

### 16.

Crear una función que retorne la presión intraocular promedio de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_pio;
DELIMITER $$
CREATE FUNCTION fn_get_avg_pio(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(6,2);
    SELECT AVG(iop.pressure_value) INTO v_avg
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN v_avg;
END $$
DELIMITER ;
```

### 17.

Crear una función que retorne la presión promedio de OD.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_pio_od;
DELIMITER $$
CREATE FUNCTION fn_get_avg_pio_od(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(6,2);
    SELECT AVG(iop.pressure_value) INTO v_avg
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    JOIN eye e ON e.eye_id = iop.eye_id
    WHERE ch.patient_id = p_patient_id AND e.code = 'OD';
    RETURN v_avg;
END $$
DELIMITER ;
```

### 18.

Crear una función que retorne la presión promedio de OI.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_pio_oi;
DELIMITER $$
CREATE FUNCTION fn_get_avg_pio_oi(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(6,2);
    SELECT AVG(iop.pressure_value) INTO v_avg
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    JOIN eye e ON e.eye_id = iop.eye_id
    WHERE ch.patient_id = p_patient_id AND e.code IN ('OI', 'OS');
    RETURN v_avg;
END $$
DELIMITER ;
```

### 19.

Crear una función que retorne la PIO máxima registrada para un paciente.

```sql
DROP FUNCTION IF EXISTS fn_get_max_pio;
DELIMITER $$
CREATE FUNCTION fn_get_max_pio(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_max DECIMAL(6,2);
    SELECT MAX(iop.pressure_value) INTO v_max
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN v_max;
END $$
DELIMITER ;
```

### 20.

Crear una función que retorne la PIO mínima registrada.

```sql
DROP FUNCTION IF EXISTS fn_get_min_pio;
DELIMITER $$
CREATE FUNCTION fn_get_min_pio(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_min DECIMAL(6,2);
    SELECT MIN(iop.pressure_value) INTO v_min
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN v_min;
END $$
DELIMITER ;
```

## Funciones clínicas y de clasificación

### 21.

Crear una función que clasifique una PIO según rangos definidos para fines académicos.

```sql
DROP FUNCTION IF EXISTS fn_classify_pio;
DELIMITER $$
CREATE FUNCTION fn_classify_pio(
    p_pio DECIMAL(6,2)
)
RETURNS VARCHAR(50)
DETERMINISTIC
BEGIN
    IF p_pio IS NULL THEN RETURN 'No registrado';
    ELSEIF p_pio < 10 THEN RETURN 'Baja / Hipotonía';
    ELSEIF p_pio <= 21 THEN RETURN 'Rango Normal';
    ELSEIF p_pio <= 29 THEN RETURN 'Sospechosa / Moderada';
    ELSE RETURN 'Severamente Elevada';
    END IF;
END $$
DELIMITER ;
```

### 22.

Crear una función que indique si una PIO supera una presión objetivo recibida como parámetro.

```sql
DROP FUNCTION IF EXISTS fn_is_pio_above_target;
DELIMITER $$
CREATE FUNCTION fn_is_pio_above_target(
    p_pio DECIMAL(6,2),
    p_target DECIMAL(6,2)
)
RETURNS BOOLEAN
DETERMINISTIC
BEGIN
    IF p_pio > p_target THEN
        RETURN TRUE;
    ELSE
        RETURN FALSE;
    END IF;
END $$
DELIMITER ;
```

### 23.

Crear una función que determine si un paciente tiene diagnóstico de glaucoma.

```sql
DROP FUNCTION IF EXISTS fn_has_glaucoma;
DELIMITER $$
CREATE FUNCTION fn_has_glaucoma(
    p_patient_id BIGINT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    IF EXISTS (SELECT 1 FROM glaucoma_record WHERE patient_id = p_patient_id AND active = TRUE) THEN
        RETURN TRUE;
    ELSE
        RETURN FALSE;
    END IF;
END $$
DELIMITER ;
```

### 24.

Crear una función que determine si un paciente tiene tratamientos activos.

```sql
DROP FUNCTION IF EXISTS fn_has_active_treatments;
DELIMITER $$
CREATE FUNCTION fn_has_active_treatments(
    p_patient_id BIGINT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(t.treatment_id) INTO v_count
    FROM treatment t
    JOIN treatment_status ts ON ts.treatment_status_id = t.treatment_status_id
    JOIN medical_visit mv ON mv.visit_id = t.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND ts.name = 'Activo';

    RETURN IF(v_count > 0, TRUE, FALSE);
END $$
DELIMITER ;
```

### 25.

Crear una función que indique si el paciente tiene al menos un OCT registrado.

```sql
DROP FUNCTION IF EXISTS fn_has_oct;
DELIMITER $$
CREATE FUNCTION fn_has_oct(
    p_patient_id BIGINT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(ce.clinical_exam_id) INTO v_count
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND et.name LIKE '%OCT%';

    RETURN IF(v_count > 0, TRUE, FALSE);
END $$
DELIMITER ;
```

### 26.

Crear una función que indique si tiene campo visual registrado.

```sql
DROP FUNCTION IF EXISTS fn_has_visual_field;
DELIMITER $$
CREATE FUNCTION fn_has_visual_field(
    p_patient_id BIGINT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(ce.clinical_exam_id) INTO v_count
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND (et.name LIKE '%Campo visual%' OR et.name LIKE '%Campimetría%');

    RETURN IF(v_count > 0, TRUE, FALSE);
END $$
DELIMITER ;
```

### 27.

Crear una función que determine si tiene paquimetría.

```sql
DROP FUNCTION IF EXISTS fn_has_pachymetry;
DELIMITER $$
CREATE FUNCTION fn_has_pachymetry(
    p_patient_id BIGINT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(ce.clinical_exam_id) INTO v_count
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND et.name LIKE '%Paquimetría%';

    RETURN IF(v_count > 0, TRUE, FALSE);
END $$
DELIMITER ;
```

### 28.

Crear una función que determine si el paciente tiene controles pendientes según un número de meses.

```sql
DROP FUNCTION IF EXISTS fn_has_pending_control;
DELIMITER $$
CREATE FUNCTION fn_has_pending_control(
    p_patient_id BIGINT,
    p_months INT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    DECLARE v_last_date DATETIME;
    SELECT MAX(mv.visit_date) INTO v_last_date
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;

    IF v_last_date IS NULL OR v_last_date < DATE_SUB(CURDATE(), INTERVAL p_months MONTH) THEN
        RETURN TRUE;
    ELSE
        RETURN FALSE;
    END IF;
END $$
DELIMITER ;
```

### 29.

Crear una función que clasifique un paciente según cantidad de consultas: nuevo, recurrente o frecuente.

```sql
DROP FUNCTION IF EXISTS fn_classify_patient_loyalty;
DELIMITER $$
CREATE FUNCTION fn_classify_patient_loyalty(
    p_patient_id BIGINT
)
RETURNS VARCHAR(30)
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(mv.visit_id) INTO v_count
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;

    IF v_count <= 1 THEN RETURN 'Nuevo';
    ELSEIF v_count <= 4 THEN RETURN 'Recurrente';
    ELSE RETURN 'Frecuente';
    END IF;
END $$
DELIMITER ;
```

### 30.

Crear una función que retorne Completo si el paciente tiene OCT, campo visual, PIO y paquimetría, o Incompleto en caso contrario.

```sql
DROP FUNCTION IF EXISTS fn_check_patient_exams_complete;
DELIMITER $$
CREATE FUNCTION fn_check_patient_exams_complete(
    p_patient_id BIGINT
)
RETURNS VARCHAR(20)
READS SQL DATA
BEGIN
    IF fn_has_oct(p_patient_id) AND fn_has_visual_field(p_patient_id) AND fn_has_pachymetry(p_patient_id) AND (fn_get_max_pio(p_patient_id) IS NOT NULL) THEN
        RETURN 'Completo';
    ELSE
        RETURN 'Incompleto';
    END IF;
END $$
DELIMITER ;
```

## Funciones estadísticas

### 31.

Crear una función que calcule el promedio de PIO entre dos fechas para un paciente.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_pio_between_dates;
DELIMITER $$
CREATE FUNCTION fn_get_avg_pio_between_dates(
    p_patient_id BIGINT,
    p_start_date DATETIME,
    p_end_date DATETIME
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(6,2);
    SELECT AVG(iop.pressure_value) INTO v_avg
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
      AND iop.measured_at BETWEEN p_start_date AND p_end_date;
    RETURN v_avg;
END $$
DELIMITER ;
```

### 32.

Crear una función que calcule la diferencia entre la primera y última PIO.

```sql
DROP FUNCTION IF EXISTS fn_get_pio_difference;
DELIMITER $$
CREATE FUNCTION fn_get_pio_difference(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_first DECIMAL(6,2);
    DECLARE v_last DECIMAL(6,2);

    SELECT iop.pressure_value INTO v_first
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY iop.measured_at ASC LIMIT 1;

    SELECT iop.pressure_value INTO v_last
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY iop.measured_at DESC LIMIT 1;

    RETURN v_last - v_first;
END $$
DELIMITER ;
```

### 33.

Crear una función que retorne el número de días desde la última consulta.

```sql
DROP FUNCTION IF EXISTS fn_days_since_last_visit;
DELIMITER $$
CREATE FUNCTION fn_days_since_last_visit(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_date DATETIME;
    SELECT MAX(mv.visit_date) INTO v_date
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;

    IF v_date IS NULL THEN RETURN NULL; END IF;
    RETURN DATEDIFF(CURDATE(), v_date);
END $$
DELIMITER ;
```

### 34.

Crear una función que retorne el número de meses desde el último OCT.

```sql
DROP FUNCTION IF EXISTS fn_months_since_last_oct;
DELIMITER $$
CREATE FUNCTION fn_months_since_last_oct(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_date DATETIME;
    SELECT MAX(ce.exam_date) INTO v_date
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND et.name LIKE '%OCT%';

    IF v_date IS NULL THEN RETURN NULL; END IF;
    RETURN TIMESTAMPDIFF(MONTH, v_date, CURDATE());
END $$
DELIMITER ;
```

### 35.

Crear una función que retorne el número de meses desde el último campo visual.

```sql
DROP FUNCTION IF EXISTS fn_months_since_last_vf;
DELIMITER $$
CREATE FUNCTION fn_months_since_last_vf(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_date DATETIME;
    SELECT MAX(ce.exam_date) INTO v_date
    FROM clinical_exam ce
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND (et.name LIKE '%Campo visual%' OR et.name LIKE '%Campimetría%');

    IF v_date IS NULL THEN RETURN NULL; END IF;
    RETURN TIMESTAMPDIFF(MONTH, v_date, CURDATE());
END $$
DELIMITER ;
```

### 36.

Crear una función que calcule el promedio de RNFL de los OCT de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_rnfl;
DELIMITER $$
CREATE FUNCTION fn_get_avg_rnfl(
    p_patient_id BIGINT
)
RETURNS DECIMAL(12,4)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(12,4);
    SELECT AVG(er.value_numeric) INTO v_avg
    FROM exam_result er
    JOIN clinical_exam ce ON ce.clinical_exam_id = er.clinical_exam_id
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND et.name LIKE '%OCT%';
    RETURN v_avg;
END $$
DELIMITER ;
```

### 37.

Crear una función que retorne el valor más reciente de RNFL.

```sql
DROP FUNCTION IF EXISTS fn_get_latest_rnfl;
DELIMITER $$
CREATE FUNCTION fn_get_latest_rnfl(
    p_patient_id BIGINT
)
RETURNS DECIMAL(12,4)
READS SQL DATA
BEGIN
    DECLARE v_val DECIMAL(12,4);
    SELECT er.value_numeric INTO v_val
    FROM exam_result er
    JOIN clinical_exam ce ON ce.clinical_exam_id = er.clinical_exam_id
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND et.name LIKE '%OCT%'
    ORDER BY ce.exam_date DESC LIMIT 1;
    RETURN v_val;
END $$
DELIMITER ;
```

### 38.

Crear una función que calcule el promedio de VFI de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_vfi;
DELIMITER $$
CREATE FUNCTION fn_get_avg_vfi(
    p_patient_id BIGINT
)
RETURNS DECIMAL(12,4)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(12,4);
    SELECT AVG(er.value_numeric) INTO v_avg
    FROM exam_result er
    JOIN clinical_exam ce ON ce.clinical_exam_id = er.clinical_exam_id
    JOIN exam_type et ON et.exam_type_id = ce.exam_type_id
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND (et.name LIKE '%Campo visual%' OR et.name LIKE '%Campimetría%');
    RETURN v_avg;
END $$
DELIMITER ;
```

### 39.

Crear una función que retorne la cantidad de tratamientos históricos.

```sql
DROP FUNCTION IF EXISTS fn_count_historical_treatments;
DELIMITER $$
CREATE FUNCTION fn_count_historical_treatments(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(t.treatment_id) INTO v_count
    FROM treatment t
    JOIN medical_visit mv ON mv.visit_id = t.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

### 40.

Crear una función que retorne la cantidad de medicamentos diferentes utilizados por un paciente.

```sql
DROP FUNCTION IF EXISTS fn_count_distinct_medications;
DELIMITER $$
CREATE FUNCTION fn_count_distinct_medications(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(DISTINCT tm.medication_id) INTO v_count
    FROM treatment_medication tm
    JOIN treatment t ON t.treatment_id = tm.treatment_id
    JOIN medical_visit mv ON mv.visit_id = t.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

## Funciones avanzadas

### 41.

Crear una función que reciba paciente y ojo y retorne la última PIO registrada.

```sql
DROP FUNCTION IF EXISTS fn_get_last_pio_by_eye;
DELIMITER $$
CREATE FUNCTION fn_get_last_pio_by_eye(
    p_patient_id BIGINT,
    p_eye_code VARCHAR(20)
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_val DECIMAL(6,2);
    SELECT iop.pressure_value INTO v_val
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    JOIN eye e ON e.eye_id = iop.eye_id
    WHERE ch.patient_id = p_patient_id AND e.code = p_eye_code
    ORDER BY iop.measured_at DESC LIMIT 1;
    RETURN v_val;
END $$
DELIMITER ;
```

### 42.

Crear una función que reciba paciente y ojo y retorne la PIO promedio.

```sql
DROP FUNCTION IF EXISTS fn_get_avg_pio_by_eye;
DELIMITER $$
CREATE FUNCTION fn_get_avg_pio_by_eye(
    p_patient_id BIGINT,
    p_eye_code VARCHAR(20)
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_avg DECIMAL(6,2);
    SELECT AVG(iop.pressure_value) INTO v_avg
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    JOIN eye e ON e.eye_id = iop.eye_id
    WHERE ch.patient_id = p_patient_id AND e.code = p_eye_code;
    RETURN v_avg;
END $$
DELIMITER ;
```

### 43.

Crear una función que determine si la última PIO es mayor o menor que la primera.

```sql
DROP FUNCTION IF EXISTS fn_compare_first_last_pio;
DELIMITER $$
CREATE FUNCTION fn_compare_first_last_pio(
    p_patient_id BIGINT
)
RETURNS VARCHAR(20)
READS SQL DATA
BEGIN
    DECLARE v_first DECIMAL(6,2);
    DECLARE v_last DECIMAL(6,2);

    SELECT iop.pressure_value INTO v_first
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY iop.measured_at ASC LIMIT 1;

    SELECT iop.pressure_value INTO v_last
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY iop.measured_at DESC LIMIT 1;

    IF v_last > v_first THEN RETURN 'Mayor';
    ELSEIF v_last < v_first THEN RETURN 'Menor';
    ELSE RETURN 'Igual';
    END IF;
END $$
DELIMITER ;
```

### 44.

Crear una función que retorne la diferencia porcentual entre primera y última PIO.

```sql
DROP FUNCTION IF EXISTS fn_get_pio_percent_diff;
DELIMITER $$
CREATE FUNCTION fn_get_pio_percent_diff(
    p_patient_id BIGINT
)
RETURNS DECIMAL(6,2)
READS SQL DATA
BEGIN
    DECLARE v_first DECIMAL(6,2);
    DECLARE v_last DECIMAL(6,2);

    SELECT iop.pressure_value INTO v_first
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY iop.measured_at ASC LIMIT 1;

    SELECT iop.pressure_value INTO v_last
    FROM intraocular_pressure iop
    JOIN medical_visit mv ON mv.visit_id = iop.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id
    ORDER BY iop.measured_at DESC LIMIT 1;

    IF v_first IS NULL OR v_first = 0 THEN RETURN 0; END IF;
    RETURN ((v_last - v_first) / v_first) * 100;
END $$
DELIMITER ;
```

### 45.

Crear una función que retorne el diagnóstico principal más reciente de un paciente.

```sql
DROP FUNCTION IF EXISTS fn_get_latest_main_diagnosis;
DELIMITER $$
CREATE FUNCTION fn_get_latest_main_diagnosis(
    p_patient_id BIGINT
)
RETURNS VARCHAR(200)
READS SQL DATA
BEGIN
    DECLARE v_diag VARCHAR(200);
    SELECT d.name INTO v_diag
    FROM visit_diagnosis vd
    JOIN diagnosis d ON d.diagnosis_id = vd.diagnosis_id
    JOIN medical_visit mv ON mv.visit_id = vd.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND vd.diagnosis_type = 'Principal'
    ORDER BY mv.visit_date DESC LIMIT 1;
    RETURN v_diag;
END $$
DELIMITER ;
```

### 46.

Crear una función que retorne el nombre del medicamento activo más reciente.

```sql
DROP FUNCTION IF EXISTS fn_get_latest_active_medication;
DELIMITER $$
CREATE FUNCTION fn_get_latest_active_medication(
    p_patient_id BIGINT
)
RETURNS VARCHAR(150)
READS SQL DATA
BEGIN
    DECLARE v_med VARCHAR(150);
    SELECT m.name INTO v_med
    FROM treatment_medication tm
    JOIN medication m ON m.medication_id = tm.medication_id
    JOIN treatment t ON t.treatment_id = tm.treatment_id
    JOIN treatment_status ts ON ts.treatment_status_id = t.treatment_status_id
    JOIN medical_visit mv ON mv.visit_id = t.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND ts.name = 'Activo'
    ORDER BY t.start_date DESC LIMIT 1;
    RETURN v_med;
END $$
DELIMITER ;
```

### 47.

Crear una función que retorne la cantidad de procedimientos realizados a un paciente.

```sql
DROP FUNCTION IF EXISTS fn_count_patient_procedures;
DELIMITER $$
CREATE FUNCTION fn_count_patient_procedures(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(vp.visit_procedure_id) INTO v_count
    FROM visit_procedure vp
    JOIN medical_visit mv ON mv.visit_id = vp.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

### 48.

Crear una función que determine si un profesional ha atendido alguna vez a un paciente específico.

```sql
DROP FUNCTION IF EXISTS fn_has_professional_attended_patient;
DELIMITER $$
CREATE FUNCTION fn_has_professional_attended_patient(
    p_professional_id BIGINT,
    p_patient_id BIGINT
)
RETURNS BOOLEAN
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(mv.visit_id) INTO v_count
    FROM medical_visit mv
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE mv.professional_id = p_professional_id AND ch.patient_id = p_patient_id;

    RETURN IF(v_count > 0, TRUE, FALSE);
END $$
DELIMITER ;
```

### 49.

Crear una función que calcule la cantidad total de exámenes especializados registrados para un paciente.

```sql
DROP FUNCTION IF EXISTS fn_count_specialized_exams;
DELIMITER $$
CREATE FUNCTION fn_count_specialized_exams(
    p_patient_id BIGINT
)
RETURNS INT
READS SQL DATA
BEGIN
    DECLARE v_count INT;
    SELECT COUNT(ce.clinical_exam_id) INTO v_count
    FROM clinical_exam ce
    JOIN medical_visit mv ON mv.visit_id = ce.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id;
    RETURN IFNULL(v_count, 0);
END $$
DELIMITER ;
```

### 50.

Crear una función que genere un resumen textual como: Paciente: Carlos Gómez Consultas: 8 Controles glaucoma: 4 Última PIO OD: 18 Última PIO OI: 17 Tratamientos activos: 2 a partir del ID del paciente.

```sql
DROP FUNCTION IF EXISTS fn_generate_patient_text_summary;
DELIMITER $$
CREATE FUNCTION fn_generate_patient_text_summary(
    p_patient_id BIGINT
)
RETURNS TEXT
READS SQL DATA
BEGIN
    DECLARE v_name VARCHAR(200);
    DECLARE v_visits INT;
    DECLARE v_glaucoma INT;
    DECLARE v_pio_od DECIMAL(6,2);
    DECLARE v_pio_oi DECIMAL(6,2);
    DECLARE v_treatments INT;

    SELECT CONCAT(pe.first_name, ' ', pe.last_name) INTO v_name
    FROM patient p JOIN person pe ON pe.person_id = p.person_id WHERE p.patient_id = p_patient_id;

    SET v_visits = fn_count_patient_visits(p_patient_id);
    SET v_glaucoma = fn_count_glaucoma_controls(p_patient_id);
    SET v_pio_od = fn_get_last_pio_by_eye(p_patient_id, 'OD');
    SET v_pio_oi = fn_get_last_pio_by_eye(p_patient_id, 'OI');

    SELECT COUNT(t.treatment_id) INTO v_treatments
    FROM treatment t
    JOIN treatment_status ts ON ts.treatment_status_id = t.treatment_status_id
    JOIN medical_visit mv ON mv.visit_id = t.visit_id
    JOIN clinical_history ch ON ch.clinical_history_id = mv.clinical_history_id
    WHERE ch.patient_id = p_patient_id AND ts.name = 'Activo';

    RETURN CONCAT(
        'Paciente: ', IFNULL(v_name,'N/A'),'\n',
        'Consultas: ', v_visits,'\n',
        'Controles glaucoma: ', v_glaucoma,'\n',
        'Última PIO OD: ', IFNULL(v_pio_od, 0),'\n',
        'Última PIO OI: ', IFNULL(v_pio_oi, 0),'\n',
        'Tratamientos activos: ', IFNULL(v_treatments, 0)
    );
END $$
DELIMITER ;
```

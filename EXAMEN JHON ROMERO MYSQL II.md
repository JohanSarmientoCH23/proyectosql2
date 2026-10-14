# EXAMEN JHON ROMERO MYSQL II

## Examen 4. Gestión de tratamientos y
medicamentos

**Diseño e implementación de una base de datos relacional normalizada para la gestión de historias clínicas de pacientes del área de oftalmología y glaucoma.**



## 4.1. Planteamiento del problema

La institución oftalmológica necesita administrar los tratamientos formulados a los pacientes durante sus consultas
médicas.
Un tratamiento puede contener varios medicamentos y un mismo medicamento puede utilizarse en diferentes
tratamientos. Para cada medicamento formulado es necesario conservar la dosis, frecuencia, duración e instrucciones
correspondientes.
El área médica necesita consultar tratamientos, identificar medicamentos utilizados con mayor frecuencia y garantizar la
coherencia de las fechas registradas.
Se solicita desarrollar consultas y mecanismos de validación que faciliten la gestión de los tratamientos.

## 4.2. Resultados de aprendizaje

El estudiante deberá interpretar relaciones muchos a muchos, consultar medicamentos asociados a tratamientos, aplicar
funciones de agrupación, utilizar subconsultas y establecer mecanismos de integridad de datos.

## 4.3. Actividades evaluativas

### Actividad 1. Análisis del modelo relacional — 10 puntos / 10 minutos

Analice las tablas treatment , treatment_medication y medication .
Explique la relación existente entre tratamientos y medicamentos, identifique la función de la tabla intermedia e indique
por qué los atributos dosage y frequency pertenecen a dicha relación y no al catálogo de medicamentos.

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

### Actividad 2. Consultas básicas — 15 puntos / 15 minutos

Escriba tres consultas SQL:

1. Listar los medicamentos con su nombre, principio activo y concentración.

   ```sql
   SELECT
       medication_id,
       name,
       active_ingredient,
       concentration
   FROM medication;
   ```

   ![](Imágenes/exame sql II/Captura desde 2026-10-14 11-44-34.png)

2. Obtener los tratamientos cuya fecha de finalización sea posterior a la fecha actual.

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

   ![](Imágenes/exame sql II/Captura desde 2026-10-14 12-54-34.png)

3. Consultar los medicamentos cuyo nombre contenga la palabra Timolol .

  ```sql
  SELECT
      medication_id,
      name,
      active_ingredient,
      concentration
  FROM medication
  WHERE name LIKE 'Timolol';
  ```

  ![](Imágenes/exame sql II/Captura desde 2026-10-14 12-06-52.png)

  ### Actividad 3. Consultas relacionales — 20 puntos / 20 minutos

  Construya dos consultas:

4. Mostrar los tratamientos con sus medicamentos asociados, incluyendo dosis y frecuencia.

   ```sql
   SELECT
   	t.treatment_id
       ts.name,
       m.name,
       tm.dosage,    
   	tm.frequency,    
   FROM treatment t
   INNER JOIN treatment_status ts 
   ON ts.treatment_status_id = t.treatment_id
   INNER JOIN treatment_medication tm 
   ON tm.treatment_id = t.treatment_id
   INNER JOIN medication m
   ON m.medication_id = tm.medication_id;
   WHERE ts.name = 'Activo';
   ```

   

5. Obtener la cantidad de medicamentos distintos registrados en cada tratamiento.

  ### Actividad 4. Consultas avanzadas — 20 puntos / 20 minutos

  Desarrolle dos consultas:

6. Mostrar los medicamentos utilizados en más de un tratamiento.

7. Obtener los tratamientos cuya cantidad de medicamentos es superior al promedio de medicamentos por 
  tratamiento, mediante una subconsulta. Incluya los tratamientos sin medicamentos al calcular el promedio.

  ### Actividad 5. Creación de una vista — 15 puntos / 10 minutos

  Crear la vista vw_patient_medications , con la siguiente información:
  Identificador del paciente.
  Nombre completo.
  Identificador del tratamiento.
  Nombre del medicamento.
  Dosis.
  Frecuencia.
  Fecha de inicio del tratamiento.
  Fecha de finalización.

  ### Actividad 6. Trigger de validación — 20 puntos / 15 minutos

  Crear el trigger trg_validate_treatment_dates , que se ejecute antes de insertar un registro en treatment .
  El trigger debe impedir el registro cuando la fecha de finalización sea anterior a la fecha de inicio, siempre que ambas
  fechas estén informadas.
  Utilice SIGNAL SQLSTATE '45000' para generar un mensaje de error descriptivo.
  Realice dos pruebas: un tratamiento con fechas válidas y otro con fechas inválidas. Utilice identificadores de consulta y
  estado existentes.
---

# Problema de Optimización: Asignación de Costo Mínimo para Soporte Técnico de ARL MARCA

**1. Objetivo General:**
Determinar la asignación óptima de recursos de soporte técnico para minimizar el costo total mensual asociado a la prestación de servicios por parte de ARL Sura a sus clientes en todo el territorio colombiano, garantizando el cumplimiento de la demanda de servicio requerida en cada departamento.

**2. Contexto y Entidades:**

*   **Cobertura Geográfica:** El servicio debe poder ser asignado a cualquiera de los 32 departamentos de Colombia más Bogotá D.C. (total 33 destinos).
*   **Proveedores de Servicio:** Se cuenta con 10 empresas prestadoras externas (P1 a P10), cada una ubicada físicamente (sede) en uno de los 10 departamentos principales del país.
*   **Capacidad de los Proveedores:** Cada empresa prestadora `p` tiene una capacidad máxima definida de horas de trabajo disponibles mensualmente (`capacidad_horas[p]`).
*   **Recursos Humanos (Asesores):** Cada empresa prestadora dispone de 7 tipos diferentes de asesores de soporte (T1, T2, T3, T4, T5, T6, T7), clasificados por nivel de experticia, siendo T1 el más básico y T7 el más experto.

**3. Costos Involucrados:**

*   **Costo por Hora de Asesor:**
    *   El asesor tipo T1 tiene un costo base por hora.
    *   Los asesores T2 a T5 tienen un costo que incrementa un 25% respecto al tipo inmediatamente anterior.
    *   Los asesores T6 y T7 tienen un costo que incrementa un 40% respecto al tipo inmediatamente anterior (T5 y T6, respectivamente).
*   **Costos de Viaje:** Para asignar un asesor a un departamento distinto al de su sede, se incurre en costos adicionales:
    *   **Transporte Principal:** Un costo base por viaje (ida y regreso) que depende del par origen-destino y del modo (terrestre, aéreo, fluvial). *(Actualmente simulado)*.
    *   **Transporte Local:** Un costo fijo por viaje para movilización dentro del departamento destino.
    *   **Hospedaje:** Un costo fijo por noche de hospedaje, asumido por cada viaje interdepartamental.
    *   **Prorrateo:** El costo total fijo del viaje (transporte principal + local + hospedaje) se divide por un número promedio de horas de trabajo efectivas por viaje (supuesto: 6 horas) para obtener un costo de viaje por hora asignada. El costo total por hora para el modelo es la suma del costo del asesor y este costo de viaje prorrateado.

**4. Demanda de Servicio:**

*   **Demanda Granular:** Se define una demanda específica de horas mensuales para cada departamento destino `d` y para cada nivel *mínimo* de experticia requerido `t_req` (`demanda_dept_tipo[(d, t_req)]`). Esto significa que se sabe cuántas horas en `d` necesitan, como mínimo, un asesor T1, cuántas necesitan al menos un T2, y así sucesivamente hasta T7. *(Actualmente simulada, distribuyendo una demanda total departamental simulada mediante porcentajes base por tipo)*.

**5. Reglas Operativas y Restricciones:**

*   **Sustitución de Asesores:** Se asume que un asesor de un nivel de experticia superior `t` puede satisfacer la demanda que requiere un nivel de experticia igual o inferior `t_req` (es decir, si `nivel(t) >= nivel(t_req)`).
*   **Satisfacción de Demanda (Restricción Clave):** Para cada departamento `d` y cada tipo de demanda `t_req`, la suma total de horas asignadas a ese departamento por *todos* los asesores `t` que estén *calificados* (según la regla de sustitución) debe ser mayor o igual a la demanda específica `demanda_dept_tipo[(d, t_req)]`.
*   **Límite de Capacidad por Proveedor:** La suma total de horas asignadas *por* una empresa prestadora `p` (sumando sobre todos los tipos de asesor que asigna y todos los destinos a los que los envía) no puede exceder su capacidad mensual total `capacidad_horas[p]`.
*   **Límite de Composición de Fuerza Laboral (70/30):** Para cada empresa prestadora `p`, las horas *efectivamente asignadas* utilizando asesores de tipo básico (T1 a T4) no pueden superar el 70% de su capacidad total `capacidad_horas[p]`. De forma análoga, las horas asignadas utilizando asesores de tipo experto (T5 a T7) no pueden superar el 30% de su capacidad total `capacidad_horas[p]`.

**6. Decisión a Optimizar:**
El modelo debe determinar el valor de `horas_asignadas[p, t, d]`: la cantidad de horas que la empresa prestadora `p` debe asignar utilizando un asesor de tipo `t` para atender la demanda en el departamento destino `d`, de forma que se cumplan todas las restricciones y se minimice el costo total mensual (suma de `horas_asignadas * costo_total_por_hora`).

**7. Supuestos Clave Actuales (para Contexto):**
*   Costos de transporte principal entre departamentos son simulados.
*   La demanda granular (por departamento y tipo) es simulada.
*   Los costos fijos de viaje se prorratean linealmente por hora asignada.
*   La sustitución de asesores por niveles superiores es perfecta (sin pérdida de eficiencia).
*   Las horas asignadas pueden ser fraccionarias (modelo continuo).

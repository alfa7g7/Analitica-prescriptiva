# Proyecto Final: Simulación y Optimización Aplicada

Este repositorio contiene el desarrollo del proyecto final, el cual integra dos enfoques de analítica prescriptiva para abordar problemas organizacionales específicos: simulación de eventos discretos y optimización matemática.

## Componentes del Proyecto

El proyecto se divide en dos partes principales, cada una ubicada en su respectiva subcarpeta:

### 1. Simulación: Análisis del Proceso de Contratación de Externos

* **Problema:** Determinar si se cuenta con los recursos necesarios para gestionar eficientemente las etapas de formalización de contratos de externos y estimar el tiempo total del proceso. La variabilidad en la duración de las etapas (por acumulación de trabajo, errores documentales) dificulta la predicción y la identificación de cuellos de botella.
* **Objetivo:** Mediante la simulación de eventos discretos, estimar el tiempo de respuesta total del proceso de contratación, evaluar la utilización de los recursos involucrados e identificar posibles puntos de congestión, basándose en un mapeo del flujo y estimaciones realistas de tiempos y capacidades.

### 2. Optimización: Asignación de Costo Mínimo para Soporte Técnico ARL

* **Problema:** Asignar eficientemente los recursos de soporte técnico (7 tipos de asesores de 10 proveedores externos ubicados en 10 departamentos) para cubrir la demanda de servicio requerida en los 32 departamentos de Colombia más Bogotá D.C., minimizando el costo total mensual.
* **Objetivo:** Desarrollar un modelo de optimización (programación lineal) que determine la cantidad óptima de horas a asignar por cada proveedor (`p`), tipo de asesor (`t`) y departamento destino (`d`) (`horas_asignadas[p, t, d]`).
* **Consideraciones Clave:** El modelo busca minimizar la suma de costos por hora de asesor (que varía por nivel de experticia) y costos de viaje prorrateados (transporte, viáticos). Debe satisfacer la demanda específica por departamento y nivel mínimo de experticia requerido, respetando la capacidad máxima de cada proveedor y una regla de composición de fuerza laboral (70% básicos / 30% expertos). Se permite que asesores más expertos cubran demandas de niveles inferiores.

## Navegación

Cada uno de estos proyectos, con sus respectivos análisis, modelos, datos y resultados, se encuentra detallado dentro de su carpeta correspondiente en este repositorio.

# PRJ-2026-001: Plan de Wireframe Mantenedor de Carga de Flujo — v2

**Metadata del Plan**
- ID: PRJ-2026-001_plan_mantenedor-carga-flujo_v2
- Versión: v2
- Fecha: 2026-04-10
- Estado: draft
- Rama de ejecución: `plan/prj-2026-001/mantenedor-carga-flujo-v2`
- Autor: GitHub Copilot
- Aprobador: PENDIENTE

---

## Resumen ejecutivo

Crear un plan ejecutable para diseñar en Figma (vía MCP) una nueva pantalla desktop estática llamada **Mantenedor de Carga de Flujo** que reemplaza entrada manual a 9 hojas Excel, con:
- Formulario dinámico de campos finitos según ítem seleccionado
- 5 vistas funcionales en pestañas: **Formulario (default)**, Registros, Carga CSV, Reportería, Auditoría
- Reutilización de header y footer del dashboard v0.1
- Trazabilidad y criterios de validación listos para implementación

---

## 1. Objetivo

Diseñar en Figma (vía MCP) una nueva pantalla desktop estática del Mantenedor de Carga de Flujo que reemplace la entrada manual a 9 hojas Excel, con formulario configurado según campos finitos del ítem seleccionado, 5 vistas funcionales en pestañas (registros, formulario, carga CSV, reportería, auditoría), header/footer reutilizado del dashboard v0.1, y criterios de validación listos para implementación.

---

## 2. Alcance

### Incluye (IN)
- Nueva pantalla desktop estática para Mantenedor de Carga de Flujo (reemplaza 9 hojas Excel: Leasing, Créditos, Deuda por pagar empresas relacionadas, Arriendos de propiedades, Backlog, Compras proyectadas, Imposiciones/remuneraciones/finiquitos, Seguros, Impuestos).
- Estructura de layout alineada al sistema actual: header y footer reutilizados del dashboard; barra contexto (con selector de ítem/tipo de registro); 5 pestañas funcionales (Formulario [default], Registros, Carga CSV, Reportería, Auditoría).
- Formulario dinámico: campos finitos según ítem seleccionado (ej: Patente comercial - Impto Territorial - Contribuciones con sus campos específicos).
- Tabla de registros actuales del ítem: CRUD básico (crear, editar, eliminar, ver).
- Interfaz de carga masiva CSV: upload, validación de formato, reportería de errores por registro.
- Vista de reportería: filtros por período, empresa, tipo de registro; generación de reporte tabular.
- Vista de auditoría: historial inmutable de cambios por registro (usuario, acción, fecha, valores previos/posteriores).
- Definición visual de estados por registro: nuevo, editado, con error, validado.

### Excluye (OUT)
- Prototipo interactivo navegable.
- Versión mobile/tablet.
- Diseño de alta fidelidad (colores finales, sistema tipográfico definitivo).
- Implementación en código frontend/backend.
- Integración real con ERP Manager o portal bancario.
- Lógica de cálculo de campos derivados (deberá especificarse en fase de componentes).

### Supuestos
- Se mantiene alcance v0.1: desktop estático.
- Se reutiliza el archivo Figma actual (key `n1PBP4Uk3keBmziUSBgSTb`) en nueva página/frame dedicada.
- Los campos del formulario de cada ítem ya están documentados en ERF paso 2 con "Patente comercial - Impto Territorial - Contribuciones" como ejemplo.
- Header y footer aprovechan estructura definida en task.md: Logo EBI, usuario, logout (header) y Saldo neto, timestamp, usuario, correo (footer).
- La vista Formulario es la pestaña por defecto.

---

## 3. Fases y Tareas

### Fase 0: Preparación y trazabilidad
**Objetivo:** Asegurar condiciones de ejecución, acceso a especificación de campos ERF, y consistencia de trabajo antes de diseñar.

| ID | Tarea | Depende de | Asignado | Estado |
|----|-------|-----------|----------|--------|
| T-00 | Confirmar aprobación del plan draft v2 y acceso a ERF paso 2 con especificación de campos | — | PM | ✓ Completado |
| T-01 | Crear rama dedicada del plan: plan/prj-2026-001/mantenedor-carga-flujo-v2 | T-00 | Responsable Git | ✓ Completado |
| T-02 | Validar que MCP Figma esté operativo y apuntando al file key correcto | T-01 | Responsable Diseño | 🕐 En progreso |
| T-03 | Extraer y consolidar matriz de campos para cada uno de los 9 ítems desde ERF paso 2; usar ejemplo Patente comercial como base | T-00 | Analista Funcional | 🕐 En progreso |

### Fase 1: Discovery funcional y definición de estructura
**Objetivo:** Traducir requerimientos de 5 vistas, formulario dinámico y campos finitos en estructura de wireframe verificable.

| ID | Tarea | Depende de | Asignado | Estado |
|----|-------|-----------|----------|--------|
| T-04 | Mapear campos del formulario para ítem prioritario (ej: Patente comercial - Impto Territorial - Contribuciones) desde matriz ERF | T-03 | UX/BA | Pendiente |
| T-05 | Definir secciones de cada pestaña: Formulario (campos + botones), Registros (tabla + CRUD), Carga CSV (upload + validación), Reportería (filtros + tabla), Auditoría (tabla historial) | T-04 | UX | Pendiente |
| T-06 | Definir estados visuales de registro: nuevo, editado, con error validación, validado | T-05 | UX | Pendiente |
| T-07 | Validar estructura de formulario dinámico con Jefatura Finanzas y Tesorería | T-05 | PM + Negocio | Pendiente |
| T-08 | Validar comportamiento esperado de 5 pestañas y flujo de usuario recomendado | T-07 | PM + Tesorería | Pendiente |

### Fase 2: Construcción del wireframe en Figma vía MCP
**Objetivo:** Crear la nueva pantalla con 5 vistas y componentes en archivo Figma del proyecto.

| ID | Tarea | Depende de | Asignado | Estado |
|----|-------|-----------|----------|--------|
| T-09 | Crear nueva página "Mantenedor Carga Flujo" en archivo Figma | T-08 | Diseñador | Pendiente |
| T-10 | Montar estructura base desktop (1600x1200) con header y footer reutilizados del dashboard | T-09 | Diseñador | Pendiente |
| T-11 | Construir layout de barra contexto con selector de ítem (dropdown desplegable) alineado a guía de layout existente | T-10 | Diseñador | Pendiente |
| T-12 | Construir componentes de pestañas: visualmente diferenciadas (activa/inactiva permite alternar vistas) | T-10 | Diseñador | Pendiente |
| T-13 | Construir pestaña "Formulario" (default): campos según ejemplo Patente comercial; botones: Guardar, Cancelar, Limpiar | T-11, T-12 | Diseñador | Pendiente |
| T-14 | Construir pestaña "Registros": tabla con filas de registros, columnas de campos capturados, iconos CRUD (editar, eliminar), indicador de estado visual | T-11, T-12 | Diseñador | Pendiente |
| T-15 | Construir pestaña "Carga CSV": área de drop/upload, icono de file, botones: Cargar, Cancelar, validación de formato | T-11, T-12 | Diseñador | Pendiente |
| T-16 | Construir pestaña "Reportería": filtros (período, empresa, tipo), botón Generar, tabla de reporte con datos | T-11, T-12 | Diseñador | Pendiente |
| T-17 | Construir pestaña "Auditoría": tabla de historial (usuario, acción, fecha, valores previos/posteriores), sin botones de edición | T-11, T-12 | Diseñador | Pendiente |
| T-18 | Construir 3 variantes de estado general (vacío, con datos, con error validación) si aplica a formulario/registros | T-13, T-14, T-15 | Diseñador | Pendiente |
| T-19 | Ajustar consistencia visual con dashboard v0.1 en todas las pestañas (espaciado, jerarquía, densidad, tipografía) | T-13, T-14, T-15, T-16, T-17 | Diseñador | Pendiente |

### Fase 3: Validación y cierre de plan
**Objetivo:** Validar el resultado con checklist funcional e integrado, feedback de stakeholders y registro de decisiones.

| ID | Tarea | Depende de | Asignado | Estado |
|----|-------|-----------|----------|--------|
| T-20 | Revisar wireframe con checklist: 5 pestañas completas, header/footer del dashboard, formulario con campos del ejemplo, tabla registros con CRUD, carga CSV, reportería, auditoría | T-19 | UX/BA | Pendiente |
| T-21 | Validar consistencia de layout con guía de implementación (32px márgenes, alineación cabecera-valores) | T-20 | Diseñador | Pendiente |
| T-22 | Realizar walkthrough con stakeholders clave (Tesorería, Finanzas) y consolidar feedback | T-20, T-21 | PM | Pendiente |
| T-23 | Registrar decisiones de diseño, cambios aceptados y pendientes para siguiente iteración | T-22 | PM/BA | Pendiente |
| T-24 | Marcar plan como approved o generar v3 si hay cambios mayores | T-23 | PM | Pendiente |

---

## 4. Entregables

| Entregable | Tipo | Criterio de aceptación | Vínculo |
|-----------|------|----------------------|---------|
| Frame "Mantenedor Carga Flujo - Pestaña Formulario (default)" | design | Formulario con campos del ítem ejemplo (Patente comercial), botones Guardar/Cancelar/Limpiar, header y footer reutilizados | Figma (key n1PBP4Uk3keBmziUSBgSTb) |
| Frame "Mantenedor Carga Flujo - Pestaña Registros" | design | Tabla con registros capturados, columnas de campos, iconos CRUD, indicadores de estado visual | Figma (key n1PBP4Uk3keBmziUSBgSTb) |
| Frame "Mantenedor Carga Flujo - Pestaña Carga CSV" | design | Área de upload, botones de carga y cancelación, validación de formato visible | Figma (key n1PBP4Uk3keBmziUSBgSTb) |
| Frame "Mantenedor Carga Flujo - Pestaña Reportería" | design | Filtros de período/empresa, tabla reporte con datos | Figma (key n1PBP4Uk3keBmziUSBgSTb) |
| Frame "Mantenedor Carga Flujo - Pestaña Auditoría" | design | Tabla historial inmutable con columnas: usuario, acción, fecha, valores previos/posteriores | Figma (key n1PBP4Uk3keBmziUSBgSTb) |
| Checklist de validación funcional/layout | doc | Cobertura de 5 pestañas, campos finitos, reuso header/footer, estados visuales, trazabilidad | docs/task.md + notas de revisión |

---

## 5. Verificación (Checklist de cierre)

- [ ] Todos los frames de las 5 pestañas están creados y navegables en Figma vía MCP.
- [ ] Header y footer coinciden exactamente con estructura del dashboard v0.1 (task.md).
- [ ] El formulario de la pestaña default incluye al menos los campos del ejemplo Patente comercial - Impto Territorial - Contribuciones.
- [ ] Tabla de registros tiene acciones CRUD visibles y estados visuales diferenciados.
- [ ] Pestaña Carga CSV incluye área de drop/upload y validación de formato.
- [ ] Pestaña Reportería incluye filtros funcionales (período, empresa) y tabla de salida.
- [ ] Pestaña Auditoría tiene tabla historial sin opciones de edición (inmutable).
- [ ] Stakeholders validaron estructura de 5 pestañas y emitieron feedback de conformidad.
- [ ] La decisiones clave quedan registradas en `/memories/repo/` para referencia futura.

---

## 6. Riesgos

| # | Riesgo | Probabilidad | Impacto | Mitigación |
|----|-------|-------------|---------|-----------|
| R-01 | Ambigüedad en especificación de campos ERF (paso 2) — matriz incompleta o ejemplo Patente comercial insuficiente | Media | Alto | T-03: extracción y consolidación de matriz de campos desde ERF; validación con PM antes de T-04 |
| R-02 | Complejidad de 5 pestañas con comportamientos distintos (formulario dinámico, tabla CRUD, CSV, reporte, auditoría) | Media | Alto | T-05, T-07: definición clara de interacción esperada por pestaña con validación de negocio |
| R-03 | Re-trabajo por cambios tardíos de estructura o campos del formulario | Media | Alto | T-08: validación de comportamiento de pestañas con stakeholders antes de construir en Figma |
| R-04 | Integración visual de 5 pestañas dentro de mismo frame mantiene consistencia con dashboard base | Baja | Medio | T-19: ajuste final de espaciado y jerarquía visual comparando con task.md e layout-implementation-v1.md |

---

## 7. Decisiones Tomadas

| Decisión | Valor | Rationale |
|----------|-------|-----------|
| Tipo de entregable | Plan detallado y ejecutable por MCP Figma | Pedido explícito del usuario basado en ERT v2.0 + ERF paso 2 |
| Tipo de wireframe | Nueva pantalla completa multi-vista | Reemplazo de 9 hojas Excel con 5 pestañas funcionales |
| Alcance de diseño | Desktop estático v0.1 | Reducir riesgo, mantener consistencia con baseline dashboard |
| Prioridad funcional | Mantenedor de Carga de Flujo con 5 vistas | Especificado en ERT v2.0; formulario dinámico según campos definidos en ERF paso 2 |
| Estructura de UI | Reutiliza header/footer de dashboard + 5 pestañas en área principal | Maximiza consistencia visual y re-uso de componentes; vista default Formulario |
| Ejemplo de campos | Patente comercial - Impto Territorial - Contribuciones | Proporcionado por usuario como referencia de estructura de formulario dinámico |

---

## 8. Recursos y Referencias

- **Figma**: https://www.figma.com/design/n1PBP4Uk3keBmziUSBgSTb
- **GitHub Repo**: https://github.com/diegosvart/cash-flow-design
- **ERT v2.0**: docs/ERT/ERT_PRJ-2026-001_CashFlow_v1.0.md (+ actualización con Mantenedor Carga Flujo)
- **ERF paso 2**: PRJ-01-CASH_FLOW-ERF.docx — Especificación de matriz de campos finitos por ítem
- **Estructura UI base**: docs/task.md (header, footer, patrón visual del dashboard)
- **Guía de layout**: docs/layout-implementation-v1.md (32px márgenes, alineación, restricciones)
- **Rama de ejecución**: `plan/prj-2026-001/mantenedor-carga-flujo-v2`

---

## 9. Control de versiones del plan

| Versión | Fecha | Autor | Estado | Cambio |
|---------|-------|-------|--------|--------|
| v1 | 2026-04-10 | GitHub Copilot | archived | Creación inicial del plan para nuevo wireframe del módulo Mantenedor de carga de flujo |
| v2 | 2026-04-10 | GitHub Copilot | draft | Actualización integral basada en ERT v2.0 + ERF paso 2: incorpora 5 vistas (Formulario/default, Registros, Carga CSV, Reportería, Auditoría); formulario dinámico con campos finitos del ejemplo Patente comercial; reuso de header/footer del dashboard; 24 tareas de construcción detalladas |

---

## Estimación de tokens y contexto

- **Tokens esperados para ejecución**: 25k-35k (4 fases, wireframe complejo con 5 pestañas)
- **Tokens disponibles estimados**: 125k-135k (post-actualización)
- **Recomendación**: 4 fases independientes para no exceder límite; permitir iteración si hay feedback mayor

---

**Plan aprobado para ejecución en rama:** `plan/prj-2026-001/mantenedor-carga-flujo-v2`  
**Próximo paso:** T-02 (Validar MCP Figma) + T-03 (Extraer campos ERF)

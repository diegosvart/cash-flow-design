# Especificación de Campos: Mantenedor de Carga de Flujo

**Documento de referencia:** Matriz de campos finitos por ítem (9 categorías de entrada manual)  
**Fuente:** ERF paso 2 - PRJ-01-CASH_FLOW-ERF.docx  
**Fecha extracto:** 2026-04-10  
**Nota:** Ejemplo detallado para "Patente comercial - Impto Territorial - Contribuciones"; estructura aplicable a otros 8 ítems

---

## 1. Matriz de 9 Ítems de Entrada Manual

El mantenedor de Carga de Flujo reemplaza entrada manual a estas 9 hojas de Excel:

| ID | Ítem / Campo | Descripción | Tipo de formulario esperado | Status |
|----|---|---|---|---|
| 1 | **Leasing** | Acuerdos de arrendamiento de activos | Tabla con campos producto/monto/fecha vencimiento | Especificación por definir |
| 2 | **Créditos** | Líneas de crédito activas y disponibles | Tabla con campos entidad/límite/utilizado/disponible | Especificación por definir |
| 3 | **Deuda por pagar empresas relacionadas** | Préstamos inter-empresa | Tabla con campos empresa/monto/fecha vencimiento | Especificación por definir |
| 4 | **Arriendos de propiedades** | Rentas de inmuebles | Tabla con campos propiedad/canon/período | Especificación por definir |
| 5 | **Backlog (Contratos)** | Ingresos proyectados no facturados | Tabla con campos cliente/contrato/monto/fecha | Especificación por definir |
| 6 | **Compras proyectadas** | Órdenes de compra emitidas sin facturación | Tabla con campos proveedor/producto/monto/fecha | Especificación por definir |
| 7 | **Imposiciones, remuneraciones y finiquitos** | Aportes, sueldos y liquidaciones | Tabla con campos empleado/tipo/monto/período | Especificación por definir |
| 8 | **Seguros** | Pólizas y primas de seguros | Tabla con campos cobertura/prima/vencimiento | Especificación por definir |
| 9 | **Impuestos** | Patentes, contribuciones, ISR, permisos circulación, F29 | Tabla con campos tipo/monto/fecha vencimiento **[DETALLE ABAJO]** | ✓ Ejemplo detallado |

---

## 2. Ejemplo Detallado: "Patente comercial - Impto Territorial - Contribuciones"

**Ítem:** Impuestos > Patente comercial - Impto Territorial - Contribuciones

**Descripción funcional:**  
Formulario para registrar pagos de patentes municipales, contribuciones inmobiliarias e impuestos territoriales asociados a la operación comercial.

### 2.1 Campos del formulario

| Campo | Tipo | Validación | Obligatorio | Ejemplo |
|-------|------|-----------|-----------|---------|
| **Tipo de Impuesto** | Dropdown (predeterminado/seleccionable) | Lista: Patente, Contribución, Impuesto Territorial, Permiso de Circulación, F29 | Sí | "Patente comercial" |
| **Descripción** | Text (textarea, 200 caracteres max) | No vacío, máx 200 caracteres | No | "Patente municipal licencia de conducción" |
| **Período/Año** | Date picker + Period selector | Formato YYYY-MM o rango (ej: 2026-01 o 2026 completo) | Sí | "2026-01" |
| **Monto** | Currency (CLP) | Número positivo ≥ 0, máx 2 decimales | Sí | "150.000,00" |
| **Moneda** | Dropdown | Predefinido: CLP, UF, USD | Sí | "CLP" |
| **Tasa de Cambio** | Number | Número positivo > 0 (si moneda es USD/UF) | Condicional | "920,50" |
| **Concepto / Referencia** | Text (100 caracteres) | No vacío si tipo es "Otro" | Condicional | "Licencia operacional municipal" |
| **Entidad Recaudadora** | Dropdown o autocomplete | Ejemplos: SII, Municipalidad, Tesorería, Notaría | Sí | "Municipalidad de Santiago" |
| **Fecha de Vencimiento** | Date picker | Fecha futura o igual a hoy | Sí | "2026-04-30" |
| **Fecha de Pago Real** | Date picker | Fecha ≤ hoy (histórica) | No | "2026-04-25" |
| **Estado de Pago** | Dropdown | Opciones: Pendiente, Pagado, Anulado, En disputa | Sí | "Pagado" |
| **Metodo de Pago** | Dropdown | Opciones: Transferencia, Cheque, Efectivo, Tarjeta, Descuento nómina | Condicional (si estado="Pagado") | "Transferencia" |
| **Referencia de Comprobante** | Text (50 caracteres) | Formato libre (recibo, factura, acta) | Condicional (si estado="Pagado") | "Rec-2026-001234" |
| **Usuario/Responsable** | Autocomplete (readonly, llenar del sesión) | Validación de archivo activo de usuarios | Síguete (auto) | "diego.morales@grupo-ebi.cl" |
| **Notas** | Textarea (500 caracteres max) | Texto libre | No | "Pago anticipado. Aplica descuento por pronto pago del 5%." |

**Total de campos:** 15 campos (11 obligatorios, 3 condicionales, 1 readonly)

### 2.2 Estados visuales del formulario

| Estado | Trigger | Comportamiento |
|--------|---------|---------------|
| **Vacío** | Cargar formulario sin datos previos | Todos campos en blanco; botones: Guardar, Cancelar, Limpiar |
| **Con datos** | Cargar registro existente para edición | Todos campos completos; estado de guardado mostrado; botones: Guardar cambios, Cancelar, Eliminar (si no se duplica) |
| **Error validación** | Usuario intenta enviar con campos faltantes/inválidos | Resaltar campos con error (rojo), mostrar mensaje corto inline ("Campo obligatorio", "Monto debe ser positivo") |
| **Enviado/Guardado** | Usuario hace clic en Guardar y transacción completa | Mostrar notificación éxito transiente (toast), limpiar formulario, pasar a pestaña "Registros" |

### 2.3 Botones de acción

| Botón | Acción | Destino |
|-------|--------|--------|
| **Guardar** | Validar formulario + crear/actualizar registro en base de datos (en fase de implementación) | Pestaña "Registros" con row nuevo/actualizado |
| **Cancelar** | Limpiar formulario sin guardar | Mismo formulario, vacío |
| **Limpiar** | Reset de todos los campos al estado inicial | Formulario vacío (equivalente a reload) |

---

## 3. Aplicabilidad de esta estructura a otros 8 ítems

Cada ítem usará **el mismo patrón de formulario dinámico** pero con **campos específicos** según su naturaleza:

### Leasing
- Campos: Producto (bien arrendado), Proveedor, Monto cuota, Plazo restante, Vencimiento, Estado pago

### Créditos
- Campos: Banco/Entidad, Tipo de crédito, Monto límite, Monto utilizado, Disponible, Tasa, Vencimiento

### Deuda empresas relacionadas
- Campos: Empresa acreedor, Tipo préstamo, Monto, Fecha inicio, Vencimiento, Tasa interés, Estado

### Arriendos propiedades
- Campos: Inmueble, Canon mensual, Período arrendamiento, Vencimiento, Incremento anual, Estado pago

### Backlog
- Campos: Cliente, Contrato/OT, Monto, Descripción servicios/productos, Fecha facturación estimada

### Compras proyectadas
- Campos: Proveedor, Descripción compra, Monto, OC número, Fecha entrega estimada, Estado

### Imposiciones/Remuneraciones/Finiquitos
- Campos: Empleado, Tipo (imposición/sueldo/finiquito), Monto, Período, Concepto, Estado

### Seguros
- Campos: Tipo cobertura, Aseguradora, Prima, Período, Vencimiento, Límite cobertura, Deducible

---

## 4. Matriz consolidada de campos por ítem

| Ítem | Campos clave | # campos | Validación clave | Prioridad |
|-----|---|---|---|---|
| 1. Leasing | Producto, Monto, Vencimiento, Estado | 6-8 | Monto positivo, fecha válida | Media |
| 2. Créditos | Banco, Monto límite, Disponible, Tasa | 7-9 | Disponible ≤ Límite | Alta |
| 3. Deuda empresas | Empresa, Monto, Tasa, Vencimiento | 6-8 | Monto positivo | Media |
| 4. Arriendos | Inmueble, Canon, Período, Vencimiento | 6-8 | Canon positivo | Baja |
| 5. Backlog | Cliente, Monto, OT, Fecha estimada | 6-8 | Monto positivo | Alta |
| 6. Compras | Proveedor, Monto, OC, Fecha entrega | 6-8 | Monto positivo | Media |
| 7. Imposiciones | Empleado, Tipo, Monto, Período | 7-9 | Monto positivo, período válido | Alta |
| 8. Seguros | Cobertura, Prima, Vencimiento, Límite | 6-8 | Prima positiva, fecha válida | Baja |
| 9. Impuestos | Tipo, Monto, Vencimiento, Entidad, Estado pago | **15** | Monto positivo, fecha válida, estado consistente | **Alta** |

---

## 5. Notas de implementación para diseño wireframe

1. **Reutilizar componentes:** Selector de tipo (dropdown), campos de monto/currency, date pickers, botones de acción.
2. **Validación visual:** Mostrar errores inline, no en modal separado.
3. **Accesibilidad:** Labels asociados a inputs, autofocus en primer campo obligatorio.
4. **Responsive:** Aunque wireframe es desktop, considerar stack vertical en tablets.
5. **Estados inmutables:** Pestaña Auditoría mostrará historial completo sin permitir edición de valores históricos.

---

**Estado de esta especificación:** 🕐 En progreso (T-03)  
**Próximo paso:** Validar con stakeholders de Finanzas/Tesorería en T-07


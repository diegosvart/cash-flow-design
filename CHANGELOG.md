# Changelog — cash-flow-design

Todos los cambios relevantes del diseño Cash Flow quedan registrados en este archivo.  
Formato basado en [Keep a Changelog](https://keepachangelog.com/es/1.0.0/).  
Versionado según [Semantic Versioning](https://semver.org/lang/es/) — MAJOR.MINOR.PATCH.

---

## [v1.0.0] — 2026-04-09

### Agregado
- Wireframe desktop del dashboard principal de Cash Flow (1600 × 1200px).
- Header con logo EBI, nombre del sistema, usuario activo y logout.
- Barra de contexto con selector multi-empresa, selector de período, selector de moneda y botón Aplicar filtros.
- KPI Strip con 4 tarjetas horizontales: Saldo Inicial, Total Ingresos, Total Egresos, Saldo Proyectado.
- Tabla principal con 8 columnas base de identificación: Categoría, Subcategoría, Monto, % del total, Empresa, Fuente, Estado, Ver detalle.
- Vista temporal semanal de 8 columnas (S-1 a S+6): 1 semana pasada y 7 semanas futuras.
- Lógica de totalización: egresos distribuidos en columna de su fecha de pago asociada; subtotales por sección.
- 3 secciones plegables (estado expandido): Saldo Disponible (3 ítems), Ingresos (4 ítems), Egresos (20 ítems).
- Footer con saldo neto del período, última actualización (DD/MM/YYYY HH:MM) y usuario.
- Archivo Figma Design: `PRJ-2026-001_CashFlow_Wireframe_Desktop` (key: `n1PBP4Uk3keBmziUSBgSTb`).
- Documentación de gobernanza: plantilla de planes, checklist de validación, decisiones de diseño.
- Repositorio GitHub: `diegosvart/cash-flow-design`.

### Decisiones de alcance
- Solo desktop. Mobile excluido de esta versión.
- Wireframe estático. Prototipado interactivo excluido.
- Alta fidelidad visual excluida — pendiente para v0.2.

### Validación
- Checklist de comprobación ejecutado: 27/27 ítems presentes, estructura visual aprobada.
- Ver [governance/checklist-v1.md](governance/checklist-v1.md) para detalle completo.

---

## [Próximas versiones]

### [v0.2] — Por planificar
- Diseño de alta fidelidad (colores, tipografía, iconografía, estilos de componente).
- Refinamiento de tabla: columnas sticky, scroll horizontal para semanas.

### [v0.3] — Por planificar
- Especificación técnica de componentes reutilizables para frontend.
- Inventario de componentes: KPI Card, Table Section Header, Table Row, Week Column Cell.

### [v1.0] — Por planificar
- Implementación frontend. React o framework acordado con TI.
- Tabla interactiva con filtros dinámicos y secciones colapsables.

### [v1.1] — Por planificar
- Integración backend con ERP Manager y portal bancario.
- Carga automática de extracto bancario y datos de 9 categorías.

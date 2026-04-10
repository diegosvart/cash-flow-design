# Checklist de Validación — Wireframe v1.0.0

**Fecha de ejecución**: 2026-04-09  
**Ejecutado por**: Diego Morales  
**Archivo Figma**: [PRJ-2026-001_CashFlow_Wireframe_Desktop](https://www.figma.com/design/n1PBP4Uk3keBmziUSBgSTb)

---

## Verificación Estructural

| # | Criterio | Estado | Observación |
|----|----------|--------|-------------|
| 1 | Tipo de archivo: Figma Design (no FigJam) | ✅ APROBADO | Creado como Design file |
| 2 | Frame desktop principal visible | ✅ APROBADO | 1600 × 1200px |
| 3 | Header presente | ✅ APROBADO | Logo, nombre, usuario, logout |
| 4 | Barra de contexto presente | ✅ APROBADO | Selectores + botón Aplicar |
| 5 | KPI Strip — 4 tarjetas | ✅ APROBADO | Saldo Inicial, Total Ingresos, Total Egresos, Saldo Proyectado |
| 6 | Tabla Principal — bloque dominante | ✅ APROBADO | ~650px de altura |
| 7 | 8 columnas base de tabla | ✅ APROBADO | Categoría, Subcategoría, Monto, % Total, Empresa, Fuente, Estado, Ver |
| 8 | Vista semanal — 8 columnas exactas | ✅ APROBADO | S-1, S+0, S+1, S+2, S+3, S+4, S+5, S+6 |
| 9 | Footer presente | ✅ APROBADO | Saldo neto + timestamp + usuario |

---

## Verificación de Secciones Plegables

| Sección | Items requeridos | Items presentes | Estado |
|---------|-----------------|-----------------|--------|
| SALDO DISPONIBLE | 3 | 3 | ✅ COMPLETO |
| INGRESOS | 4 | 4 | ✅ COMPLETO |
| EGRESOS | 20 | 20 | ✅ COMPLETO |
| **TOTAL** | **27** | **27** | **✅ COMPLETO** |

**Ítems EGRESOS verificados**:
- ✅ Cheques a fecha girados no cobrados detalle
- ✅ Cheques por pagar
- ✅ Inversiones - fondos mutuos y depósitos a plazo
- ✅ Proveedores crédito por pagar
- ✅ Honorarios por pagar
- ✅ Fondos por rendir y varios
- ✅ Bono ley recolector
- ✅ Toma de inversión
- ✅ Factoring
- ✅ Leasing
- ✅ Créditos
- ✅ Préstamo empresa relacionada E
- ✅ Arriendos propiedades
- ✅ Seguros
- ✅ Compras proyectadas
- ✅ Remuneraciones y finiquitos
- ✅ Leyes sociales - IVA
- ✅ Impuestos – impuesto renta y permisos de circulación
- ✅ Patente comercial – Impto Territorial – Contribuciones
- ✅ Dividendos

---

## Verificación Funcional

| Criterio | Estado |
|----------|--------|
| Ventana temporal: 1 semana pasada (S-1) | ✅ |
| Ventana temporal: 7 semanas futuras (S+0 a S+6) | ✅ |
| Orden cronológico izquierda a derecha | ✅ |
| Subtotales semanales por sección | ✅ |
| Total general de egresos por semana | ✅ |
| Controles de filtro diferenciados visualmente | ✅ |
| Secciones con color diferenciado | ✅ |
| Jerarquía visual: tabla > KPIs > header | ✅ |

---

## Omisiones Aceptadas (Out of Scope)

| Elemento | Motivo |
|----------|--------|
| Vista mobile | Fuera del alcance de v0.1 |
| Prototipado interactivo | Fuera del alcance de v0.1 |
| Alta fidelidad visual | Planificado para v0.2 |

---

## Resultado Final

**✅ WIREFRAME v1.0.0 — VALIDADO Y APROBADO**

Cobertura: 27/27 ítems | Estructura: 9/9 bloques | Lógica temporal: Conforme

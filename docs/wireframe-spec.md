# Especificación del Wireframe v0.1

**Versión**: v0.1  
**Estado**: Completado  
**Fecha**: 2026-04-09  
**Archivo Figma**: [PRJ-2026-001_CashFlow_Wireframe_Desktop](https://www.figma.com/design/n1PBP4Uk3keBmziUSBgSTb)

---

## Contexto

Wireframe de fidelidad baja que establece la estructura, jerarquía y lógica funcional del dashboard principal del Sistema de Gestión de Cash Flow para Grupo EBI. Prioriza estructura sobre estilo.

---

## Frame Principal

| Propiedad | Valor |
|-----------|-------|
| Nombre | Dashboard Cash Flow / Desktop |
| Dimensiones | 1600 × 1200 px |
| Fidelidad | Baja (wireframe) |
| Plataforma | Desktop only |

---

## Bloques de Layout (top-down)

### 1. Header (60px)
- Logo Grupo EBI (izquierda)
- Nombre del sistema (centro)
- Usuario activo + Logout (derecha)

### 2. Barra de Contexto (70px)
Controles interactivos de filtrado global:

| Control | Tipo | Valor por defecto |
|---------|------|------------------|
| Selector empresa(s) | Multi-select dropdown | Todas |
| Selector período | Dropdown + input fecha | Diario · 09/04/2026 |
| Selector moneda | Dropdown | CLP |
| Botón Aplicar filtros | CTA primario | — |

### 3. KPI Strip (100px)
4 tarjetas horizontales de igual ancho:

| Tarjeta | Color indicador |
|---------|----------------|
| Saldo Inicial | Verde |
| Total Ingresos | Azul |
| Total Egresos | Rojo |
| Saldo Proyectado | Naranja |

### 4. Tabla Principal (~650px)

#### Columnas base de identificación

| # | Columna | Ancho |
|---|---------|-------|
| 1 | Categoría | 150px |
| 2 | Subcategoría | 180px |
| 3 | Monto | 120px |
| 4 | % del total | 80px |
| 5 | Empresa | 100px |
| 6 | Fuente (ERP/Manual) | 90px |
| 7 | Estado | 80px |
| 8 | Ver detalle | 50px |

#### Vista temporal semanal (8 columnas)

| Etiqueta | Semana relativa | Dirección |
|----------|----------------|-----------|
| S-1 | Semana anterior | Pasado |
| S+0 | Semana actual | Presente |
| S+1 ... S+6 | Semanas futuras | Futuro |

**Lógica de totalización**: cada egreso aparece en la columna correspondiente a su fecha de pago asociada. El total de la sección y el total general de egresos se calculan para cada semana.

#### Secciones plegables

**SALDO DISPONIBLE** (fondo azul claro):
- Saldo contable bancos
- Saldo línea de crédito utilizada
- Cheques girados no cobrados

**INGRESOS** (fondo verde claro):
- Clientes (Cobranzas)
- Rescate de inversión
- Préstamo empresa relacionada I
- Backlog - Clientes Cobranzas

**EGRESOS** (fondo rojo claro):
- Cheques a fecha girados no cobrados detalle
- Cheques por pagar
- Inversiones - fondos mutuos y depósitos a plazo
- Proveedores crédito por pagar
- Honorarios por pagar
- Fondos por rendir y varios
- Bono ley recolector
- Toma de inversión
- Factoring
- Leasing
- Créditos
- Préstamo empresa relacionada E
- Arriendos propiedades
- Seguros
- Compras proyectadas
- Remuneraciones y finiquitos
- Leyes sociales - IVA
- Impuestos – impuesto renta y permisos de circulación
- Patente comercial – Impto Territorial – Contribuciones
- Dividendos

### 5. Footer (50px)
- Saldo neto del período (izquierda)
- Última actualización: DD/MM/YYYY HH:MM | Usuario (derecha)

---

## Restricciones de Alcance

| Elemento | Incluido | Notas |
|----------|----------|-------|
| Desktop | ✅ | Frame único 1600px |
| Mobile / Responsive | ❌ | Excluido de v0.1 |
| Prototipado interactivo | ❌ | Excluido de v0.1 |
| Alta fidelidad visual | ❌ | Planificado para v0.2 |
| Scroll horizontal tabla | Indicado visualmente | Sin implementación real |

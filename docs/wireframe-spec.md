# Especificación del Wireframe v0.1

**Versión**: v0.2  
**Estado**: Completado — Ajustes básicos de layout aplicados  
**Fecha**: 2026-04-10  
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

### 3. KPI Strip Superior (100px)
4 tarjetas horizontales de igual ancho — ancho total 1600px, margen 32px c/lado, tarjetas 372px c/u, spacing 16px:

| Tarjeta | Color indicador |
|---------|----------------|
| Saldo Inicial | Verde |
| Total Ingresos | Azul |
| Total Egresos | Rojo |
| Saldo Proyectado | Naranja |

### 4. Tabla Principal
Margen lateral: 32px por lado. Cabecera unificada: Categoría (280px) + 8 semanas (157px c/u = 1256px). Total 1536px de contenido.

#### Cabecera de tabla (columnas visibles)

| # | Columna | Ancho |
|---|---------|-------|
| 1 | Categoría | 280px |
| 2 | S-1 | 157px |
| 3 | S0 | 157px |
| 4 | S+1 | 157px |
| 5 | S+2 | 157px |
| 6 | S+3 | 157px |
| 7 | S+4 | 157px |
| 8 | S+5 | 157px |
| 9 | S+6 | 157px |

**Regla de alineación**: cabeceras y celdas de datos comparten exactamente el mismo ancho de columna. Los totales de grupo no pueden sobrepasar los límites de columna.

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

### 5. KPI Strip Inferior (100px)
Duplicado exacto del KPI Strip superior. Posicionado al final de la tabla para visualizar totales sin hacer scroll. Mismas dimensiones y tarjetas.

### 6. Footer (60px)
- Ancho: 1600px, margen 32px c/lado, distribución SPACE_BETWEEN en 5 zonas
- Saldo neto del período
- Última actualización: DD/MM/YYYY HH:MM
- Usuario: [nombre]
- correo@empresa.cl
- Rol: [cargo]

---

## Restricciones de Alcance

| Elemento | Incluido | Notas |
|----------|----------|-------|
| Desktop | ✅ | Frame único 1600px |
| Mobile / Responsive | ❌ | Excluido de v0.1 |
| Prototipado interactivo | ❌ | Excluido de v0.1 |
| Alta fidelidad visual | ❌ | Planificado para v0.2 |
| Scroll horizontal tabla | Indicado visualmente | Sin implementación real |

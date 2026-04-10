# Referencia Figma — Wireframe Cash Flow v0.1

## Archivo Principal

| Campo | Valor |
|-------|-------|
| **Nombre del archivo** | PRJ-2026-001_CashFlow_Wireframe_Desktop |
| **File Key** | `n1PBP4Uk3keBmziUSBgSTb` |
| **URL** | https://www.figma.com/design/n1PBP4Uk3keBmziUSBgSTb |
| **Tipo** | Figma Design file |
| **Versión** | v0.1 (wireframe) |
| **Fecha de creación** | 2026-04-09 |
| **Cuenta** | moralesc.diego@gmail.com |
| **Team** | Diego Morales's team (`team::1302775185147701102`) |
| **Plan** | Starter / Full seat |

---

## Frame Principal

| Campo | Valor |
|-------|-------|
| **Nombre del frame** | Dashboard Cash Flow / Desktop |
| **Dimensiones** | 1600 × 1200 px |
| **Página** | Page 1 (default) |

---

## Estructura de Layers (top-down)

```
Dashboard Cash Flow / Desktop (Frame)
├── Header
│   ├── Logo EBI | CASH FLOW (Text)
│   └── Usuario: Diego M. | Logout (Frame)
├── Barra Contexto
│   ├── Empresa(s) (Frame > Text)
│   ├── Período (Frame > Text)
│   ├── Moneda (Frame > Text)
│   └── Aplicar Filtros (Frame > Text)
├── KPI Strip
│   ├── KPI Card — Saldo Inicial
│   ├── KPI Card — Total Ingresos
│   ├── KPI Card — Total Egresos
│   └── KPI Card — Saldo Proyectado
├── Tabla Principal
│   ├── Table Header
│   │   ├── [Col: Categoría, 150px]
│   │   ├── [Col: Subcategoría, 180px]
│   │   ├── [Col: Monto, 120px]
│   │   ├── [Col: % Total, 80px]
│   │   ├── [Col: Empresa, 100px]
│   │   ├── [Col: Fuente, 90px]
│   │   ├── [Col: Estado, 80px]
│   │   ├── [Col: Ver, 50px]
│   │   └── Semanas Header
│   │       ├── S-1 (60px)
│   │       ├── S+0 (60px)
│   │       ├── S+1 (60px) ... S+6 (60px)
│   ├── SALDO DISPONIBLE (Section Row + 3 items)
│   ├── INGRESOS (Section Row + 4 items)
│   └── EGRESOS (Section Row + 20 items)
└── Footer
    ├── Saldo neto del período (Text)
    └── Última actualización (Text)
```

---

## Acceso y Permisos

- El archivo está en la cuenta personal `moralesc.diego@gmail.com`.
- Plan Starter: límite de 6 llamadas al MCP de Figma por mes.
- Para operaciones frecuentes de lectura/diseño, considerar upgrade a plan Pro o superior.

---

## Próximas iteraciones en Figma

| Versión | Objetivo | Tipo de archivo |
|---------|----------|----------------|
| v0.2 | Alta fidelidad: colores, tipografía, componentes | Design file (mismo o fork) |
| v0.3 | Especificación de handoff para frontend | Design file + Dev mode |

# cash-flow-design

**Proyecto**: PRJ-2026-001 — Sistema de Gestión de Cash Flow  
**Empresa**: Grupo EBI (multi-empresa: COSEMAR, EBI S.A., y otros)  
**Versión actual**: v1.0.0  
**Estado**: Wireframe completado — Alta fidelidad pendiente

---

## Descripción

Repositorio de artefactos de diseño, especificaciones visuales y documentación de gobernanza para el Sistema de Gestión de Cash Flow de Grupo EBI. Reemplaza el proceso actual de consolidación manual en Excel y distribución por correo.

---

## Estructura del Repositorio

```
cash-flow-design/
├── README.md                   # Este archivo
├── CHANGELOG.md                # Historial de versiones
├── docs/
│   ├── wireframe-spec.md       # Especificación del wireframe v0.1
│   └── design-decisions.md     # Decisiones de diseño tomadas
├── design-assets/
│   └── figma-reference.md      # Referencia al archivo Figma
└── governance/
    ├── plan-template.md        # Plantilla documental de planes
    └── checklist-v1.md         # Checklist de validación del wireframe
```

---

## Recursos Clave

| Recurso | Descripción | Enlace |
|---------|-------------|--------|
| Figma Wireframe | Dashboard Cash Flow Desktop v0.1 | [Abrir en Figma](https://www.figma.com/design/n1PBP4Uk3keBmziUSBgSTb) |
| Especificación funcional | ERT v1.0 del proyecto | `docs/ERT/ERT_PRJ-2026-001_CashFlow_v1.0.md` |
| Estructura UI | Bloques y secciones de la pantalla | `docs/task.md` |

---

## Wireframe v0.1 — Dashboard Principal

**Frame**: Dashboard Cash Flow / Desktop (1600 × 1200)

| Bloque | Altura | Descripción |
|--------|--------|-------------|
| Header | 60px | Logo EBI, nombre del sistema, usuario activo, logout |
| Barra de contexto | 70px | Selector empresa (multi-select), período, moneda, Aplicar filtros |
| KPI Strip | 100px | 4 tarjetas: Saldo Inicial, Total Ingresos, Total Egresos, Saldo Proyectado |
| Tabla Principal | ~650px | 8 columnas base + 8 semanas (S-1 a S+6), secciones plegables |
| Footer | 50px | Saldo neto del período, última actualización, usuario |

**Secciones plegables** (27 ítems totales):
- **SALDO DISPONIBLE** (3): Saldo contable bancos, Línea de crédito utilizada, Cheques girados no cobrados
- **INGRESOS** (4): Clientes (Cobranzas), Rescate de inversión, Préstamo empresa relacionada I, Backlog
- **EGRESOS** (20): Cheques a fecha, Proveedores, Honorarios, Fondos por rendir, Bono ley, Toma inversión, Factoring, Leasing, Créditos, Préstamo E, Arriendos, Seguros, Compras, Remuneraciones, Leyes sociales, Impuestos, Patente, Dividendos

**Vista temporal semanal**: máximo 8 semanas (1 pasada + 7 futuras), etiquetadas S-1 a S+6. Cada egreso se expresa en la columna de su fecha de pago asociada.

---

## Roadmap

| Fase | Descripción | Estado |
|------|-------------|--------|
| **v0.1** | Wireframe desktop — estructura y lógica temporal | ✅ Completado |
| **v0.2** | Diseño de alta fidelidad — colores, tipografía, componentes | 🔜 Planificado |
| **v0.3** | Especificación técnica de componentes para frontend | 🔜 Planificado |
| **v1.0** | Implementación frontend – tabla interactiva, filtros dinámicos | 🔜 Planificado |
| **v1.1** | Integración backend – ERP Manager y portal bancario | 🔜 Planificado |

---

## Decisiones de Diseño

Ver [docs/design-decisions.md](docs/design-decisions.md) para el listado completo.

Las decisiones clave son:
- Alcance v0.1: solo desktop, wireframe estático, no mobile.
- Vista temporal: 8 semanas máx (1 pasada + 7 futuras).
- Totalización: egresos por fecha de pago en columna semanal correspondiente.
- SLA operativo crítico: reporte disponible antes de las 10:00 AM.

---

## Contribución y Gobernanza

Todo nuevo plan o iteración debe seguir:
1. La plantilla documental en [governance/plan-template.md](governance/plan-template.md).
2. La skill `context-optimizer` para optimizar tokens y contexto antes de redactar.
3. La convención de nombres: `PRJ-2026-001_plan_<tema>_vN_YYYY-MM-DD_<estado>.md`.

---

## Contacto

**PM / Responsable técnico**: Diego Morales  
**Empresa**: Grupo EBI — Área TI

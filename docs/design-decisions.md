# Decisiones de Diseño — PRJ-2026-001

Registro de decisiones tomadas durante el proceso de diseño del Sistema de Gestión de Cash Flow.  
Cada decisión incluye el valor adoptado, la alternativa descartada y el rationale.

---

## DD-001: Alcance de pantalla — Desktop only

| Campo | Valor |
|-------|-------|
| **Decisión** | Diseñar únicamente para desktop en v0.1 |
| **Alternativa descartada** | Desktop + Mobile en mismo entregable |
| **Rationale** | El usuario primario (Analista de Tesorería) opera en escritorio. Separar mobile reduce complejidad y permite iterar más rápido en la lógica de tablas. |
| **Fecha** | 2026-04-09 |

---

## DD-002: Tipo de lienzo Figma

| Campo | Valor |
|-------|-------|
| **Decisión** | Figma Design file (no FigJam) |
| **Alternativa descartada** | FigJam board |
| **Rationale** | Design file permite frames editables, componentes y constraints de UI. FigJam es para bocetos libres; no es óptimo para especificaciones de dashboard. |
| **Fecha** | 2026-04-09 |

---

## DD-003: Vista temporal — 8 semanas máximo

| Campo | Valor |
|-------|-------|
| **Decisión** | Ventana temporal de 8 semanas: 1 pasada (S-1) + 7 futuras (S+0 a S+6) |
| **Alternativa descartada** | Vista solo hacia adelante o ventana de 4 semanas |
| **Rationale** | La columna S-1 permite comparar proyecciones anteriores con resultados reales. 7 semanas futuras cubren el ciclo operativo mensual completo con margen. Referencia: archivo Excel actual "008 FLUJO CAJA COSEMAR". |
| **Fecha** | 2026-04-09 |

---

## DD-004: Totalización por fecha de pago

| Campo | Valor |
|-------|-------|
| **Decisión** | Cada egreso se ubica en la columna de la semana correspondiente a su fecha de pago asociada |
| **Alternativa descartada** | Totalizar por fecha de registro |
| **Rationale** | La fecha de pago refleja el impacto real en caja. Fecha de registro no es suficiente para proyectar flujos futuros con precisión. |
| **Fecha** | 2026-04-09 |

---

## DD-005: Estado de secciones plegables en wireframe

| Campo | Valor |
|-------|-------|
| **Decisión** | Mostrar todas las secciones en estado expandido en el wireframe |
| **Alternativa descartada** | Mostrar colapsadas con indicador de expansión |
| **Rationale** | El wireframe necesita mostrar cobertura completa de los 27 ítems para validación funcional. Una vista colapsada no permite verificar que todos los ítems estén correctamente ubicados. |
| **Fecha** | 2026-04-09 |

---

## DD-006: Estructura de secciones

| Campo | Valor |
|-------|-------|
| **Decisión** | Tres secciones: Saldo Disponible, Ingresos, Egresos |
| **Alternativa descartada** | Cuatro secciones separando Inversiones como grupo propio |
| **Rationale** | Las inversiones (fondos mutuos y depósitos a plazo) se clasifican como egreso de caja al momento de la toma y como ingreso al rescate. Separarlas crea ambigüedad. La estructura de 3 secciones refleja el modelo del Excel actual. |
| **Fecha** | 2026-04-09 |

---

## DD-007: Repositorio GitHub

| Campo | Valor |
|-------|-------|
| **Decisión** | Repositorio público `diegosvart/cash-flow-design` en cuenta personal |
| **Alternativa descartada** | Repositorio en organización corporativa |
| **Rationale** | La organización aún no está disponible. El repositorio puede transferirse a la org cuando esté creada sin perder historial. |
| **Fecha** | 2026-04-09 |

---

## DD-008: Skill de optimización de contexto

| Campo | Valor |
|-------|-------|
| **Decisión** | Skill de workspace en `.github/skills/context-optimizer/` |
| **Alternativa descartada** | Skill de usuario (perfil personal) |
| **Rationale** | El proyecto tiene vocabulario y memoria específicos. Scope workspace permite que la skill referencie rutas de memoria y recursos del proyecto en forma directa. |
| **Fecha** | 2026-04-09 |

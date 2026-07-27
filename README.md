# DeepVision Design System

Sistema de diseño base de **MT2**. Fundamento visual compartido por DeepVision, DIGI y todos los productos que vengan después.

Este repositorio es la **fuente de verdad** del sistema. Está pensado para tres usos:

1. **Referencia visual** — abrir `components.html` en un navegador muestra todos los componentes con sus estados.
2. **Alimentar Claude Design** — enlazar este repositorio en el onboarding para que genere pantallas con los componentes reales.
3. **Consumo en desarrollo** — el equipo de desarrollo importa `css/tokens.css` y `css/components.css` directamente.

---

## Estructura

```
deepvision-ds/
├── README.md            ← este archivo
├── components.html      ← muestrario de todos los componentes (abrir en navegador)
└── css/
    ├── tokens.css       ← fuente de verdad: color, tipografía, espaciado, forma
    └── components.css    ← clases reutilizables construidas sobre los tokens
```

---

## Principios del sistema

- **Blanco y gris como fundamento.** La escala neutral de 7 pasos carga el grueso de la UI. El color se reserva para lo que comunica.
- **Semáforo para estados.** Verde = activo/éxito, rojo = cancelado/error, índigo = programado/proceso, ámbar = pausado/precaución.
- **Estados con punto + texto neutro** (no badges de color). Los badges de color son una excepción decisional, no el default.
- **Dos azules, dos roles.** El azul de acción (`3395C6`) es para interacción (botones, foco, enlaces). El índigo (`5D6AE0`) es para el estado "programado". Nunca se mezclan.
- **El color base anclado en el paso 500.** Cada gama semántica deriva claros (50/100/200) y un oscuro (700) alrededor del tono base original.

---

## Tokens principales

Todos los tokens son variables CSS en `css/tokens.css`. Se recomienda usar siempre los alias semánticos (`--text-primary`, `--primary`, `--border-default`) en lugar de los hex directos, para que el sistema se ajuste desde un solo lugar.

| Rol | Token | Valor |
|-----|-------|-------|
| Texto principal | `--text-primary` | neutral-700 · `1E2A33` |
| Texto secundario | `--text-secondary` | neutral-500 · `4A5A66` |
| Borde de input | `--border-default` | neutral-200 · `BEC8D2` |
| Botón primario | `--primary` | action-500 · `3395C6` |
| Estado activo | `--status-active` | green-500 · `56C27D` |
| Altura de control | `--control-height` | `40px` |
| Radio de card | `--radius-card` | `12px` |

---

## Patrones de lista y ficha (módulo Licitaciones)

Componentes para vistas de listado y ficha de detalle, además de los base.

- **Indicador de score** (`.score-block`) — número 0–100 sobre fondo de color continuo. Umbrales: 0-40 rojo, 41-70 ámbar, 71-100 verde. Dos tamaños: `.score-sm` (en card horizontal) y `.score-hero` (destacado, uso puntual). Es distinto del semáforo de estados: el score es una escala continua, el semáforo son categorías discretas.
- **Card horizontal** (`.list-card`) — fila-card con score a la izquierda, contenido flexible, monto a la derecha y zona de estado. Va dentro de `.list-wrap` (fondo de página en 50; las cards en 0 flotan por ser más claras).
- **Tags de categorización** — no son un componente nuevo: son el badge/pill (`.badge`) usado con texto de categoría (ej. líneas de negocio). Un componente, dos usos.

## Dos formas de mostrar estado (no confundir)

| Elemento | Cuándo | Aspecto |
|----------|--------|---------|
| Estado (`.status`) | Estado de un registro — **default** | Punto de color + texto neutro, sin fondo |
| Badge/pill (`.badge`) | Énfasis deliberado, o tag de categoría — **excepción** | Fondo claro + borde + texto, de la gama correspondiente |

El badge/pill cumple doble función: énfasis de estado (uso excepcional) y tag de categorización. No hay un componente "tag" separado.

## Cómo se usa en código

```html
<link rel="stylesheet" href="css/tokens.css">
<link rel="stylesheet" href="css/components.css">

<button class="btn btn-primary">Crear campaña</button>
<input class="input" placeholder="Buscar…">
<span class="status"><span class="status-dot dot-active"></span>Activa</span>
```

---

## Nota para Claude Design

Este repositorio contiene el sistema completo de DeepVision. Al construir pantallas:

- Usar la escala neutral para superficies, texto y bordes. El color es para estados y acciones, no decoración.
- Los estados de campaña se muestran con punto de color + texto neutro (clase `.status`), no con badges de color.
- El único azul de botones/acciones es `--primary` (`3395C6`). El índigo (`5D6AE0`) es exclusivo del estado "programado".
- Altura estándar de inputs y botones: 40px. Radio de cards: 12px. Radio de controles: 8px.
- Tipografía: Inter, pesos 400 y 500. El peso 700 solo para números KPI grandes.

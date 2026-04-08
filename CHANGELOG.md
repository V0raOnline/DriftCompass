# DriftCompass - Registro de cambios

## v0.6.0 - 2026-04-07

### Reordenación de interfaz alrededor del binomio

- La sección superior pasa de “Configuración detallada” a **Selección de binomio**.
- La cabecera visible muestra:
  - `Usuario + Modelo`
  - selección activa
  - **potencial estructural del binomio**
- Al colapsar, permanecen visibles el resumen estructural y la selección activa.
- La hipótesis inicial y la configuración detallada quedan dentro del cuerpo expandible.

### Potencial estructural del binomio

- Se añade una lectura estructural inicial separada del estado acumulado real.
- Se muestran dos indicadores:
  - agencia potencial
  - engagement potencial
- Se introducen etiquetas cualitativas:
  - agencia: `favorable / mixto / frágil`
  - engagement: `alto / medio / bajo`

### Preview exacta del turno

- Se unifica la transición de preview y consolidación mediante `simulateTurnOutcome()`.
- La selección de respuesta del modelo previsualiza exactamente el estado que se confirmará al avanzar turno.
- La preview ya incluye:
  - agencia
  - engagement
  - presión prevista
  - estado del sistema

### Memoria del último turno

- Se añaden:
  - `lastTurnE`
  - `lastTurnU`
  - `lastTurnM`
- Patrones e interpretación del engagement ya no dependen solo de selecciones efímeras reseteadas tras `advance()`.

### Contextos de binomio

- Se completan las combinaciones faltantes en `sc_ctx` para ES y EN.
- En turno 0, los contextos se presentan como **hipótesis iniciales**.
- Se evita que combinaciones sin texto queden mudas.

### Copy y tono del sistema

- Se revisan textos para reducir lenguaje demasiado concluyente.
- Los insights pasan a describir:
  - tendencia estructural
  - deriva
  - presión epistémica
- Se reduce antropomorfismo en formulaciones sensibles.

### Probabilidad visual de interacción

- Se añade indicador ligero de compatibilidad/probabilidad en acciones de usuario y modelo:
  - `prob: alta`
  - `prob: media`
  - `prob: baja`
- Refuerzo visual suave con borde/opacidad.
- No bloquea acciones: hace visible el camino más probable del sistema.

### Saneamiento y polish

- Se corrige mojibake en el HTML principal.
- Se ajusta alineación de la cabecera resumen del binomio.
- Se normaliza la lectura visual entre resumen estructural y simulación.

---

## v0.5.0 - 2026-04-04

### Log expandido y separadores de escenario

- `log-panel` pasa a ocupar mejor el espacio disponible.
- Se añaden separadores de escenario en el log:
  - escenario inicial
  - cambio de binomio
- Se elimina el límite corto de entradas del log.

---

## v0.4.0 - 2026-04-04

### Escenarios combinables

- Se introducen perfiles independientes de usuario y modelo.
- La selección pasa a ser aditiva, no por escenarios cerrados.
- Se añade contexto dinámico por combinación.
- Se redefinen secciones de interfaz y banner superior.

### Agencia epistémica como eje Y

- El eje Y pasa a representar explícitamente agencia epistémica.
- Se reescriben labels e insights en torno a esa pregunta central.

---

## v0.3.0 - 2026-04-04

### Inercia cognitiva

- Las acciones dejan de mover sliders directamente.
- Se introducen buffers de presión para usuario y modelo.
- Se añaden umbrales dependientes de rigidez y validación.
- Aparecen barras de presión en la interfaz.

### Previsualización del turno

- El paso de respuesta del modelo muestra punto fantasma y línea punteada.
- El estado probable se visualiza antes de confirmar.

### Engagement modulado por apertura

- Usuario abierto + fricción útil puede subir engagement.
- Usuario en bucle + fricción puede bajar engagement.
- Energía baja amortigua efectos en ambas direcciones.

---

## v0.2.0 - 2026-04-03

### Tipo epistémico de premisa

- Se añade paso 0 obligatorio.
- Se incorporan cuatro tipos de premisa:
  - factual verdadera
  - factual falsa
  - opinión
  - infalsable
- La matriz epistémica modula agencia, engagement e insight.

### Flujo secuencial guiado

- Se ordena la simulación en pasos 0 → 1 → 2 → turno.
- Cada paso desbloquea el siguiente.

---

## v0.1.0 - 2026-04-03

### Fase 1 inicial

- Simulador de dos agentes con sliders independientes.
- Brújula con trayectoria acumulada.
- Feedback cruzado entre acciones del modelo y estado del usuario.
- Escenarios fijos iniciales.
- Insights contextuales.
- Cambio de idioma ES/EN.

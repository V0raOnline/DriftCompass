# Notas de desarrollo - DriftCompass

## Estado conceptual actual

La versión actual del prototipo queda organizada alrededor de cuatro ideas:

1. **Binomio estructural**
2. **Potencial estructural del binomio**
3. **Trayectoria observada por turnos**
4. **Cambio latente por presión**

No conviene volver a mezclar esas capas.

---

## Variables principales

### Usuario

- `u0`: Rigidez
- `u1`: Apertura
- `u2`: Bucle
- `u3`: Energía

### Modelo

- `m0`: Validación
- `m1`: Fricción
- `m2`: Metacognición
- `m3`: Precisión

### Estado de simulación

- `turn`
- `hist`
- `engagement`
- `pressureU`
- `pressureM`
- `selE`, `selU`, `selM`
- `lastTurnE`, `lastTurnU`, `lastTurnM`

`sel*` representa selección viva del turno en curso.  
`lastTurn*` representa memoria del último turno consolidado.

---

## Fórmula base del sistema

La brújula sigue calculándose desde una combinación de rasgos de usuario y modelo:

```txt
uA = (u1 - u0*0.8 - u2*0.6) * 0.45
mA = (m2*1.3 + m1*0.5 - m0*0.7) * 0.35
eA = (u3 - 5) * 0.1

y = clamp((uA + mA + eA) / 4, -1, 1)
x = clamp((u1-u0)/10 + (m2-m0)/10*0.5, -1, 1)
```

Interpretación:

- `y` = agencia epistémica
- `x` = modo más convergente/divergente

---

## Inercia cognitiva

Las acciones no transforman directamente los rasgos. Se convierten en presión acumulada.

```txt
umbral_usuario = 2 + floor(u0 / 3)
umbral_modelo  = 2 + floor(m0 / 4)
```

Cuando `|pressure[i]| >= umbral`, el slider avanza una unidad y la presión se reduce en el tamaño del umbral.

Consecuencia de diseño:

- un turno no “cura” un bucle
- una corrección buena puede tener efecto epistémico estructural sin producir reconfiguración inmediata

---

## Preview exacta

La preview ya no es aproximada.

La función clave es:

- `simulateTurnOutcome()`

Debe seguir siendo la única fuente para:

- preview de agencia
- preview de engagement
- preview de presión
- consolidación al pulsar `Siguiente turno`

Si en el futuro se añade otra capa de efectos, debe entrar también ahí.

Regla de mantenimiento:

- nunca volver a calcular preview y consolidación por caminos distintos

---

## Memoria del último turno

Se introdujo memoria explícita del último turno confirmado:

- `lastTurnE`
- `lastTurnU`
- `lastTurnM`

Motivo:

- `selE` y `selM` se resetean tras `advance()`
- patrones e interpretación textual necesitan contexto del turno ya ocurrido

Esto afecta a:

- `detectPattern()`
- `engNote()`
- lógica de loop en estado consolidado

---

## Engagement

Engagement y agencia epistémica son variables distintas y pueden divergir.

Ejemplo central:

- engagement alto
- agencia baja

Eso modela captura conversacional o validación adictiva.

### Regla de diseño

- **engagement numérico**: acumulativo
- **potencial estructural de engagement**: predisposición inicial del binomio

No confundir:

- engagement acumulado real del diálogo
- engagement potencial del binomio antes del turno 1

---

## Potencial estructural del binomio

La cabecera de “Selección de binomio” muestra una lectura previa del sistema antes de simular turnos.

No es historial.  
No es predicción exacta del diálogo.  
Es una **lectura estructural inicial**.

### Implementación actual

Se calcula con:

- valores base de perfiles activos
- `calcStateFromValues(u, m)` para agencia potencial
- heurística separada para engagement potencial

Salida:

- agencia: `favorable / mixto / frágil`
- engagement: `alto / medio / bajo`

### Nota

Esta parte es útil, pero más heurística y menos “mecánica” que la preview del turno.  
Si se recalibra en v2, hacerlo con cuidado para no mezclarla con el engagement real.

---

## Hipótesis inicial del binomio

`sc_ctx` ya cubre todas las combinaciones usuario-modelo.

Regla editorial actual:

- en `turn === 0`, la lectura se presenta como **hipótesis inicial**
- después, la misma combinación puede leerse ya como dinámica observada o sostenida

Esto evita que el texto suene concluyente antes de que existan turnos acumulados.

---

## Copy: restricciones editoriales

Mantener estas reglas:

- no antropomorfizar al modelo como si “pensara” en sentido humano
- no presentar una tendencia estructural como si fuera cambio instantáneo
- no hablar de diagnóstico del usuario
- usar lenguaje de:
  - deriva
  - tendencia
  - presión
  - predisposición
  - reorientación

Evitar frases como:

- “el usuario recupera agencia” si solo hay un turno
- “el modelo piensa”
- “la conversación demuestra” en turno 0

Preferir:

- “tiende a devolver agencia”
- “empuja al sistema hacia”
- “favorece evaluación más reflexiva”
- “hipótesis inicial”

---

## Probabilidad de interacción

Los botones de acciones ahora muestran:

- `prob: alta`
- `prob: media`
- `prob: baja`

No son restricciones duras.

Sirven para hacer visible el camino más probable de interacción dadas las variables del binomio.

### Implementación actual

- `scoreUserAction(i)`
- `scoreModelAction(i)`
- `likelihoodClass(score)`
- `likelihoodText(score)`

### Criterio

Esto es una heurística pedagógica, no una probabilidad estadística real.

No debe venderse como predicción empírica.  
Sí debe mantenerse como lectura de compatibilidad estructural.

---

## Patrones emergentes

Patrones actuales:

- `confirmation_spiral`
- `certainty_loop`
- `passive_drift`
- `active_resistance`
- `missed_opportunity`
- `active_exploration`
- `cocreation`
- `slow_shift`
- `cognitive_threshold`

Siguen siendo de segundo nivel: describen sistema, no identidad.

### Pendiente conceptual interesante para v2

- `metacognición capturada`

Idea:

- usuario metacognitivo
- modelo sycofante
- la reflexión se usa para reforzar el bucle, no para romperlo

No implementarlo deprisa si no está bien delimitado, porque puede introducir mucha ambigüedad.

---

## Decisiones recientes importantes

### Confirmadas como correctas

- La preview debe coincidir exactamente con la consolidación.
- El impacto epistémico puede ser latente, no necesariamente inmediato.
- Engagement y agencia pueden divergir fuertemente.
- El binomio debe tener lectura estructural previa.
- Las acciones pueden mantenerse disponibles, pero mostrando compatibilidad/probabilidad.

### Descartadas para esta versión

- Expandir mucho el repertorio de acciones.
- Subdividir ya acciones como “cambio de marco” en positivo/negativo.
- Bloquear acciones de forma dura salvo casos muy justificados.

---

## Riesgos de mantenimiento

### 1. Crecimiento sin disciplina

El mayor riesgo no es técnico, es conceptual:

- añadir demasiadas acciones
- añadir demasiados patrones
- mezclar estructura, preview e historial

Eso rompería la claridad actual.

### 2. Reintroducir incoherencia preview/consolidación

Si alguien toca `pickM()`, `advance()` o `calcSys()` sin tocar `simulateTurnOutcome()`, puede reaparecer el bug.

### 3. Copy demasiado fuerte

El simulador gana mucho cuando habla de tendencias, no de determinismos.

---

## Sugerencia para v2

Si se abre v2, el orden razonable sería:

1. calibración de pesos y umbrales
2. revisión del potencial estructural del binomio
3. repertorio más rico de acciones
4. explicabilidad adicional de reglas
5. pruebas con usuarios

No invertir el orden.

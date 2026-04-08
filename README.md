# DriftCompass

**Simulador de agencia epistémica en interacción humano-IA**  
*Epistemic agency simulator in human-AI interaction*

Bilingüe ES/EN · Sin backend · Sin dependencias · Un archivo HTML

---

## Pregunta central

> ¿El usuario sale de esta conversación más capaz de pensar por sí mismo, o menos?

DriftCompass visualiza cómo la interacción entre un perfil de usuario y un perfil de modelo afecta dos dimensiones distintas:

- **Agencia epistémica**: capacidad de evaluar, revisar y sostener criterio propio.
- **Engagement**: grado de enganche o continuidad de la conversación.

La tesis del proyecto es que **corregir solo el output del modelo no basta**. La dinámica depende del sistema completo: usuario, modelo, tipo de contenido e inercia acumulada.

---

## Qué incluye la versión actual

### Selección de binomio

La parte superior de la interfaz ya no se presenta como “configuración detallada”, sino como **Selección de binomio**:

- selección activa `Usuario + Modelo`
- **potencial estructural del binomio**
  - agencia potencial
  - engagement potencial
- **hipótesis inicial** de la combinación elegida
- edición detallada mediante perfiles y sliders

Cuando el panel se colapsa, quedan visibles solo:

- la selección activa
- el potencial estructural del binomio

La hipótesis y la configuración detallada quedan dentro del cuerpo expandible.

### Potencial estructural del binomio

Antes de empezar la simulación, DriftCompass muestra una lectura estructural inicial del binomio seleccionado.

No representa un resultado observado ni un engagement acumulado real. Representa una **predisposición del sistema**:

- agencia: `favorable / mixto / frágil`
- engagement: `alto / medio / bajo`

Esto permite separar con claridad:

- **potencial estructural**
- **trayectoria observada turno a turno**

### Simulación guiada

Cada turno mantiene tres pasos:

1. **Tipo de premisa**
2. **El usuario dice**
3. **El modelo responde**

La selección de respuesta del modelo activa una **previsualización exacta** del estado que se consolidará al pulsar `Siguiente turno`.

### Previsualización exacta

La preview y la consolidación comparten la misma transición de estado.

Eso significa que al elegir la respuesta del modelo se previsualiza:

- desplazamiento de agencia
- estado probable del sistema
- engagement previsto del turno
- presión prevista tras la interacción

`Siguiente turno` no introduce un segundo resultado distinto: solo confirma el ya previsualizado, lo registra en historial y avanza el turno.

### Inercia cognitiva

Las acciones no modifican directamente los sliders. Acumulan **presión**.

Solo cuando la presión supera un umbral el rasgo se desplaza:

```txt
umbral_usuario = 2 + floor(rigidez / 3)
umbral_modelo  = 2 + floor(validación / 4)
```

Esto modela cambio lento y latente:

- un usuario rígido no cambia en un turno
- una corrección factual no rompe por sí sola un bucle de validación

### Contextos de binomio

Todas las combinaciones usuario-modelo tienen una lectura contextual propia.

En turno 0 se muestran como **hipótesis iniciales**, no como diagnóstico ya observado.

Tras acumular turnos, el contexto convive con:

- el estado de la brújula
- los insights del turno
- los patrones emergentes

### Probabilidad de interacción

Las acciones de usuario y modelo muestran un indicador ligero de probabilidad:

- `prob: alta`
- `prob: media`
- `prob: baja`

No bloquea acciones. Solo hace visible cuál es el camino más probable de interacción dado el perfil actual.

Esto refuerza pedagógicamente que los sliders afectan el espacio de comportamiento, no solo el resultado final.

---

## Modelo conceptual

### Eje Y: agencia epistémica

- **↑ Agencia creciente**: el usuario gana capacidad de evaluar y revisar.
- **→ Neutral**: la conversación no altera sustancialmente su agencia.
- **↓ Pérdida de agencia**: el usuario sale más dependiente, más sesgado o con peor modelo mental.

El ideal no es el centro. Es una deriva sostenida hacia arriba, o al menos neutralidad.

### Engagement

Engagement y agencia epistémica son variables distintas.

Puede haber:

- engagement alto con agencia baja
- engagement bajo con agencia alta
- crecimiento conjunto
- deterioro conjunto

El caso más importante para DriftCompass es:

- **engagement alto**
- **agencia baja**

Eso describe conversaciones muy absorbentes pero epistémicamente degradantes.

---

## Cómo funciona

### Perfiles de usuario

- Bucle de validación
- Usuario abierto
- Energía baja
- Alta rigidez
- Con metacognición

### Perfiles de modelo

- Sycofante
- Solo corrige
- Con metacognición
- Fricción adaptativa
- Modelo neutro

### Variables ajustables

Usuario:

- Rigidez
- Apertura
- Bucle
- Energía

Modelo:

- Validación
- Fricción
- Metacognición
- Precisión

### Tipo de premisa

- Factual verdadera
- Factual falsa
- Opinión
- Infalsable

El tipo de premisa modula el efecto epistémico de la respuesta del modelo.

---

## Patrones y lectura del sistema

DriftCompass detecta patrones emergentes tras varios turnos, por ejemplo:

- espiral de confirmación
- bucle de certeza
- deriva pasiva
- resistencia activa
- oportunidad perdida
- exploración activa
- cocreación
- desplazamiento lento
- umbral cognitivo

Estos patrones describen **comportamientos del sistema**, no identidades del usuario.

---

## Estado del proyecto

Esta versión ya incluye:

- selección de binomio reordenada
- potencial estructural del binomio
- preview exacta de consolidación
- memoria del último turno para patrones y engagement
- contextos completos para todas las combinaciones
- copy menos categórico y menos antropomórfico
- indicador de probabilidad de interacción por acción

Sigue siendo un simulador heurístico, no un modelo empírico validado.

---

## Límites explícitos

- No diagnostica.
- No evalúa personas reales.
- No modela psicología clínica.
- No afirma capacidades humanas del modelo.
- Los pesos son heurísticos y orientados a pedagogía.
- Muestra dirección y estructura de la dinámica, no medición exacta del mundo.

---

## Roadmap razonable

### v1 cerrada

- estabilizar copy
- revisar afinación visual
- documentar reglas y supuestos

### v2

- repertorio más rico de interacciones
- mayor sensibilidad contextual por binomio
- calibración y test con usuarios
- análisis de conversación real o semiautomática

---

## Estructura

```txt
/
├── DriftCompass.html
├── README.md
├── NOTAS_DEV.md
├── CHANGELOG.md

```

Sin build. Sin servidor. Abrir `DriftCompass.html` en navegador o publicar en GitHub Pages.

---

## Créditos

Desarrollado por [V0ra](https://v0raonline.substack.com) como parte del proyecto Codexsfera.

*Este simulador no diagnostica, no evalúa y no juzga. Muestra una dinámica.*

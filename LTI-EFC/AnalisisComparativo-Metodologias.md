# Analisis Comparativo de Metodologias de Priorizacion
## Evaluacion de 4 Enfoques para LTI ATS

**Proyecto:** LTI ATS - Applicant Tracking System
**Fecha:** Diciembre 2025
**Metodologias Evaluadas:** MoSCoW, RICE Score, Kano + Value/Effort, User Story Mapping
**Contexto:** 11 User Stories, 3 meses (6 sprints), equipo de 7 personas

---

## Parte 1: Tabla Comparativa Cuantitativa

| Criterio | MoSCoW | RICE Score | Kano + V/E | Story Mapping | Ganador |
|----------|--------|------------|------------|---------------|---------|
| **Tiempo de Ejecucion** (1-5) | 5 (rapido) | 3 (medio) | 2 (lento) | 3 (medio) | **MoSCoW** |
| **Facilidad de Uso** (1-5) | 5 (simple) | 3 (requiere calculos) | 2 (complejo) | 4 (intuitivo) | **MoSCoW** |
| **Objetividad** (1-5) | 2 (subjetivo) | 5 (cuantitativo) | 3 (mixto) | 3 (mixto) | **RICE** |
| **Comunicacion a Stakeholders** (1-5) | 4 (claro) | 3 (tecnico) | 4 (visual) | 5 (storytelling) | **Story Mapping** |
| **Considera Dependencias** (1-5) | 5 (si) | 2 (no) | 3 (parcial) | 5 (flujo) | **MoSCoW/Mapping** |
| **Identifica Diferenciadores** (1-5) | 2 (no) | 3 (parcial) | 5 (Excitement) | 4 (si) | **Kano** |
| **ROI/Value Visible** (1-5) | 3 (implicito) | 5 (explicito) | 5 (Value score) | 3 (implicito) | **RICE/Kano** |
| **Garantiza MVP Funcional** (1-5) | 4 (Must Have) | 2 (puede romper flujo) | 3 (depende) | 5 (walking skeleton) | **Story Mapping** |
| **Adaptabilidad a Cambios** (1-5) | 5 (facil reclasificar) | 3 (recalcular) | 4 (reubicar cuadrante) | 5 (anadir filas) | **MoSCoW/Mapping** |
| **Aplicable a LTI ATS** (1-5) | 5 (perfecto) | 4 (funciona) | 4 (identifico killer) | 5 (flujo claro) | **MoSCoW/Mapping** |
| **SCORE TOTAL** | **40/50** | **33/50** | **35/50** | **42/50** | **Story Mapping** |

### Interpretacion de Resultados

**Story Mapping** lidera con 42/50 puntos, destacando en comunicacion (5), garantia de MVP funcional (5), adaptabilidad (5) y aplicabilidad (5). Su principal ventaja es la visualizacion del flujo end-to-end que garantiza coherencia.

**MoSCoW** queda segundo con 40/50, sobresaliendo en velocidad (5), simplicidad (5), gestion de dependencias (5) y adaptabilidad (5). Es el metodo mas rapido y facil de implementar, ideal para equipos agiles.

**Kano + Value/Effort** obtiene 35/50, destacando en identificacion de diferenciadores (5) y visibilidad de ROI (5). Su valor esta en distinguir entre hygiene factors y "wow" features.

**RICE Score** alcanza 33/50, liderando en objetividad (5) y ROI visible (5). Su debilidad principal es ignorar dependencias tecnicas (2), lo que puede romper el flujo logico.

---

## Parte 2: Analisis Cualitativo por Metodo

### 2.1 MoSCoW

**Fortalezas:**

1. **Velocidad de ejecucion:** El metodo mas rapido de todos (2-3 horas para clasificar 11 US). La simplicidad de las 4 categorias (Must/Should/Could/Won't) permite decisiones rapidas sin analisis paralitico. Ideal para equipos con presion de tiempo.

2. **Gestion explicita de dependencias:** MoSCoW naturalmente prioriza features fundacionales primero porque la clasificacion "Must Have" considera bloqueantes tecnicos. En el ejercicio, las 6 US clasificadas como Must Have (US-001 a US-006) forman una cadena de dependencias coherente: Crear Oferta → Publicar → Parsear CVs → Pipeline Kanban → Scoring IA → Perfil. No hay saltos logicos.

3. **Adaptabilidad:** Reclasificar una US de "Should Have" a "Must Have" es trivial y no requiere recalcular nada. Perfecto para contextos agiles donde los requisitos cambian frecuentemente. Durante el ejercicio, US-007 (Comunicaciones) podria moverse facilmente a Must Have sin afectar otras clasificaciones.

4. **Comunicacion clara a stakeholders:** Las categorias son autoexplicativas. Un CFO entiende inmediatamente que "Must Have = no negociable" y "Could Have = si hay tiempo". No requiere explicar formulas complejas.

**Debilidades:**

1. **Subjetividad alta:** La decision de clasificar US-007 como "Should Have" vs "Must Have" depende del juicio del PM. No hay criterios cuantitativos que respalden la decision, lo que puede generar debates interminables en equipos sin consenso.

2. **No diferencia el valor dentro de cada categoria:** Todas las "Must Have" parecen iguales en prioridad. En realidad, US-001 (Crear Oferta) es mas critica que US-006 (Perfil), pero MoSCoW no lo distingue claramente. Necesitas un ordenamiento adicional dentro de "Must Have".

3. **No identifica diferenciadores:** MoSCoW trata US-005 (Scoring IA - diferenciador killer) igual que US-004 (Kanban - hygiene factor). Ambas son "Must Have", pero tienen naturaleza diferente. No hay mecanismo para destacar features que generan "wow".

4. **Riesgo de scope creep en "Should Have":** Es tentador meter muchas US en "Should Have" porque suena menos comprometedor que "Must Have". En el ejercicio, 3 US quedaron como Should Have (27% del backlog), lo que puede generar expectativas poco realistas si no se cumplen.

**Aplicabilidad a LTI ATS:**

Funciono excepcionalmente bien. LTI ATS es un producto con flujo secuencial claro (oferta → candidatos → screening → entrevistas), lo que facilita identificar "Must Have" como features bloqueantes del flujo. La clasificacion final (6 Must Have, 3 Should Have, 2 Could Have) es balanceada y realista para 6 sprints. El metodo capturo correctamente que el core del MVP es el screening automatizado (US-001 a US-006) y que la evaluacion colaborativa (US-008, US-009) puede esperar.

**Recomendacion:** MoSCoW es ideal para LTI ATS si el equipo ya tiene consenso sobre que es "critico" y si hay presion de tiempo para definir el backlog rapidamente. Es el metodo mas pragmatico de los 4.

---

### 2.2 RICE Score

**Fortalezas:**

1. **Objetividad y justificacion cuantitativa:** RICE elimina debates subjetivos con numeros concretos. El debate "¿US-007 es mas importante que US-008?" se resuelve matematicamente: US-007 (RICE: 12.3) > US-008 (RICE: 6.0). Esto es especialmente valioso en equipos grandes o distribuidos donde el consenso es dificil.

2. **Visibilidad del ROI:** La formula (Reach × Impact × Confidence) / Effort hace explicito el trade-off valor/esfuerzo. US-001 tiene RICE de 32.0 porque combina alto alcance (100), alto impacto (2), alta confianza (80%) con bajo esfuerzo (5 SP). Esta transparencia facilita decisiones de inversion.

3. **Identificacion de Quick Wins:** RICE destaca automaticamente features con RICE alto + Effort bajo. En el ejercicio, US-001 (RICE: 32.0, 5 SP) y US-011 (RICE: 10.0, 3 SP) son Quick Wins obvios. Esto permite ejecutar victorias tempranas para generar momentum.

4. **Fuerza a cuantificar asunciones:** Al requerir numeros especificos (Reach: 100, Impact: 2), RICE obliga al equipo a hacer explicitas sus hipotesis. Esto facilita validacion posterior: ¿Era correcto asumir Reach de 100 para US-001? ¿El Impact real fue 2 o 1.5?

**Debilidades:**

1. **Ignora dependencias tecnicas completamente:** RICE priorizo US-004 (Kanban, RICE: 30.0) en posicion #2, por encima de US-002 (Publicar, RICE: 12.3) en posicion #6. Pero tecnicamente, el Kanban es inutil sin candidatos, y no hay candidatos sin publicacion. RICE romperia el flujo logico si se siguiera ciegamente.

2. **Calidad de la priorizacion depende de estimaciones precisas:** Si Reach, Impact o Confidence estan mal estimados, todo el ranking es incorrecto. En el ejercicio, asumir Reach de 200 para US-007 (Comunicaciones) porque "afecta a todos los candidatos" es debatible - ¿realmente genera valor a candidatos que nunca responden emails?

3. **No captura naturaleza de la satisfaccion:** RICE trata todas las features igual. US-002 (Publicar - hygiene factor Basic) y US-005 (Scoring IA - diferenciador Excitement) tienen scores similares (12.3 vs 18.5), pero su naturaleza es diferente. Publicar es esperado, Scoring genera "wow". RICE no lo distingue.

4. **Complejidad de setup:** Definir los rangos de Reach (0-1000), Impact (0.25-3), Confidence (50-100%) requiere calibracion y consenso previo. En el ejercicio, tomo ~30 min solo definir estos parametros. MoSCoW seria 3x mas rapido.

5. **Penaliza features complejas pero criticas:** US-003 (Parsing CVs) tiene Effort de 21 SP, lo que hundio su RICE a 22.9 a pesar de su alto impacto. En realidad, es indispensable para el diferenciador de IA. RICE podria llevar a cortar features complejas que son estrategicamente criticas.

**Aplicabilidad a LTI ATS:**

Funciono razonablemente bien pero con caveats. RICE identifico correctamente el top 3 (US-001, US-004, US-003) que son efectivamente las features mas criticas. Sin embargo, el ordenamiento interno de posiciones 4-11 es cuestionable. Por ejemplo, US-007 (Comunicaciones, RICE: 12.3) quedo #7, por encima de US-008 (Entrevistas, RICE: 6.0) en #9, pero en realidad las entrevistas son mas criticas para el flujo end-to-end que los emails automaticos.

El metodo seria mas efectivo si se complementara con un "ajuste de dependencias" post-calculo: despues de ordenar por RICE, reordenar manualmente respetando dependencias tecnicas. Esto hibrido (RICE + ajuste manual) seria mas robusto.

**Recomendacion:** RICE es ideal si necesitas justificar decisiones con datos a stakeholders cuantitativos (CFOs, VCs, board) o si hay mucho debate interno sobre prioridades. Pero no lo uses ciegamente - siempre valida que el orden resultante respeta dependencias tecnicas.

---

### 2.3 Kano + Value/Effort

**Fortalezas:**

1. **Identificacion explicita de diferenciadores (Excitement):** El mayor valor de Kano es la categorizacion en Basic/Performance/Excitement/Indifferent. En el ejercicio, Kano identifico correctamente que US-005 (Scoring IA) es "Excitement" - el unico feature que genera "wow". Esto es critico para posicionamiento de mercado. Los otros metodos (MoSCoW, RICE, Story Mapping) no distinguen entre hygiene factors y diferenciadores.

2. **Elimina features de bajo valor (Indifferent):** Kano clasifico US-010 (Dashboard) y US-011 (Aprobaciones) como "Indifferent" - features que no generan satisfaccion en core users. Esto evita desperdiciar esfuerzo en features que parecen importantes pero no lo son. MoSCoW los clasifico como "Could Have" (menos enfatico).

3. **Visualizacion intuitiva con matriz Value/Effort:** La matriz 2×2 (Quick Wins / Big Bets / Money Pits / Time Sinks) es extremadamente visual y facil de comunicar. Stakeholders no tecnicos entienden inmediatamente que "Quick Wins = hacer YA" y "Money Pits = evitar". Es casi tan visual como Story Mapping pero mas cuantitativo.

4. **Balance explicito de tipos de features:** Kano fuerza a balancear el MVP: 27% Basic (hygiene), 45% Performance (value drivers), 9% Excitement (diferenciadores), 18% Indifferent (eliminar). Este balance consciente evita MVPs que son "solo hygiene" o "solo wow sin fundamentos".

5. **Trade-offs documentados:** El metodo incluyo analisis explicito de 3 trade-offs (US-005 vs US-008+US-009, multicanal 2 vs 8 job boards, dashboard basico vs eliminar). Esto transparenta decisiones dificiles y facilita retrospectivas.

**Debilidades:**

1. **Complejidad y tiempo de setup:** Kano requiere 2 pasos (clasificacion Kano + estimacion Value/Effort) vs 1 paso en MoSCoW. En el ejercicio, tomo ~2 horas clasificar las 11 US en categorias Kano, debatir si US-008 es Performance o Basic, y luego ubicarlas en la matriz. Es 3-4x mas lento que MoSCoW.

2. **Subjetividad en clasificacion Kano:** ¿US-004 (Kanban) es Basic o Performance? Argumentos para ambos: es "esperado" (Basic) pero "cuanto mejor el Kanban, mayor satisfaccion" (Performance). En el ejercicio se clasifico como Basic, pero podria ser Performance. Esto genera debates largos.

3. **No garantiza flujo end-to-end:** Kano priorizo US-007 (Comunicaciones) como Quick Win (P0) porque tiene Value 7/10 con Effort 5 SP. Pero el walking skeleton no necesita emails automaticos - puedes contratar sin ellos. Kano puede priorizar Quick Wins que no son criticos para MVP minimo.

4. **Value score sigue siendo subjetivo:** Asignar Value 8/10 a US-006 (Perfil) vs Value 7/10 a US-007 (Comunicaciones) es debatible. Aunque es mas granular que MoSCoW, sigue siendo juicio del PM. RICE es mas objetivo con Reach × Impact.

5. **Matriz puede generar confusion en features fronterizas:** US-002 (Publicar) tiene Value 9, Effort 8. ¿Es Quick Win o Big Bet? Esta en la frontera del cuadrante. Kano lo clasifico como Big Bet, pero alguien podria argumentar que con Value 9 deberia ser Quick Win. Los limites de cuadrantes son arbitrarios.

**Aplicabilidad a LTI ATS:**

Funciono muy bien para identificar la naturaleza de cada feature. La clasificacion Kano fue precisa: US-002, US-004, US-006 son Basic (su ausencia mataria el producto), US-005 es Excitement (genera wow), US-010 y US-011 son Indifferent (eliminar). Esta claridad ayudo a tomar decisiones dificiles, como postponer US-011 (Aprobaciones) completamente porque no genera satisfaccion real.

Sin embargo, la priorizacion final (P0: US-004, US-001, US-006, US-007 / P1: US-002, US-003, US-005, US-008, US-009) incluyo US-007 en P0 (Quick Wins del MVP) cuando en realidad no es necesaria para el walking skeleton. Story Mapping corrigio esto moviendola a Release 2.

**Recomendacion:** Kano es ideal si necesitas identificar diferenciadores para posicionamiento de producto o si estas en fase de discovery entendiendo que tipo de features construir. Es especialmente util para productos consumer donde la "satisfaccion del usuario" es critica. Para B2B como LTI ATS, sigue siendo valioso pero Story Mapping o MoSCoW son mas pragmaticos.

---

### 2.4 Story Mapping

**Fortalezas:**

1. **Garantiza MVP funcional end-to-end (walking skeleton):** La mayor fortaleza de Story Mapping es estructurar el backlog por "actividades del usuario" (backbone horizontal). Esto asegura que cada release tiene "1 US por actividad critica", garantizando flujo completo. En el ejercicio, el MVP incluyo: Publicar Oferta (US-001) → Distribuir (US-002) → Recibir Candidatos (US-003) → Screening (US-004, US-005, US-006). Ningun otro metodo garantiza esto tan explicitamente.

2. **Visualizacion superior para comunicacion:** El Story Map 2D (actividades × releases) es la herramienta mas visual de todas. Un stakeholder no tecnico (CEO, inversor, cliente) entiende inmediatamente "asi es como el reclutador trabajara con el producto". Es storytelling visual. MoSCoW es una lista plana, RICE es una tabla de numeros, Kano es una matriz abstracta, pero Story Mapping muestra el journey real.

3. **Priorizacion consciente del flujo del usuario:** Story Mapping priorizo US-002 (Publicar) en Release 1 a pesar de su complejidad (13 SP) porque "no hay candidatos sin publicacion". En contraste, RICE lo puso en posicion #6 porque penaliza Effort alto. Story Mapping es mas consciente de dependencias logicas del usuario.

4. **Releases incrementales coherentes:** Cada release es una "fila" del Story Map que añade profundidad al producto sin romper el flujo. Release 1 (screening automatizado) → Release 2 (evaluacion colaborativa) → Release 3 (features avanzadas). Cada release es vendible por si sola. Los otros metodos no estructuran releases tan claramente.

5. **Evolucion del producto clara:** El Story Map es una herramienta viva que crece con el producto. En el ejercicio, se planificaron expansiones horizontales (nuevas actividades: Onboarding, Talent Pool) y verticales (profundidad en actividades existentes: bias detection en Screening, video entrevistas en Entrevistar). Esto da claridad del roadmap a 6-12 meses.

**Debilidades:**

1. **Complejidad de setup inicial:** Story Mapping requiere definir el "backbone" (actividades principales del usuario) antes de priorizar US. En el ejercicio, tomo ~45 min definir las 9 actividades (Publicar Oferta, Distribuir, Recibir Candidatos, Screening, Entrevistar, Evaluar, Comunicar, Contratar, Medir) y debatir si "Comunicar" es actividad separada o transversal. MoSCoW seria 5x mas rapido.

2. **Requiere entendimiento profundo del user journey:** Si el PM no conoce bien como trabajan los reclutadores, el Story Map sera incorrecto. En el ejercicio, fue critico entender que Screening es la actividad de mayor volumen (100% de candidatos) mientras que Entrevistar es solo 5% (candidatos pre-seleccionados). Sin este contexto, la priorizacion seria erronea.

3. **Subjetividad en definicion de "walking skeleton":** ¿El MVP minimo incluye Comunicaciones (US-007) o no? Story Mapping lo excluyo diciendo "puedes contratar sin emails automaticos", pero Kano lo incluyo como Quick Win. Ambos argumentos son validos. La definicion de "minimo viable" sigue siendo subjetiva.

4. **No cuantifica ROI explicitamente:** Story Mapping no tiene numeros (scores, valores) que justifiquen decisiones. Si un CFO pregunta "¿Por que US-005 esta en MVP a pesar de costar 13 SP?", la respuesta es cualitativa ("es el diferenciador killer"). RICE daria respuesta cuantitativa (RICE: 18.5). Story Mapping es menos "data-driven".

5. **Puede ser overengineering para backlogs pequeños:** Para 11 US, crear un Story Map completo puede ser excesivo. MoSCoW seria suficiente. Story Mapping brilla con backlogs grandes (30-50 US) donde la complejidad del journey justifica la herramienta visual.

**Aplicabilidad a LTI ATS:**

Funciono excepcionalmente bien. LTI ATS es un producto con journey largo y complejo (9 actividades secuenciales y paralelas), ideal para Story Mapping. El metodo capturo correctamente que:
- El MVP debe cubrir las primeras 4 actividades (Publicar → Distribuir → Recibir → Screening) porque son secuenciales y bloqueantes
- Las actividades finales (Entrevistar, Evaluar) pueden ser manuales en MVP porque son bajo volumen
- Comunicar es transversal y puede automatizarse en Release 2

El walking skeleton resultante (US-001, US-002, US-003, US-004, US-005, US-006) es identico al "Must Have" de MoSCoW, lo que valida que ambos metodos convergen en el core del MVP.

**Recomendacion:** Story Mapping es ideal para LTI ATS porque es un producto complejo con journey multi-etapa. Es especialmente valioso si necesitas comunicar el roadmap a stakeholders no tecnicos o si planeas multiple releases con coherencia. Sin embargo, requiere mas tiempo de setup que MoSCoW, asi que es mejor para equipos maduros con experiencia en metodologias agiles.

---

## Parte 3: Analisis de Resultados (Diferencias en la Priorizacion)

### 3.1 User Stories Priorizadas en Sprint 1-3 (MVP)

Comparacion de que US cada metodo incluyo en el MVP (primeros 6 sprints / 12 semanas):

| Metodo | US Incluidas en MVP (Sprint 1-3) | Observaciones |
|--------|-----------------------------------|---------------|
| **MoSCoW** | US-001, US-002, US-003, US-004, US-005, US-006 (Must Have) | Baseline - 6 US core |
| **RICE** | US-001, US-004, US-003, US-006, US-005, US-002 (Top 6 por score) | Identicas a MoSCoW pero orden interno diferente |
| **Kano** | US-001, US-004, US-006, US-007 (Quick Wins) + US-002, US-003, US-005 (Big Bets Priority) | Añade US-007, total 7 US en MVP |
| **Story Mapping** | US-001, US-002, US-003, US-004, US-005, US-006 (Walking Skeleton Release 1) | Identicas a MoSCoW |

**Analisis de convergencia - US que aparecen en TODOS los metodos:**

**Consenso universal (6 US):**
- **US-001 (Crear Oferta con IA):** Todos los metodos coinciden que es #1 o top 3. Es el punto de entrada del sistema, bloqueante total.
- **US-002 (Publicar en Multiples Canales):** Todos la incluyen en MVP. Sin publicacion no hay candidatos. Es critica para volumen.
- **US-003 (Parsear CVs con IA):** Todos coinciden que es core del diferenciador de IA. Aunque compleja (13-21 SP), es indispensable.
- **US-004 (Pipeline Kanban):** Todos la incluyen. Es la interfaz principal del producto, sin ella el sistema no es usable.
- **US-005 (Scoring IA):** Todos la incluyen en MVP. Es el diferenciador killer. MoSCoW, Kano y Story Mapping la marcan como critica. RICE le da score alto (18.5).
- **US-006 (Perfil Completo):** Todos la incluyen. Necesaria para revisar candidatos y tomar decisiones informadas.

**Conclusion:** Estos 6 features tienen consenso del 100% y forman el "core irrefutable" del MVP. Cualquier metodo que uses, estas 6 US deben estar en los primeros 3 sprints.

---

### US Controversiales (aparecen solo en algunos metodos)

**US-007 (Comunicaciones Automaticas):**
- **Incluida en MVP:** Kano (como Quick Win P0, Sprint 1-3)
- **Excluida del MVP:** MoSCoW (Should Have, Sprint 5), RICE (#7, Sprint 5), Story Mapping (Release 2, Sprint 5)
- **Por que la controversia:** Kano la prioriza porque tiene Value/Effort favorable (7/10 valor, 5 SP esfuerzo) = Quick Win. Los otros metodos argumentan que no es bloqueante para el walking skeleton - puedes contratar sin emails automaticos usando Gmail manualmente. **Decision correcta:** Excluir del MVP minimo (Sprint 1-3), incluir en Sprint 5. Kano se equivoco priorizandola demasiado alto.

**US-008 (Programar Entrevistas):**
- **Incluida en MVP:** Ningun metodo (todos la posponen a Sprint 4-5)
- **Justificacion unanime:** Solo 5% de candidatos llegan a entrevista. Es importante para eficiencia pero hay workaround facil (Google Calendar manual). Consenso del 100% en postponerla.

**US-009 (Evaluacion Colaborativa):**
- **Incluida en MVP:** Ningun metodo (todos la posponen a Sprint 5-6)
- **Justificacion unanime:** Solo 3% de candidatos llegan a evaluacion final. Feature compleja (13 SP) que puede hacerse con Google Docs temporalmente. Consenso del 100% en postponerla.

**US-010 (Dashboard de Metricas):**
- **Incluida en MVP:** Ningun metodo (todos la clasifican como baja prioridad)
- **Justificacion unanime:** MoSCoW (Could Have), RICE (score mas bajo: 1.0), Kano (Indifferent), Story Mapping (Release 2 condicional). Consenso del 100% en que no es critica para operaciones diarias.

**US-011 (Aprobar Oferta):**
- **Incluida en MVP:** Ningun metodo (todos la clasifican como baja prioridad o eliminar)
- **Justificacion unanime:** MoSCoW (Could Have), RICE (#8), Kano (Indifferent → Won't Have), Story Mapping (Release 2 o v2.0). Consenso del 100% en que añade friccion sin valor significativo para el target inicial (startups).

---

### 3.2 User Stories Diferidas/Eliminadas

**Consenso de eliminacion del MVP (unanimidad en 3 US):**
- **US-008 (Programar Entrevistas):** Todos la mueven a Sprint 4-5. No es bloqueante para walking skeleton.
- **US-009 (Evaluacion Colaborativa):** Todos la mueven a Sprint 5-6. Complejidad alta, bajo volumen de uso.
- **US-010 (Dashboard):** Todos la clasifican como baja prioridad (Sprint 6 o post-MVP).

**Consenso de simplificacion:**
- **US-002 (Publicar Multicanal):** Kano propuso reducir de 8 job boards a 4 (LinkedIn, Indeed, Glassdoor, Monster) para bajar esfuerzo de 13 SP a 6-7 SP. Los otros metodos no entraron en este nivel de detalle, pero el trade-off es valido.
- **US-010 (Dashboard):** Kano propuso version "mini" de 3 SP en lugar de 5 SP, con metricas ultra-basicas. Story Mapping tambien sugirio version condicional. Consenso en que si se incluye, debe ser simplificada.

**Controversia - US-011 (Aprobar Oferta):**
- **MoSCoW:** Could Have (Sprint 5-6) - podria incluirse si hay capacidad
- **RICE:** Score medio (10.0), posicion #8 - incluir en Sprint 5
- **Kano:** Indifferent → Won't Have v1 - eliminar completamente del MVP
- **Story Mapping:** Release 2 o v2.0 - postponer hasta que clientes enterprise lo soliciten

**Decision correcta:** Kano tiene razon - US-011 debe eliminarse del MVP v1 porque es "Indifferent" para el target inicial (startups/scale-ups que prefieren velocidad sobre control). MoSCoW y RICE fueron demasiado conservadores incluyendola en "Could Have" / posicion #8. Esta US debe implementarse solo cuando tengamos clientes enterprise que explicitamente la soliciten.

---

### 3.3 Orden de Implementacion (diferencias internas)

Aunque los 4 metodos coinciden en las 6 US del MVP, el orden de implementacion varia:

| Orden | MoSCoW | RICE | Kano | Story Mapping |
|-------|--------|------|------|---------------|
| 1 | US-001 | US-001 | US-004 | US-001 |
| 2 | US-002 | US-004 | US-001 | US-002 |
| 3 | US-003 | US-003 | US-006 | US-003 |
| 4 | US-004 | US-006 | US-007 | US-004 |
| 5 | US-005 | US-005 | US-002 | US-005 |
| 6 | US-006 | US-002 | US-003 | US-006 |

**Observaciones:**
- **US-001 esta en top 2 en todos los metodos** excepto Kano (que la pone #2). Consenso casi total.
- **Kano prioriza US-004 (Kanban) como #1** por ser Quick Win con maximo valor (10/10). Pero esto ignora dependencias: el Kanban es inutil sin candidatos (que vienen de US-002 y US-003).
- **RICE prioriza US-004 en #2, por encima de US-002 (#6)** por el mismo motivo: mejor ratio Value/Effort. Pero rompe el flujo logico.
- **MoSCoW y Story Mapping son los unicos que respetan estrictamente dependencias tecnicas:** US-001 → US-002 → US-003 → US-004 → US-005 → US-006 es el orden logico del flujo.

**Conclusion:** El orden "correcto" depende de si priorizas ROI inmediato (RICE, Kano) o coherencia del flujo (MoSCoW, Story Mapping). Para LTI ATS, respetar dependencias es mas importante que maximizar ROI individual de cada feature, porque construir US-004 antes que US-002 es tecnicamente imposible.

---

## Parte 4: Recomendacion Final para LTI ATS

### 4.1 Metodo Ganador

**Metodo recomendado:** **User Story Mapping**

**Justificacion (3 razones principales):**

**1. Garantiza MVP funcional end-to-end sin gaps**

Story Mapping es el unico metodo que estructura explicitamente el backlog por "actividades del usuario" (backbone horizontal), asegurando que cada release cubre el journey completo. En el ejercicio, el MVP incluyo: Publicar Oferta → Distribuir → Recibir Candidatos → Screening, cubriendo las 4 actividades criticas secuenciales. Los otros metodos priorizan features individuales sin garantizar coherencia del flujo. RICE, por ejemplo, priorizaria US-004 (Kanban, score 30.0) antes que US-002 (Publicar, score 12.3), rompiendo el flujo logico. Story Mapping previene estos errores estructurando el backlog por journey.

**2. Comunicacion superior a stakeholders no tecnicos**

El Story Map 2D (actividades × releases) es storytelling visual. Un CEO, inversor o cliente piloto entiende inmediatamente "asi es como el reclutador trabajara con el producto" viendo el mapa. En contraste, MoSCoW es una lista plana (poco visual), RICE es una tabla de numeros (poco intuitiva para no tecnicos), y Kano es una matriz abstracta (requiere explicacion). Durante el ejercicio, el Story Map fue la herramienta mas efectiva para visualizar como el producto evoluciona desde MVP (screening automatizado) → v1.1 (evaluacion colaborativa) → v2.0 (features avanzadas).

**3. Equilibrio optimo entre pragmatismo (MoSCoW) y estructura (RICE/Kano)**

Story Mapping combina lo mejor de los otros metodos:
- **Como MoSCoW:** Es pragmatico y considera dependencias tecnicas explicitamente
- **Como RICE:** Fuerza a cuantificar esfuerzo (Story Points por US) para priorizar
- **Como Kano:** Identifica diferenciadores (US-005 esta en Release 1 a pesar de su complejidad porque es killer feature)

Pero evita las debilidades:
- **A diferencia de MoSCoW:** Visualiza el producto completo, no solo una lista de prioridades
- **A diferencia de RICE:** No ignora dependencias tecnicas que rompen el flujo
- **A diferencia de Kano:** No prioriza Quick Wins que no son criticos para walking skeleton (ej: US-007)

**Trade-off aceptado:** Story Mapping requiere mas tiempo de setup inicial (~1-2 horas para definir el backbone) vs MoSCoW (~30 min), pero la claridad del roadmap justifica la inversion. Para LTI ATS con 11 US y 3 meses de desarrollo, el esfuerzo adicional vale la pena.

---

### 4.2 Metodo Complementario

**Usar adicionalmente:** **Modelo Kano**

**Para que:** **Discovery de diferenciadores y validacion de tipo de features**

**Justificacion:**

Aunque Story Mapping es el metodo principal para estructurar el backlog, Kano añade valor en una fase previa (discovery) o como validacion paralela:

**Uso en Discovery (antes de Story Mapping):**
Antes de crear el Story Map, usa Kano para clasificar las 11 US en Basic/Performance/Excitement/Indifferent. Esto aclara:
- ¿Cuales features son hygiene factors esperados? (US-002, US-004, US-006)
- ¿Cuales son diferenciadores que generan "wow"? (US-005)
- ¿Cuales podemos eliminar sin impacto? (US-010, US-011)

Esta clasificacion informara el Story Mapping: las features "Excitement" deben estar en Release 1 aunque sean complejas, las "Indifferent" se eliminan o postponen a v2.0.

**Uso como validacion (paralelo a Story Mapping):**
Despues de crear el Story Map, valida que cada release tiene balance adecuado de tipos de features:
- Release 1 debe tener mayoria de Basic + Performance + al menos 1 Excitement
- Release 2 puede tener solo Performance (mejoras incrementales)
- Evitar releases que sean 100% Basic (no generan diferenciacion) o 100% Excitement (sin fundamentos)

En el ejercicio, la clasificacion Kano valido que el MVP de Story Mapping es balanceado: 3 Basic (US-002, US-004, US-006) + 2 Performance (US-001, US-003) + 1 Excitement (US-005) = 50% hygiene, 50% diferenciacion.

**Inversion de tiempo:** 1-2 horas adicionales para clasificacion Kano. Vale la pena para productos B2C o B2B con enfoque en experiencia del usuario.

---

### 4.3 Recomendacion Hibrida (Opcional)

**Propuesta de workflow hibrido para LTI ATS:**

**Paso 1: Usar Kano para clasificar tipos de features (1-2 horas)**
- Clasificar las 11 US en Basic/Performance/Excitement/Indifferent
- Identificar diferenciadores (Excitement) que deben estar en MVP
- Eliminar features Indifferent del backlog inicial (US-010, US-11 → v2.0)
- Output: 9 US clasificadas por tipo

**Paso 2: Crear Story Map del journey (2-3 horas)**
- Definir backbone (actividades principales): Publicar, Distribuir, Recibir, Screening, Entrevistar, Evaluar, Comunicar, Medir
- Ubicar las 9 US (post-Kano) en actividades correspondientes
- Definir walking skeleton (Release 1): 1 US por actividad critica que cubra flujo end-to-end
- Output: Story Map con 3 releases planificadas

**Paso 3: Validar con RICE para features controversiales (1 hora)**
- Calcular RICE score solo para features donde hay debate interno (ej: US-007 - ¿incluir en MVP o no?)
- Usar RICE como "tiebreaker" cuantitativo cuando Story Mapping no da respuesta clara
- Output: Decision basada en datos para 2-3 features controversiales

**Paso 4: Comunicar con Story Map, defender con RICE si necesario**
- Presentar el Story Map a stakeholders para comunicar el roadmap visualmente
- Si alguien cuestiona una decision (ej: "¿Por que US-005 esta en MVP si cuesta 13 SP?"), usar RICE score (18.5) para justificar con datos
- Output: Consenso del equipo y stakeholders en el backlog priorizado

**Tiempo total:** 4-6 horas (vs 30 min de MoSCoW solo, pero con resultado mucho mas robusto)

**Ventaja del hibrido:**
- **Kano** identifica diferenciadores y elimina ruido
- **Story Mapping** estructura el backlog por journey garantizando coherencia
- **RICE** resuelve debates con datos cuando hay controversia
- Combina lo mejor de los 3 metodos evitando debilidades individuales

**Trade-off:** Requiere mas tiempo (4-6 horas vs 30 min de MoSCoW puro), pero para un proyecto de 3 meses con 7 personas (inversion de $200-300K), gastar 6 horas en priorizacion correcta es absolutamente justificado.

---

## Parte 5: Lecciones Aprendidas del Ejercicio

### 5.1 ¿Que aprendimos al experimentar con 4 metodos?

**Insight 1: Los 4 metodos convergen en el core, difieren en la periferia**

**Descripcion:** Todos los metodos identificaron las mismas 6 US como "core del MVP" (US-001 a US-006). La convergencia fue del 100%. Las diferencias aparecen en features "fronterizas" como US-007 (Comunicaciones) - Kano la incluyo en MVP, los otros no. Esto sugiere que para features obviamente criticas o obviamente prescindibles, el metodo importa poco. El metodo importa mucho para features "grises" donde el trade-off no es obvio.

**Implicacion practica:** Si tienes un backlog de 50 US, usa un metodo ligero (MoSCoW) para clasificar rapidamente las 40 US obvias (20 Must Have, 20 Won't Have), y usa un metodo robusto (Story Mapping + Kano) solo para las 10 US controversiales. Esto optimiza tiempo sin sacrificar calidad de decision.

---

**Insight 2: La objetividad tiene costo - RICE toma 3x mas tiempo que MoSCoW**

**Descripcion:** RICE es el metodo mas "objetivo" porque usa numeros (Reach, Impact, Confidence, Effort), pero requiere calibrar parametros, debatir estimaciones, y calcular scores. En el ejercicio, RICE tomo ~2 horas vs ~40 min de MoSCoW. ¿La objetividad adicional vale 3x mas tiempo? Depende del contexto:
- **Si:** En equipos grandes (10+ personas) donde el consenso es dificil, o si necesitas defender decisiones ante stakeholders cuantitativos (CFO, board)
- **No:** En equipos pequeños (5-7 personas) con consenso fuerte, o si hay presion de tiempo para lanzar rapido

**Implicacion practica:** No uses RICE por default. Usalo solo cuando la subjetividad sea un problema real (debates interminables, politica interna) o cuando necesites justificar ROI con numeros. Para la mayoria de MVPs, MoSCoW o Story Mapping son suficientes.

---

**Insight 3: Story Mapping es la mejor herramienta de comunicacion, pero requiere facilitacion experta**

**Descripcion:** El Story Map 2D (actividades × releases) fue la herramienta mas visual y facil de comunicar a stakeholders no tecnicos. Sin embargo, crear un Story Map correcto requiere experiencia:
- Definir el backbone (actividades principales) no es trivial - requiere entender profundamente el journey del usuario
- Ubicar US en actividades puede ser ambiguo (ej: US-007 Comunicaciones - ¿es actividad separada o transversal?)
- Definir el walking skeleton requiere criterio experimentado sobre que es "minimo viable"

En el ejercicio, el PM tuvo que facilitar activamente, hacer preguntas, y guiar decisiones. Un equipo junior sin facilitador experto podria crear un Story Map incorrecto.

**Implicacion practica:** Story Mapping es ideal para equipos maduros con PM experimentado. Para equipos junior, empieza con MoSCoW (mas simple) y evoluciona a Story Mapping cuando el equipo tenga mas contexto del producto y usuarios.

---

**Insight 4: Kano es excelente para productos consumer, menos critico para B2B**

**Descripcion:** El Modelo Kano distingue entre Basic/Performance/Excitement basado en "satisfaccion del usuario". Esto es muy valioso para productos consumer (B2C) donde la experiencia emocional es critica. Para B2B como LTI ATS, la clasificacion sigue siendo util pero menos determinante:
- En B2C, un feature "Excitement" puede ser el diferenciador total (ej: Instagram Stories)
- En B2B, los compradores son mas racionales y priorizan ROI, eficiencia, integraciones

En el ejercicio, Kano identifico correctamente US-005 (Scoring IA) como "Excitement", pero en realidad los clientes B2B compran LTI ATS mas por "reducir time-to-hire 50%" (ROI cuantificable) que por "wow factor". El Excitement importa mas en demos/ventas que en adopcion diaria.

**Implicacion practica:** Usa Kano si tu producto es B2C, freemium, o viralidad/experiencia es critica. Para B2B enterprise, Kano sigue siendo util en discovery pero complementalo con RICE (que enfatiza ROI medible) o Story Mapping (que enfatiza flujo de trabajo).

---

**Insight 5: Ningun metodo captura "riesgo tecnico" explicitamente**

**Descripcion:** Los 4 metodos ignoran o minimizan el riesgo tecnico:
- **MoSCoW** menciona riesgo en el analisis pero no lo usa en la clasificacion Must/Should/Could
- **RICE** no tiene componente de riesgo en la formula (algunos equipos añaden "Risk" haciendo RICE → RICES, pero no es estandar)
- **Kano** ignora riesgo completamente, solo considera satisfaccion del usuario
- **Story Mapping** no cuantifica riesgo, aunque si considera "complejidad" al estimar Story Points

En el ejercicio, US-003 (Parsing CVs) y US-005 (Scoring IA) tienen riesgo tecnico alto (precision de modelos de ML es incierta), pero ninguno de los metodos ajusto la priorizacion por esto. En la practica, el equipo deberia:
- Priorizar features de alto riesgo mas temprano (para validar factibilidad)
- O despriorizarlas si el riesgo es demasiado alto (y buscar alternativas)

**Implicacion practica:** Complementa cualquier metodo de priorizacion con un analisis explicito de riesgos tecnicos. Usa una matriz simple: Riesgo (Bajo/Medio/Alto) × Impacto si falla (Bajo/Medio/Alto). Features con Riesgo Alto + Impacto Alto deben tener estrategia de mitigacion especifica (spikes tecnicos, prototipos, Plan B).

---

### 5.2 ¿Cuando usar cada metodo?

Guia rapida para elegir metodo segun contexto:

| Metodo | Mejor Para | Evitar Si |
|--------|-----------|-----------|
| **MoSCoW** | - MVPs rapidos (lanzar en <3 meses)<br>- Equipos pequeños (3-7 personas) con consenso fuerte<br>- Backlogs pequeños (<20 US)<br>- PRD claro con requisitos bien definidos<br>- Necesitas velocidad sobre precision | - Necesitas justificar decisiones con datos cuantitativos a CFO/board<br>- Hay debates internos fuertes sobre prioridades<br>- Producto complejo con journey multi-etapa largo<br>- Equipo distribuido sin consenso previo |
| **RICE Score** | - Backlogs maduros (v1.1, v2.0) con historico de metricas<br>- Decisiones data-driven para stakeholders cuantitativos<br>- Necesitas justificar ROI de cada feature<br>- Equipos grandes (10+ personas) donde consenso es dificil<br>- Cultura de empresa analitica (ej: ex-Google, ex-Amazon) | - Producto nuevo sin datos historicos de Reach/Impact<br>- Equipo junior sin experiencia estimando parametros<br>- Presion de tiempo (RICE toma 2-3x mas que MoSCoW)<br>- Producto con dependencias tecnicas fuertes (RICE las ignora) |
| **Kano + Value/Effort** | - Discovery de producto (fase pre-MVP)<br>- Identificar diferenciadores para posicionamiento<br>- Productos consumer (B2C) donde satisfaccion es critica<br>- Necesitas eliminar features de bajo valor<br>- Presentaciones a inversores (matriz Value/Effort es visual) | - Poco tiempo (<2 horas para priorizacion)<br>- Equipo junior sin entrenamiento en Kano<br>- Producto B2B enterprise donde ROI cuantificable > experiencia<br>- Ya sabes claramente que es diferenciador (no necesitas Kano) |
| **Story Mapping** | - Productos complejos con journeys multi-etapa (ej: ATS, CRM, ERP)<br>- Necesitas garantizar MVP funcional end-to-end<br>- Comunicacion a stakeholders no tecnicos (CEO, clientes, inversores)<br>- Planificacion de multiples releases coherentes<br>- Equipos maduros con PM experimentado | - Productos simples sin journey claro (ej: API tool, biblioteca)<br>- Features independientes sin flujo (ej: utilidades, plugins)<br>- Equipo junior sin facilitador experto<br>- Backlog muy pequeño (<10 US) donde Story Map es overengineering |

---

### 5.3 Conclusion Final

**¿Que metodo fue mas efectivo para LTI ATS y por que?**

**User Story Mapping** resulto ser el metodo mas efectivo para LTI ATS, seguido de cerca por MoSCoW. La razon fundamental es que LTI ATS es un producto con **journey largo y complejo** (9 actividades secuenciales y paralelas desde publicar oferta hasta medir resultados), donde el valor esta en **completar el proceso de principio a fin**, no en features individuales aisladas.

Story Mapping destaco por 3 motivos criticos:

1. **Garantizo MVP funcional end-to-end:** El walking skeleton resultante (US-001, US-002, US-003, US-004, US-005, US-006) cubre las 4 actividades criticas (Publicar → Distribuir → Recibir → Screening), asegurando que el reclutador puede trabajar completamente con el sistema. RICE, en cambio, habria priorizado US-004 (Kanban) antes que US-002 (Publicar) por mejor ratio Value/Effort, rompiendo el flujo logico.

2. **Facilito comunicacion visual del roadmap:** El Story Map 2D fue la herramienta mas efectiva para mostrar a stakeholders (CEO, inversores potenciales, clientes beta) como evoluciona el producto. Ver "asi es como el reclutador trabajara" fue mas poderoso que mostrar una lista de prioridades (MoSCoW) o una tabla de scores (RICE).

3. **Equilibrio entre pragmatismo y estructura:** Story Mapping combino la claridad de dependencias de MoSCoW, la conciencia de esfuerzo de RICE, y la identificacion de diferenciadores de Kano, sin las debilidades de cada uno.

**MoSCoW quedo muy cerca** (40/50 vs 42/50) porque es extremadamente pragmatico y rapido. La clasificacion Must/Should/Could convergio identicamente con Story Mapping en las 6 US core. Para equipos con presion de tiempo o experiencia limitada, MoSCoW es la opcion mas segura.

---

**¿Que sorprendio del ejercicio?**

**Sorpresa #1:** Los 4 metodos convergieron en las mismas 6 US para el MVP (US-001 a US-006), con consenso del 100%. Esto sugiere que para features obviamente criticas, el metodo importa menos de lo que pensamos. La eleccion de metodo es mas relevante para features "grises" o controversiales.

**Sorpresa #2:** RICE, siendo el metodo mas "objetivo" y "data-driven", fue el menos efectivo para LTI ATS porque ignoro dependencias tecnicas. Esto desafia la asuncion de que "mas datos = mejores decisiones". En productos con flujo complejo, la coherencia del journey (Story Mapping) supera la precision numerica (RICE).

**Sorpresa #3:** Kano priorizo incorrectamente US-007 (Comunicaciones) como Quick Win P0, incluyendola en el MVP cuando en realidad no es necesaria para el walking skeleton. Esto revela que "Quick Wins" (alto valor, bajo esfuerzo) no siempre deben priorizarse - importa si son bloqueantes para el flujo.

**Sorpresa #4:** El tiempo invertido en priorizacion vario dramaticamente: MoSCoW (40 min) vs RICE (2h) vs Kano (2h) vs Story Mapping (2-3h). Para un proyecto de 3 meses ($200-300K inversion), gastar 2-3h extra en Story Mapping es absolutamente justificado, pero muchos equipos subestiman este tiempo y usan MoSCoW por default sin considerar alternativas.

---

**¿Que recomendarias a otros PMs?**

**Recomendacion #1: Elige metodo segun tipo de producto, no por preferencia personal**

- **Producto con journey complejo (ATS, CRM, ERP):** Usa Story Mapping
- **MVP rapido con equipo pequeño:** Usa MoSCoW
- **Necesitas justificar ROI con datos:** Usa RICE
- **Discovery de diferenciadores:** Usa Kano

No uses el metodo que "te gusta" o "usaste en tu empresa anterior". Usa el que mejor se adapta al contexto.

**Recomendacion #2: Combina metodos en workflow hibrido**

Usa Kano (1-2h) para clasificar tipos de features → Story Mapping (2-3h) para estructurar el journey → RICE (1h) como tiebreaker para features controversiales. Este hibrido de 4-6h es mas robusto que cualquier metodo individual.

**Recomendacion #3: Valida que el MVP garantiza flujo end-to-end**

Despues de priorizar con cualquier metodo, haz el "test del walking skeleton": ¿Un usuario puede completar el journey de principio a fin con el MVP? Si la respuesta es no, hay un gap. Story Mapping es el unico metodo que garantiza esto por diseño, pero puedes validarlo manualmente con otros metodos.

**Recomendacion #4: Documenta trade-offs, no solo decisiones**

Kano fue el unico metodo que documento explicitamente 3 trade-offs (US-005 vs US-008+US-009, multicanal 2 vs 8, dashboard basico vs eliminar). Esta documentacion es oro en retrospectivas: ¿Fue correcta la decision de priorizar US-005 sobre US-008? Los datos para responder estan documentados. Otros metodos solo documentan "que priorizamos", no "que sacrificamos".

**Recomendacion #5: Invierte tiempo proporcional al costo del proyecto**

Para un MVP de 3 meses con 7 personas ($200-300K inversion), gastar 6 horas en priorizacion robusta es 0.01% del presupuesto. No uses MoSCoW (40 min) solo porque "es rapido" si el proyecto justifica Story Mapping (3h). El costo de priorizar mal (construir features equivocadas) es 100-1000x mayor que el costo de priorizar bien.

---

## Anexo: Tabla Maestra de Comparacion

| Aspecto | MoSCoW | RICE Score | Kano + V/E | Story Mapping |
|---------|--------|------------|------------|---------------|
| **Tiempo de setup** | 30-60 min | 1.5-2h | 2-3h | 2-3h |
| **Complejidad** | Muy simple | Media | Alta | Media-alta |
| **Objetividad** | Baja (cualitativo) | Muy alta (cuantitativo) | Media (mixto) | Media (cualitativo con SP) |
| **Considera dependencias** | Si, explicito | No | Parcial | Si, explicito |
| **Visualizacion** | Lista plana | Tabla numerica | Matriz 2×2 | Mapa 2D journey |
| **Identifica diferenciadores** | No | Parcial (Impact alto) | Si (Excitement) | Si (en Release) |
| **Garantiza MVP funcional** | Si (Must Have) | No (puede romper flujo) | No (Quick Wins pueden no ser criticos) | Si (walking skeleton) |
| **Comunicacion stakeholders** | Buena (categorias claras) | Media (tecnico) | Buena (visual) | Excelente (storytelling) |
| **Mejor para LTI ATS** | 5/5 | 4/5 | 4/5 | 5/5 |
| **Recomendacion general** | **Default para MVPs rapidos** | Usa si necesitas datos | Usa en discovery | **Mejor para productos complejos** |

---

## Resumen Ejecutivo (1 pagina)

**Pregunta clave:** ¿Cual metodo de priorizacion fue mas efectivo para LTI ATS?

**Respuesta:** **User Story Mapping**, con **MoSCoW** como segundo muy cercano.

**Justificacion:**
1. LTI ATS es un producto con journey complejo (9 actividades) donde el valor esta en completar el proceso end-to-end, no en features aisladas. Story Mapping garantiza esto por diseño con el "walking skeleton".
2. El Story Map 2D fue la herramienta mas visual para comunicar el roadmap a stakeholders no tecnicos (CEO, inversores, clientes).
3. Story Mapping equilibro pragmatismo (como MoSCoW) con estructura robusta (como RICE/Kano), evitando debilidades de cada metodo individual.

**Convergencia:** Los 4 metodos coincidieron en las mismas 6 US para el MVP (US-001 a US-006), con consenso del 100%. Las diferencias aparecieron en features "fronterizas" como US-007 (Comunicaciones).

**Aprendizajes clave:**
- **Insight 1:** Los metodos convergen en el core, difieren en la periferia
- **Insight 2:** La objetividad (RICE) tiene costo - 3x mas tiempo que MoSCoW
- **Insight 3:** Story Mapping es la mejor herramienta de comunicacion, pero requiere facilitacion experta
- **Insight 4:** Kano es excelente para B2C, menos critico para B2B
- **Insight 5:** Ningun metodo captura "riesgo tecnico" explicitamente

**Recomendacion final:** Usa Story Mapping como metodo principal, complementado con Kano en discovery (identificar diferenciadores) y RICE como tiebreaker para features controversiales. Invierte 4-6h en este workflow hibrido - es 0.01% del presupuesto del proyecto pero previene errores que costarian 100-1000x mas.

**Score final:**
1. Story Mapping: 42/50
2. MoSCoW: 40/50
3. Kano + V/E: 35/50
4. RICE: 33/50

---

**Documento elaborado por:** Product Manager LTI ATS
**Fecha:** Diciembre 2025
**Version:** 1.0
**Metodos evaluados:** 4 (MoSCoW, RICE, Kano, Story Mapping)
**User Stories analizadas:** 11
**Tiempo de analisis:** ~8 horas (2h por metodo)

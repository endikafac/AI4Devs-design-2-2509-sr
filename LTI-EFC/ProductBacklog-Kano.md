# Product Backlog - LTI ATS MVP
## Modelo Kano + Matriz Value vs Effort

**Proyecto:** LTI ATS - Applicant Tracking System
**Método de Priorización:** Modelo Kano + Value/Effort Matrix
**Fecha:** Diciembre 2025
**Timeline:** 3 meses (6 sprints de 2 semanas)
**Equipo:** 5 devs full-stack + 1 ML engineer + 1 QA

---

## Paso 1: Clasificación Kano por User Story

### US-001: Crear Oferta de Empleo con Asistencia de IA
**Categoría Kano:** **Performance (Desempeño)**
**Justificación:** Los reclutadores esperan poder crear ofertas (Basic), pero la asistencia de IA que genera descripciones optimizadas incrementa la satisfacción linealmente. Cuanto mejor sea la IA en generar descripciones, mayor la satisfacción. Sin embargo, la funcionalidad básica de crear ofertas manualmente ya es esperada.

---

### US-002: Publicar Oferta en Múltiples Canales
**Categoría Kano:** **Basic (Básico)**
**Justificación:** Publicar ofertas es absolutamente esperado en cualquier ATS moderno. Su ausencia causa insatisfacción inmediata, pero su presencia no genera sorpresa ni deleite especial. Es un "must-have" funcional que los usuarios dan por sentado.

---

### US-003: Recibir y Parsear CVs Automáticamente
**Categoría Kano:** **Performance (Desempeño)**
**Justificación:** El parsing automático es un diferenciador competitivo. Cuanto mejor sea la precisión del parsing (85% → 95% → 99%), mayor la satisfacción. Los usuarios valoran linealmente cada mejora en la precisión. Es un "más es mejor" claro.

---

### US-004: Visualizar Pipeline de Candidatos Tipo Kanban
**Categoría Kano:** **Basic (Básico)**
**Justificación:** El pipeline Kanban es el estándar de la industria y absolutamente esperado. Todo ATS moderno tiene un tablero visual. Su ausencia sería inaceptable, pero su presencia no sorprende. Es hygiene factor, no diferenciador.

---

### US-005: Filtrar y Rankear Candidatos con IA
**Categoría Kano:** **Excitement (Sorpresa/Deleite)**
**Justificación:** El scoring predictivo con IA que rankea candidatos automáticamente es inesperado y genera "WOW". La mayoría de ATS requieren filtrado manual. Esta feature diferencia al producto y deleita a los usuarios. Su ausencia no molestaría (porque no lo esperan), pero su presencia genera encantamiento.

---

### US-006: Ver Perfil Completo de Candidato
**Categoría Kano:** **Basic (Básico)**
**Justificación:** Ver información detallada del candidato es absolutamente esperado. Es el equivalente a "ver detalles de un producto en un e-commerce". Sin esto, el sistema no es funcional. Presencia no aumenta satisfacción, pero ausencia la destruye.

---

### US-007: Enviar Comunicaciones Automáticas a Candidatos
**Categoría Kano:** **Performance (Desempeño)**
**Justificación:** Las comunicaciones automáticas son valoradas linealmente. Emails básicos → templates personalizados → comunicación omnicanal (email + SMS + WhatsApp). Cada mejora incrementa satisfacción. No es sorpresa (muchos ATS lo tienen), pero "más es mejor".

---

### US-008: Programar Entrevistas con Integración de Calendario
**Categoría Kano:** **Performance (Desempeño)**
**Justificación:** El scheduling automático incrementa satisfacción linealmente según su sofisticación: calendario simple → disponibilidad compartida → auto-scheduling con IA → integración con Zoom. Cada nivel mejora la experiencia. Es un feature esperado en ATS modernos, pero mejoras graduales aumentan valor.

---

### US-009: Completar Evaluación Colaborativa con Scorecard
**Categoría Kano:** **Performance (Desempeño)**
**Justificación:** Los scorecards son esperados (Basic en su forma simple), pero la colaboración en tiempo real, votaciones, comentarios sincronizados, y agregación inteligente de feedback elevan la satisfacción linealmente. "Más colaboración = mejor experiencia".

---

### US-010: Visualizar Dashboard con Métricas de Reclutamiento
**Categoría Kano:** **Indifferent (Indiferente)**
**Justificación:** Los dashboards de analytics son valorados principalmente por management, no por usuarios diarios (reclutadores). Para el usuario operativo, su ausencia no molesta significativamente en el día a día. Su presencia no genera gran satisfacción para el core user. Es un "nice to have" más que un driver de valor.

---

### US-011: Aprobar Oferta de Empleo Antes de Publicación
**Categoría Kano:** **Indifferent (Indiferente)**
**Justificación:** Los workflows de aprobación son valorados en organizaciones grandes con governance estricto, pero añaden fricción. En startups y empresas ágiles, se perciben como burocracia innecesaria. No genera satisfacción significativa y su ausencia no molesta a la mayoría. Es context-dependent.

---

## Paso 2: Matriz Value vs Effort - Tabla Completa

| US-ID | Título | Kano | Value (1-10) | Effort (SP) | Cuadrante | Prioridad |
|-------|--------|------|--------------|-------------|-----------|-----------|
| US-004 | Visualizar Pipeline Kanban | Basic | 10 | 5 | Quick Win | P0 |
| US-001 | Crear Oferta con IA | Performance | 9 | 5 | Quick Win | P0 |
| US-002 | Publicar en Múltiples Canales | Basic | 9 | 8 | Big Bet | P1 |
| US-006 | Ver Perfil Completo | Basic | 8 | 3 | Quick Win | P0 |
| US-003 | Parsear CVs con IA | Performance | 9 | 13 | Big Bet | P1 |
| US-005 | Rankear Candidatos con IA | Excitement | 10 | 13 | Big Bet | P1 |
| US-007 | Comunicaciones Automáticas | Performance | 7 | 5 | Quick Win | P0 |
| US-008 | Programar Entrevistas | Performance | 8 | 8 | Big Bet | P1 |
| US-009 | Evaluación Colaborativa | Performance | 8 | 8 | Big Bet | P1 |
| US-011 | Aprobar Oferta | Indifferent | 5 | 3 | Time Sink | P3 |
| US-010 | Dashboard de Métricas | Indifferent | 4 | 5 | Money Pit | P2 |

---

### Visualización de la Matriz

```
         HIGH VALUE (7-10)
            │
  Big Bets  │  Quick Wins
   (⏰ P1)  │  (⚡ P0)
            │
  US-002    │  US-004 (10,5) ⭐
  US-003    │  US-001 (9,5)  ⭐
  US-005    │  US-006 (8,3)  ⭐
  US-008    │  US-007 (7,5)
  US-009    │
────────────┼────────────
  US-010    │  US-011
   (💰 P2)  │  (❌ P3)
            │
    LOW VALUE (1-6)

      HIGH        LOW
       EFFORT
```

**Leyenda:**
- ⭐ = Features críticas para MVP
- 🔥 = Features diferenciadores (Excitement Kano)

---

## Paso 3: Backlog Priorizado por Cuadrantes

### 🔥 Prioridad P0 - Quick Wins (Sprint 1-3)

#### US-004: Visualizar Pipeline de Candidatos Tipo Kanban
- **Kano:** Basic | **Value:** 10/10 | **Effort:** 5 SP
- **Por qué P0:** Es la interfaz central del producto y bloqueante absoluto. Sin pipeline visual, el sistema no es usable. Complejidad moderada con tecnología madura (drag-and-drop). Máximo valor, esfuerzo razonable. **Enabler crítico para todas las demás features.**

#### US-001: Crear Oferta de Empleo con Asistencia de IA
- **Kano:** Performance | **Value:** 9/10 | **Effort:** 5 SP
- **Por qué P0:** Punto de entrada del flujo. Sin ofertas no hay proceso de reclutamiento. La asistencia de IA la eleva de Basic a Performance, generando valor inmediato sin complejidad excesiva. Quick win estratégico que muestra capacidades de IA desde el día 1.

#### US-006: Ver Perfil Completo de Candidato
- **Kano:** Basic | **Value:** 8/10 | **Effort:** 3 SP
- **Por qué P0:** Necesaria para revisar y evaluar candidatos. Sin perfiles, la información está fragmentada. Bajo esfuerzo (principalmente UI), alto valor. Permite tomar decisiones informadas. **Menor esfuerzo de todos los Quick Wins.**

#### US-007: Enviar Comunicaciones Automáticas a Candidatos
- **Kano:** Performance | **Value:** 7/10 | **Effort:** 5 SP
- **Por qué P0:** Mejora drásticamente la experiencia del candidato y reduce carga administrativa. Tecnología madura (SendGrid), moderada complejidad. Diferenciador operativo que automatiza tarea repetitiva. **Último Quick Win, puede posponerse a Sprint 3 si hay presión.**

---

### ⚠️ Prioridad P1 - Big Bets (Sprint 2-5)

#### US-002: Publicar Oferta en Múltiples Canales
- **Kano:** Basic | **Value:** 9/10 | **Effort:** 8 SP
- **Por qué P1:** Crítica para alcance de candidatos pero alta complejidad técnica (múltiples APIs externas). Inversión justificada porque sin publicación multicanal, el volumen de candidatos es insuficiente. **Big Bet necesario para viabilidad del negocio.**

#### US-003: Recibir y Parsear CVs Automáticamente
- **Kano:** Performance | **Value:** 9/10 | **Effort:** 13 SP
- **Por qué P1:** Corazón de la propuesta de valor de IA. Máxima complejidad técnica (NLP, OCR, NER) pero diferenciador competitivo crítico. Sin parsing, el reclutador transcribe manualmente, anulando el valor del producto. **Big Bet estratégico indispensable.**

#### US-005: Filtrar y Rankear Candidatos con IA
- **Kano:** Excitement (🔥) | **Value:** 10/10 | **Effort:** 13 SP
- **Por qué P1:** **Killer feature diferenciador.** El scoring predictivo es lo que genera "WOW" y reduce time-to-hire en 50%. Máxima complejidad (ML, embeddings, scoring) pero máximo valor. Es el feature que vende el producto. **Big Bet que justifica el posicionamiento premium.**

#### US-008: Programar Entrevistas con Integración de Calendario
- **Kano:** Performance | **Value:** 8/10 | **Effort:** 8 SP
- **Por qué P1:** Ahorra tiempo administrativo significativo pero alta complejidad de integración (Google Calendar, Outlook, zonas horarias). Inversión justificada para eficiencia operativa. **Big Bet de productividad.**

#### US-009: Completar Evaluación Colaborativa con Scorecard
- **Kano:** Performance | **Value:** 8/10 | **Effort:** 8 SP
- **Por qué P1:** Core de la colaboración en tiempo real. Alta complejidad (WebSocket, concurrencia) pero diferenciador clave. Mejora calidad de decisiones de contratación. **Big Bet de colaboración.**

---

### 💡 Prioridad P2 - Money Pits (Sprint 6 o backlog futuro)

#### US-010: Visualizar Dashboard con Métricas de Reclutamiento
- **Kano:** Indifferent | **Value:** 4/10 | **Effort:** 5 SP
- **Por qué P2:** Valorado principalmente por management, no por usuarios operativos diarios. Esfuerzo moderado pero valor limitado para el core user (reclutador). El MVP puede funcionar sin analytics sofisticado. **Evitar o simplificar: versión básica en Sprint 6 solo si hay capacidad.**

---

### 🚫 Prioridad P3 - Time Sinks (Won't Have v1)

#### US-011: Aprobar Oferta de Empleo Antes de Publicación
- **Kano:** Indifferent | **Value:** 5/10 | **Effort:** 3 SP
- **Por qué P3:** Añade fricción al proceso. Valorado solo en organizaciones con governance estricto. Bajo esfuerzo, pero bajo valor. No genera satisfacción significativa. **Posponer a v1.1 cuando clientes enterprise lo soliciten.**

---

## Paso 4: Estrategia de Priorización

### Párrafo 1: Estrategia General

La estrategia de priorización combina el **Modelo Kano para entender drivers de satisfacción** con la **Matriz Value/Effort para maximizar ROI**. Se priorizan primero los **Quick Wins** (P0) que son features **Basic** y **Performance** de bajo esfuerzo: pipeline Kanban, creación de ofertas, perfiles de candidatos, y comunicaciones automáticas. Estas 4 US permiten un flujo operativo básico en los primeros 3 sprints con mínima inversión. Los **Big Bets** (P1) incluyen las features de alta complejidad pero valor crítico: publicación multicanal, parsing de CVs, scoring con IA, scheduling, y evaluación colaborativa. Estas 5 US requieren inversión significativa (8-13 SP cada una) pero son indispensables para el diferenciador competitivo. Finalmente, las features **Indifferent** (US-10, US-11) se posponen o simplifican radicalmente (P2-P3) porque no generan satisfacción significativa en usuarios core.

---

### Párrafo 2: Diferenciación con Features "Excitement"

El backlog incluye **1 feature Excitement crítica: US-005 (Rankear Candidatos con IA)**. Este es el **"WOW factor"** que diferencia a LTI ATS de competidores tradicionales. Aunque tiene máxima complejidad (13 SP), genera encantamiento porque es inesperado: la mayoría de ATS requieren filtrado manual o filtros básicos. El scoring predictivo con explicabilidad ("Por qué este candidato es 95% compatible") es lo que vende el producto en demos y genera virality. La estrategia es implementar esta feature en **Sprints 3-4** (después del walking skeleton básico) para tener una versión impresionante que pueda demostrar el valor único de IA. **Trade-off:** Invertiríamos 13 SP en esta feature cuando podríamos hacer 2-3 features simples, pero el diferenciador competitivo justifica la apuesta. Sin US-005, LTI ATS sería un ATS genérico más.

---

### Párrafo 3: Balance MVP

El MVP balancea:

1. **Basic (4 features):** US-002 (publicar), US-004 (Kanban), US-006 (perfil). Estas son **non-negotiable** porque su ausencia causa insatisfacción inmediata. Sin ellas, el producto no es funcional.

2. **Performance (5 features):** US-001 (crear con IA), US-003 (parsing), US-007 (comunicaciones), US-008 (scheduling), US-009 (evaluación). Estas son **value drivers** que incrementan satisfacción linealmente. Se incluyen las más críticas (crear, parsing, comunicaciones) en P0-P1, mientras que scheduling y evaluación pueden ser versiones simplificadas si hay presión de tiempo.

3. **Excitement (1 feature):** US-005 (scoring IA). Es el **diferenciador killer**. Se prioriza P1 (Big Bet) porque aunque es costoso, genera el "WOW" necesario para posicionamiento premium.

4. **Indifferent (2 features):** US-010 (dashboard), US-011 (aprobaciones). Se minimizan o posponen (P2-P3) porque no impactan satisfacción del core user.

**Balance estratégico:** 36% Basic, 45% Performance, 9% Excitement, 18% Indifferent. El MVP se enfoca en hygiene factors (Basic) + value drivers (Performance) + 1 diferenciador (Excitement), mientras elimina noise (Indifferent).

---

## Paso 5: Análisis de Trade-offs

### Trade-off #1: US-005 (Scoring IA) vs. US-008 + US-009 (Scheduling + Evaluación)

**Dilema:** Con 13 SP, podemos implementar el scoring con IA (US-005) O las dos features de evaluación colaborativa (US-008: 8 SP + US-009: 8 SP = 16 SP, pero con overlap podríamos hacer ambas en ~13 SP optimizando). ¿Priorizamos el diferenciador de IA o la colaboración completa?

**Opción A - Scoring IA (US-005):**
- **Pro:** Diferenciador único, genera "WOW", reduce time-to-hire 50%, posicionamiento premium, valor en demos.
- **Contra:** No permite evaluación estructurada post-screening, el proceso queda incompleto sin herramientas de decisión colaborativa.

**Opción B - Scheduling + Evaluación (US-008 + US-009):**
- **Pro:** Completa el flujo end-to-end incluyendo evaluación, mejora colaboración del equipo, menos riesgo técnico.
- **Contra:** Sin scoring IA, el producto es un ATS genérico sin diferenciador. Pierde el "magic moment".

**Decisión tomada:** **Opción A (US-005 Scoring IA)**. Justificación: El diferenciador de IA es más crítico para el posicionamiento de mercado. La evaluación colaborativa puede hacerse inicialmente con herramientas externas (Google Docs, Notion) como workaround temporal, pero el scoring con IA no puede replicarse fácilmente y es el hook de ventas principal. US-008 y US-009 se implementan en P1 pero después del scoring.

---

### Trade-off #2: US-002 (Publicar Multicanal) - ¿8 job boards o 2?

**Dilema:** La integración con múltiples job boards tiene esfuerzo variable. Integrar LinkedIn + Indeed (los 2 más importantes) = ~5 SP. Integrar 8 job boards (LinkedIn, Indeed, Glassdoor, Monster, ZipRecruiter, Wellfound, RemoteOK, Workable) = 8 SP. ¿Hacemos multicanal completo o MVP con top 2?

**Opción A - Top 2 (LinkedIn + Indeed):**
- **Pro:** Menor esfuerzo (5 SP), 70% del volumen de candidatos, lanzamiento más rápido.
- **Contra:** "Multicanal" suena limitado con solo 2, expectativas de clientes pueden ser 5-8 integraciones.

**Opción B - 8 job boards completos:**
- **Pro:** Verdadero "multicanal", diferenciador competitivo fuerte, alcance maximizado.
- **Contra:** Alto esfuerzo (8 SP), cada integración añade dependencia externa y riesgo, mantenimiento complejo.

**Decisión tomada:** **Opción intermedia: Top 4 (LinkedIn, Indeed, Glassdoor, Monster) = 6-7 SP**. Justificación: Los top 4 cubren 85-90% del volumen de candidatos y justifican el claim de "multicanal" sin sobrecarga técnica. Las integraciones adicionales (ZipRecruiter, Wellfound, etc.) se añaden en v1.1 basado en demanda real de clientes. Pragmatismo: suficiente diferenciación sin overengineering.

---

### Trade-off #3: US-010 (Dashboard) - ¿Versión básica o eliminar completamente del MVP?

**Dilema:** El dashboard tiene valor limitado para usuarios operativos (reclutadores) pero es importante para managers y para justificar ROI del producto. ¿Invertimos 5 SP en versión básica o eliminamos completamente y lanzamos sin analytics?

**Opción A - Dashboard básico (5 SP):**
- **Pro:** Permite a management ver métricas clave (time-to-hire, conversion rates), ayuda a vender el producto a executives, demuestra impacto.
- **Contra:** Esfuerzo moderado (5 SP) para feature que no usan reclutadores diariamente. Ese esfuerzo podría ir a refinar US-003 o US-005.

**Opción B - Sin dashboard en MVP:**
- **Pro:** Ahorra 5 SP que pueden invertirse en mejorar parsing o scoring (core value), lanzamiento más enfocado.
- **Contra:** Dificulta ventas a nivel C-suite (CFO, COO quieren ver ROI cuantificado), percepción de "producto incompleto".

**Decisión tomada:** **Opción A con alcance ultra-reducido: Dashboard "mini" (3 SP) solo en Sprint 6 si hay capacidad**. Justificación: Incluir métricas básicas (time-to-hire promedio, # candidatos por etapa, fuente más efectiva) en una sola vista simple. No es prioritario para operaciones pero facilita ventas B2B. Se implementa solo si Sprint 6 tiene buffer después de completar todas las P0-P1. Si hay presión, se pospone a v1.1 sin afectar lanzamiento.

---

## Paso 6: Distribución en Sprints

### Sprint 1-2 (Primeras 4 semanas): Walking Skeleton + Quick Wins

**User Stories:**
- ✅ **US-001:** Crear Oferta con IA (5 SP) - Sprint 1
- ✅ **US-004:** Pipeline Kanban (5 SP) - Sprint 2
- ✅ **US-006:** Ver Perfil Completo (3 SP) - Sprint 2
- 🔄 **US-002:** Publicar Multicanal (8 SP) - Inicio en Sprint 1, completar en Sprint 2

**Entregable:** Un reclutador puede crear una oferta con asistencia de IA, publicarla en LinkedIn e Indeed, y cuando llegan candidatos (manualmente o via webhook), verlos en un tablero Kanban drag-and-drop y acceder a perfiles completos. **Milestone:** Walking skeleton funcional end-to-end.

**Story Points totales:** 21 SP en 4 semanas (asumiendo ~40-45 SP de capacidad con 5 devs)

---

### Sprint 3-4 (Semanas 5-8): IA Core + Performance

**User Stories:**
- ✅ **US-003:** Parsear CVs con IA (13 SP) - Sprint 3-4 (feature compleja, 2 sprints)
- ✅ **US-005:** Rankear con IA (13 SP) - Sprint 3-4 (paralelo a US-003, ML engineer)
- ✅ **US-007:** Comunicaciones Automáticas (5 SP) - Sprint 3

**Entregable:** Los CVs recibidos se parsean automáticamente con >85% precisión (nombre, email, skills, experiencia). Los candidatos se rankean con scoring predictivo (0-100) y aparecen ordenados en el Kanban. El sistema envía emails automáticos cuando cambian de etapa. **Milestone:** MVP con diferenciador de IA completo, listo para beta testing.

**Story Points totales:** 31 SP en 4 semanas

**Nota:** US-003 y US-005 requieren 2 sprints cada una pero se trabajan en paralelo por equipos diferentes (devs backend en parsing, ML engineer en scoring).

---

### Sprint 5-6 (Semanas 9-12): Evaluación Colaborativa + Pulido

**User Stories:**
- ✅ **US-008:** Programar Entrevistas (8 SP) - Sprint 5
- ✅ **US-009:** Evaluación Colaborativa (8 SP) - Sprint 5-6
- ⚠️ **US-010:** Dashboard Métricas (3 SP versión mini) - Sprint 6 (solo si hay capacidad)
- 🔧 **Deuda técnica, bugs, performance, documentación** - Sprint 6

**Entregable:** Los reclutadores pueden programar entrevistas con sincronización automática de calendarios (Google/Outlook). Los entrevistadores completan scorecards estructurados con comentarios en tiempo real y votaciones colaborativas. Dashboard básico muestra métricas clave. **Milestone:** MVP completo listo para producción.

**Story Points totales:** 16-19 SP en 4 semanas (dejando buffer intencional de ~20 SP para pulido)

---

### Resumen de Distribución

| Sprint | Semanas | User Stories | SP Totales | Milestone |
|--------|---------|--------------|------------|-----------|
| **Sprint 1-2** | 1-4 | US-001, US-002, US-004, US-006 | 21 | Walking skeleton end-to-end |
| **Sprint 3-4** | 5-8 | US-003, US-005, US-007 | 31 | MVP con diferenciador IA (Beta Ready) |
| **Sprint 5-6** | 9-12 | US-008, US-009, US-010 (mini), pulido | 16-19 | MVP completo listo producción |

**Total SP implementados:** 68-71 SP en 6 sprints (11-12 SP/sprint promedio, razonable para equipo de 6 personas técnicas)

---

## Paso 7: Justificación de Exclusiones y Simplificaciones

### Features Eliminadas del MVP (Won't Have v1)

**US-011: Aprobar Oferta de Empleo Antes de Publicación** (Prioridad P3)
- **Razón de exclusión:** Kano "Indifferent". Añade fricción al proceso y es valorado solo en organizaciones enterprise con governance estricto. El MVP target son startups y scale-ups que prefieren velocidad sobre control. Feature movida a v1.1 cuando tengamos clientes enterprise que explícitamente lo soliciten.
- **Workaround temporal:** Las ofertas pueden revisarse manualmente antes de hacer clic en "Publicar". El Manager simplemente valida pre-publicación sin workflow formal.

---

### Features Simplificadas

**US-010: Dashboard de Métricas** (Prioridad P2 → Mini versión)
- **Razón de simplificación:** Kano "Indifferent" para core users. Esfuerzo original 5 SP, reducido a 3 SP con alcance ultra-limitado: solo time-to-hire promedio, candidatos por etapa, y fuente más efectiva. Reportes avanzados, filtros complejos, y exportación se mueven a v1.1.
- **Implementación condicional:** Solo se implementa en Sprint 6 si hay capacidad después de completar todas las P0-P1. Si hay presión de tiempo, se elimina completamente del MVP sin impacto.

**US-002: Publicar Multicanal** (8 job boards → 4 job boards)
- **Razón de simplificación:** Balance entre claim de "multicanal" y esfuerzo técnico. Top 4 (LinkedIn, Indeed, Glassdoor, Monster) cubren 85-90% del volumen. Integraciones 5-8 se añaden en v1.1 basado en demanda real.

---

## Conclusión: Balance Estratégico Kano

### Distribución del Backlog por Categoría Kano

| Categoría Kano | # User Stories | % Backlog | Prioridad | Estrategia |
|----------------|----------------|-----------|-----------|------------|
| **Basic** | 3 (US-002, US-004, US-006) | 27% | P0-P1 | Non-negotiable, todas incluidas en MVP |
| **Performance** | 5 (US-001, US-003, US-007, US-008, US-009) | 45% | P0-P1 | Core value drivers, todas incluidas, algunas versiones simplificadas |
| **Excitement** | 1 (US-005) | 9% | P1 | Killer differentiator, prioridad alta (Big Bet estratégico) |
| **Indifferent** | 2 (US-010, US-011) | 18% | P2-P3 | Minimizar o eliminar, bajo ROI para core users |

---

### Matriz de Satisfacción Esperada

**Sin MVP (competidor tradicional):**
- Basic features ausentes → **Insatisfacción alta** ❌
- Performance features limitadas → **Satisfacción baja** 😐
- Excitement features no existen → **Neutral** (no lo esperaban) 🤷

**Con LTI ATS MVP:**
- **Basic features completas** → Satisfacción neutral (esperado) ✅
- **Performance features completas** → **Satisfacción alta** (mejora lineal) 😊
- **1 Excitement feature (Scoring IA)** → **Encantamiento** (WOW factor) 🤩
- Indifferent features ausentes → Neutral (no afecta) 🤷

**Resultado:** Satisfacción neta muy alta con esfuerzo optimizado, gracias a eliminar Indifferent y maximizar inversión en Excitement + Performance.

---

### Próximos Pasos

1. **Sprint Planning Sprint 1:**
   - Grooming detallado de US-001 (Crear Oferta con IA)
   - Story splitting de US-002 (Publicar Multicanal) en tareas por job board
   - Estimación en story points con planning poker
   - Definición de acceptance criteria con ejemplos concretos

2. **Setup técnico:**
   - Repos (monorepo vs multi-repo)
   - CI/CD pipeline (GitHub Actions)
   - Entornos (dev, staging, prod)
   - Setup de integraciones de IA (OpenAI API key, rate limits)

3. **Validación de asunciones:**
   - User testing del wireframe de Kanban con 5 reclutadores
   - Validar precisión esperada del parsing (benchmark con CVs reales)
   - Pilotos de scoring IA con datasets de candidatos reales

4. **Kickoff Sprint 1** 🚀

---

**Documento elaborado por:** Product Manager LTI ATS
**Método:** Modelo Kano + Matriz Value vs Effort
**Fecha:** Diciembre 2025
**Versión:** 2.0 (Kano)

---

## Anexo: Comparación con Método Anterior (MoSCoW)

| Aspecto | MoSCoW (v1.0) | Kano + Value/Effort (v2.0) |
|---------|---------------|---------------------------|
| **Método** | Categorización cualitativa | Cuantitativo (Value 1-10, Effort SP) |
| **Enfoque** | Dependencias técnicas + flujo | ROI (Value/Effort) + drivers de satisfacción |
| **Diferenciador** | Implícito en "Must Have" | Explícito con categoría "Excitement" |
| **US-005 (Scoring IA)** | Must Have (junto a otras 5) | **Excitement** destacado como killer feature |
| **US-010 (Dashboard)** | Could Have (Sprint 6) | **Indifferent** → P2 (eliminar o mini versión) |
| **US-011 (Aprobaciones)** | Could Have (Sprint 5-6) | **Indifferent** → P3 (Won't Have v1) |
| **Trade-offs** | Implícitos | **Explícitos y documentados** (3 trade-offs) |
| **Claridad de ROI** | Media (basado en intuición PM) | **Alta** (matriz visual, cuadrantes claros) |

**Conclusión de comparación:** El método Kano + Value/Effort proporciona **mayor claridad para stakeholders no técnicos** (executives, inversores) porque visualiza ROI explícitamente y diferencia entre hygiene factors (Basic), value drivers (Performance), y diferenciadores (Excitement). Es especialmente útil para justificar decisiones de priorización en board meetings y roadmap discussions.

# Product Backlog - LTI ATS MVP
## Método de Priorización: RICE Score

**Proyecto:** LTI ATS - Applicant Tracking System
**Versión:** 1.0
**Método de Priorización:** RICE Score
**Fecha:** Diciembre 2025
**Timeline:** 3 meses (6 sprints de 2 semanas)
**Capacidad Total:** 240 Story Points (40 SP por sprint)
**Equipo:** 5 devs full-stack + 1 ML engineer + 1 QA

---

## Fórmula RICE

**RICE Score = (Reach × Impact × Confidence) / Effort**

### Definiciones para LTI ATS

**Reach (Alcance - 0-1000):** ¿Cuántos usuarios/procesos afecta por mes?
- Todos los procesos de contratación = 100
- Todos los reclutadores diariamente = 80
- Managers semanalmente = 30
- Candidatos = 200 (múltiples candidatos por oferta)
- Feature ocasional = 10

**Impact (Impacto - 0.25, 0.5, 1, 2, 3):** ¿Cuánto mejora la experiencia/proceso?
- 3 = Impacto masivo (reducción 50%+ tiempo, diferenciador clave)
- 2 = Impacto alto (mejora significativa workflow)
- 1 = Impacto medio (mejora moderada)
- 0.5 = Impacto bajo
- 0.25 = Impacto mínimo

**Confidence (Confianza - 50%, 80%, 100%):** ¿Qué certeza tenemos de Reach/Impact?
- 100% = Datos sólidos, funcionalidad probada en otros ATS
- 80% = Estimación razonable basada en investigación
- 50% = Suposición/hipótesis

**Effort (Esfuerzo - Story Points):** Estimación Fibonacci (1, 2, 3, 5, 8, 13, 21)
- 1-2 SP = Tarea simple (1-3 días)
- 3-5 SP = Funcionalidad media (1 semana)
- 8 SP = Funcionalidad compleja (2 semanas)
- 13 SP = Muy complejo (2-3 semanas)
- 21 SP = Épico (debe dividirse)

---

## Tabla de Análisis RICE - Todas las User Stories

| ID | Título | Reach | Impact | Confidence | Effort (SP) | **RICE Score** | **Ranking** |
|----|--------|-------|--------|------------|-------------|----------------|-------------|
| US-001 | Crear Oferta con IA | 100 | 2 | 80% | 5 | **32.0** | 1 |
| US-004 | Pipeline Kanban | 80 | 3 | 100% | 8 | **30.0** | 2 |
| US-003 | Parsear CVs con IA | 200 | 3 | 80% | 21 | **22.9** | 3 |
| US-006 | Perfil Completo de Candidato | 80 | 2 | 100% | 8 | **20.0** | 4 |
| US-005 | Filtrar y Rankear con IA | 100 | 3 | 80% | 13 | **18.5** | 5 |
| US-002 | Publicar en Múltiples Canales | 100 | 2 | 80% | 13 | **12.3** | 6 |
| US-007 | Comunicaciones Automáticas | 200 | 1 | 80% | 13 | **12.3** | 7 |
| US-011 | Aprobar Oferta (Workflow) | 30 | 1 | 100% | 3 | **10.0** | 8 |
| US-008 | Programar Entrevistas | 30 | 2 | 80% | 8 | **6.0** | 9 |
| US-009 | Evaluación Colaborativa | 30 | 2 | 80% | 13 | **3.7** | 10 |
| US-010 | Dashboard con Métricas | 10 | 1 | 80% | 8 | **1.0** | 11 |

---

## Top 10 Priorizadas (orden descendente de RICE)

### #1 - US-001: Crear Oferta con IA (RICE: 32.0)

**¿Por qué RICE alto?**
- **Reach (100):** Afecta absolutamente todos los procesos de reclutamiento, ya que sin ofertas no puede iniciarse ningún flujo
- **Impact (2):** Alto impacto al reducir el tiempo de creación de ofertas de 2 horas a 15 minutos con asistencia de IA. Genera descripciones optimizadas SEO que aumentan candidaturas en 30%
- **Confidence (80%):** Funcionalidad probada en otros ATS modernos (Lever, Greenhouse). La integración con LLM es tecnología madura
- **Effort (5 SP):** Complejidad moderada - formularios, validaciones, integración con LLM (OpenAI/Anthropic), gestión de estados
- **Resultado:** (100 × 2 × 0.8) / 5 = **32.0** - El RICE más alto del backlog

**Riesgos identificados:**
- Dependencia externa de API de LLM (OpenAI/Anthropic) - necesita circuit breaker y fallback manual
- Calidad de los prompts para generación de descripciones - requiere iteración y refinamiento
- Gestión de estados (draft, pending approval, active) puede requerir workflow adicional

**Quick Win:** ⚡ **SI** - RICE alto (32.0) con Effort bajo-medio (5 SP). Es la funcionalidad fundacional con mejor ROI y debe implementarse primero.

---

### #2 - US-004: Pipeline Kanban (RICE: 30.0)

**¿Por qué RICE alto?**
- **Reach (80):** Usada diariamente por todos los reclutadores y managers - es la interfaz principal del producto
- **Impact (3):** Impacto masivo - el paradigma visual tipo Kanban es el estándar de la industria. Reduce tiempo de gestión de candidatos en 60% vs listas lineales
- **Confidence (100%):** Patrón completamente validado en todos los ATS modernos. Librerías maduras (react-beautiful-dnd)
- **Effort (8 SP):** Complejidad moderada-alta - drag-and-drop, actualización de estados, filtros, búsqueda, manejo de performance
- **Resultado:** (80 × 3 × 1.0) / 8 = **30.0**

**Riesgos identificados:**
- Performance con cientos de candidatos - necesita virtualización y paginación desde el inicio
- Sincronización en tiempo real si múltiples usuarios mueven candidatos simultáneamente
- Manejo de estados y transiciones complejas entre etapas

**Quick Win:** ⚡ **NO** - Aunque tiene RICE muy alto, el Effort de 8 SP lo coloca en complejidad media-alta. Sin embargo, es crítico para el MVP.

---

### #3 - US-003: Parsear CVs con IA (RICE: 22.9)

**¿Por qué RICE alto?**
- **Reach (200):** Afecta a todos los candidatos (múltiples por oferta), procesando cientos de CVs mensualmente por cliente
- **Impact (3):** Impacto masivo - automatiza la tarea más tediosa del reclutamiento. Reduce tiempo de screening en 60%. Es el core del diferenciador de IA
- **Confidence (80%):** Tecnología probada (SpaCy NER, transformers) pero con incertidumbre en precisión inicial. Requiere iteración
- **Effort (21 SP):** Muy complejo - procesamiento de múltiples formatos (PDF, DOCX, imágenes), OCR, NER, extracción de skills, experiencia, educación
- **Resultado:** (200 × 3 × 0.8) / 21 = **22.9**

**Riesgos identificados:**
- Precisión del parsing es crítica - CVs mal parseados generan frustración masiva. Meta: >85% precisión en campos críticos
- Múltiples formatos de CV (PDF, DOCX, escaneados, formatos creativos) requieren procesamiento robusto
- Necesita fallback manual y proceso de mejora continua de modelos
- Dependencia del ML engineer - es el cuello de botella técnico

**Quick Win:** ⚡ **NO** - Aunque tiene RICE alto (22.9), el Effort de 21 SP es el más alto del backlog. Debe dividirse en dos sprints: parsing básico (Sprint 2) y parsing avanzado (Sprint 3).

---

### #4 - US-006: Perfil Completo de Candidato (RICE: 20.0)

**¿Por qué RICE alto?**
- **Reach (80):** Usado diariamente por reclutadores, managers y entrevistadores para revisar candidatos
- **Impact (2):** Alto impacto - consolida toda la información en un solo lugar. Reduce tiempo de revisión pre-entrevista de 20 a 5 minutos
- **Confidence (100%):** Funcionalidad estándar en todos los ATS. Patrón de UI bien conocido (tabs, timeline, documentos)
- **Effort (8 SP):** Complejidad moderada-alta - vista de datos, timeline de interacciones, documentos adjuntos, historial
- **Resultado:** (80 × 2 × 1.0) / 8 = **20.0**

**Riesgos identificados:**
- Performance con muchos documentos adjuntos (CVs, cartas, portafolios) - necesita carga lazy
- Visualización de CVs en múltiples formatos debe ser consistente
- Historial de interacciones puede crecer indefinidamente - necesita paginación

**Quick Win:** ⚡ **NO** - RICE alto pero Effort de 8 SP. Es esencial para el MVP pero no es un Quick Win por complejidad.

---

### #5 - US-005: Filtrar y Rankear con IA (RICE: 18.5)

**¿Por qué RICE alto?**
- **Reach (100):** Afecta todos los procesos de selección - cada oferta requiere ranking de candidatos
- **Impact (3):** Impacto masivo - es el diferenciador killer del producto. Scoring y ranking automático reduce time-to-hire en 50% y mejora calidad de matching en 40%
- **Confidence (80%):** Tecnología emergente en ATS. Existen casos de éxito pero con variabilidad en precisión. Requiere validación con usuarios reales
- **Effort (13 SP):** Muy complejo - modelo de scoring (ML), embeddings semánticos, comparación con requisitos, generación de resúmenes con LLM, explicabilidad
- **Resultado:** (100 × 3 × 0.8) / 13 = **18.5**

**Riesgos identificados:**
- Precisión del scoring es determinante para el éxito del producto - necesita >70% de acierto en top 3 candidatos
- Bias en el modelo puede generar discriminación - requiere auditoría y explicabilidad desde el inicio
- Subjetividad en "mejor candidato" varía por empresa y rol - necesita calibración
- Dependencia crítica del ML engineer para modelo de scoring y embeddings

**Quick Win:** ⚡ **NO** - RICE alto (18.5) pero Effort de 13 SP. Es complejo y debe dividirse en scoring básico (Sprint 3) y refinamiento (Sprint 4).

---

### #6 - US-002: Publicar en Múltiples Canales (RICE: 12.3)

**¿Por qué RICE alto?**
- **Reach (100):** Afecta todos los procesos - cada oferta debe publicarse para recibir candidatos
- **Impact (2):** Alto impacto - multiposting aumenta el volumen de candidaturas en 3-5x vs publicación manual en 1-2 canales
- **Confidence (80%):** Integraciones con job boards son comunes pero cada API tiene peculiaridades. Requiere manejo robusto de errores
- **Effort (13 SP):** Muy complejo - múltiples integraciones API (LinkedIn, Indeed, job boards), webhooks, retry logic, tracking de fuentes
- **Resultado:** (100 × 2 × 0.8) / 13 = **12.3**

**Riesgos identificados:**
- Múltiples dependencias externas - cada job board tiene limitaciones, rate limits, y formato específico
- APIs pueden fallar o cambiar - necesita circuit breakers y monitoreo constante
- Costos de publicación en job boards premium (LinkedIn, Indeed) pueden ser altos
- Tracking de fuente de candidatos requiere webhooks y puede tener delays

**Quick Win:** ⚡ **NO** - RICE medio (12.3) con Effort alto (13 SP). Crítico para el MVP pero debe implementarse gradualmente (1-2 job boards en Sprint 1, resto en Sprint 2).

---

### #7 - US-007: Comunicaciones Automáticas (RICE: 12.3)

**¿Por qué RICE alto?**
- **Reach (200):** Afecta a todos los candidatos - cada uno recibe múltiples emails durante el proceso (confirmación, rechazo, invitación a entrevista)
- **Impact (1):** Impacto medio - mejora significativamente la experiencia del candidato y reduce carga administrativa del reclutador (ahorra 30 min/día)
- **Confidence (80%):** Funcionalidad estándar en ATS modernos. Integraciones con email providers (SendGrid) son maduras
- **Effort (13 SP):** Complejidad media-alta - integración con email provider, templates dinámicos, triggers basados en eventos, configuración SPF/DKIM
- **Resultado:** (200 × 1 × 0.8) / 13 = **12.3**

**Riesgos identificados:**
- Emails marcados como spam - necesita configuración correcta de SPF, DKIM, DMARC desde el inicio
- Templates deben ser personalizables por empresa y rol
- Manejo de bounces y unsubscribes requiere flujo adicional
- Timing de envío de emails crítico - no enviar en horarios inapropiados

**Quick Win:** ⚡ **NO** - RICE medio (12.3) con Effort alto (13 SP). Importante para experiencia del candidato pero puede ser semi-automático en MVP inicial.

---

### #8 - US-011: Aprobar Oferta (Workflow) (RICE: 10.0)

**¿Por qué RICE alto?**
- **Reach (30):** Afecta principalmente a managers de contratación que revisan ofertas semanalmente antes de publicar
- **Impact (1):** Impacto medio - mejora control de calidad y governance. Evita publicaciones incorrectas que pueden dañar employer branding
- **Confidence (100%):** Workflow de aprobación es patrón estándar en sistemas enterprise. Tecnología bien conocida
- **Effort (3 SP):** Baja complejidad - workflow simple (draft → pending → approved → rejected), notificaciones, comentarios de revisión
- **Resultado:** (30 × 1 × 1.0) / 3 = **10.0**

**Riesgos identificados:**
- Añade fricción al proceso - puede ralentizar time-to-publish si los aprobadores no responden rápido
- Necesita notificaciones push para que los managers actúen rápido
- Debe tener opción de "publicación directa" para reclutadores senior

**Quick Win:** ⚡ **SI** - RICE medio (10.0) con Effort muy bajo (3 SP). Es una funcionalidad simple que puede implementarse rápidamente en Sprint 5 si hay capacidad.

---

### #9 - US-008: Programar Entrevistas (RICE: 6.0)

**¿Por qué RICE medio?**
- **Reach (30):** Afecta principalmente a reclutadores y managers que programan entrevistas semanalmente (no todos los candidatos llegan a esta etapa)
- **Impact (2):** Alto impacto para los usuarios que lo usan - elimina el "ping-pong" de emails para encontrar horarios. Ahorra 20 min por entrevista
- **Confidence (80%):** Integraciones de calendario son complejas y tienden a fallar. Necesita testing exhaustivo
- **Effort (8 SP):** Alta complejidad - integración con Google Calendar y Outlook, zonas horarias, conflictos, disponibilidad compartida
- **Resultado:** (30 × 2 × 0.8) / 8 = **6.0**

**Riesgos identificados:**
- APIs de calendario (Google, Microsoft) son complejas y frágiles - necesita fallback manual robusto
- Manejo de zonas horarias es crítico para empresas distribuidas
- Conflictos de calendario y disponibilidad compartida añaden complejidad
- Necesita permisos OAuth de usuarios (puede tener fricción en onboarding)

**Quick Win:** ⚡ **NO** - RICE medio-bajo (6.0) con Effort alto (8 SP). Importante pero no crítico para MVP - puede hacerse manualmente en fase inicial.

---

### #10 - US-009: Evaluación Colaborativa (RICE: 3.7)

**¿Por qué RICE bajo?**
- **Reach (30):** Afecta principalmente a entrevistadores y managers que completan scorecards post-entrevista (solo candidatos que llegaron a entrevista)
- **Impact (2):** Alto impacto para decisiones de calidad - centraliza feedback y elimina silos. Mejora consistencia de evaluaciones
- **Confidence (80%):** Funcionalidad de colaboración en tiempo real añade complejidad técnica (WebSocket, concurrencia). Requiere testing exhaustivo
- **Effort (13 SP):** Muy complejo - scorecards configurables, ponderación, agregación de scores, comentarios en tiempo real, votaciones, concurrencia
- **Resultado:** (30 × 2 × 0.8) / 13 = **3.7**

**Riesgos identificados:**
- Colaboración en tiempo real (WebSocket) añade complejidad técnica significativa
- Sincronización de estado entre múltiples usuarios puede tener race conditions
- Scorecards deben ser configurables por rol y empresa - añade flexibilidad pero complejidad
- Testing de concurrencia requiere esfuerzo adicional de QA

**Quick Win:** ⚡ **NO** - RICE bajo (3.7) con Effort muy alto (13 SP). Importante para diferenciación pero puede implementarse post-MVP o de forma simplificada (sin tiempo real).

---

### #11 - US-010: Dashboard con Métricas (RICE: 1.0)

**¿Por qué RICE bajo?**
- **Reach (10):** Usado ocasionalmente por managers y admins para revisar métricas (semanalmente o mensualmente)
- **Impact (1):** Impacto medio - ayuda a justificar ROI del ATS y optimizar procesos, pero no es necesario para operaciones diarias
- **Confidence (80%):** Funcionalidad estándar de reporting. Tecnología madura (Chart.js, Recharts) pero con incertidumbre en qué métricas son realmente útiles
- **Effort (8 SP):** Complejidad moderada-alta - agregación de datos, cálculo de métricas (time-to-hire, conversion rates), visualizaciones, filtros
- **Resultado:** (10 × 1 × 0.8) / 8 = **1.0** - El RICE más bajo del backlog

**Riesgos identificados:**
- Performance con grandes volúmenes de datos históricos - necesita agregaciones eficientes e índices
- Definición de métricas relevantes requiere validación con usuarios
- Puede convertirse en "scope creep" si se agregan muchas métricas innecesarias

**Quick Win:** ⚡ **NO** - RICE muy bajo (1.0) con Effort alto (8 SP). Debe ser versión básica en Sprint 6 o moverse a v1.1 si hay retrasos.

---

## Distribución en Sprints (40 SP por sprint)

### **Sprint 1 (40 SP): Foundation - Gestión de Ofertas**

- **US-001:** Crear Oferta con IA **(5 SP)** - RICE: 32.0
- **US-002:** Publicar en Múltiples Canales **(13 SP)** - RICE: 12.3
- **Setup técnico:** Infraestructura, repos, CI/CD, DB schema **(22 SP)**

**Total:** 40 SP
**Entregable:** Reclutador puede crear ofertas con asistencia de IA y publicarlas en 1-2 job boards (LinkedIn, Indeed)

**Justificación:** US-001 tiene el RICE más alto (32.0) y es fundacional - sin ofertas no hay proceso. US-002 es crítica para que las ofertas lleguen a candidatos. Ambas son "Must Have" y no tienen dependencias.

---

### **Sprint 2 (40 SP): Ingesta y Visualización**

- **US-003:** Parsear CVs con IA - Fase 1: Parsing básico **(13 SP)** - RICE: 22.9
- **US-004:** Pipeline Kanban **(8 SP)** - RICE: 30.0
- **US-002:** Publicar - Completar integraciones adicionales **(10 SP)**
- **Testing & Fixes:** **(9 SP)**

**Total:** 40 SP
**Entregable:** CVs se parsean automáticamente (extracción básica: nombre, email, experiencia) y candidatos aparecen en tablero Kanban drag-and-drop

**Justificación:** US-004 tiene el 2do RICE más alto (30.0) y es la interfaz principal del producto. US-003 tiene RICE alto (22.9) pero por su complejidad (21 SP total) se divide en dos fases. Sprint 2 implementa parsing básico funcional.

---

### **Sprint 3 (40 SP): Inteligencia y Perfiles**

- **US-003:** Parsear CVs con IA - Fase 2: Parsing avanzado **(8 SP)** - RICE: 22.9
- **US-005:** Filtrar y Rankear con IA - Fase 1: Scoring básico **(8 SP)** - RICE: 18.5
- **US-006:** Perfil Completo de Candidato **(8 SP)** - RICE: 20.0
- **Refinamiento y Testing:** **(16 SP)**

**Total:** 40 SP
**Entregable:** Parsing avanzado de skills y experiencia estructurada. Candidatos rankeados con score de compatibilidad (0-100). Perfiles completos con timeline e historial.

**Justificación:** Sprint 3 completa el "walking skeleton" del MVP - flujo end-to-end funcional. US-006 (RICE: 20.0) es crítica para revisar candidatos. US-005 (RICE: 18.5) es el diferenciador de IA pero se implementa gradualmente.

**MILESTONE CRÍTICO:** Al final de Sprint 3, el sistema permite crear oferta → publicar → recibir CVs → ver en Kanban rankeados por IA → ver perfiles completos. **MVP mínimo viable para beta testing.**

---

### **Sprint 4 (40 SP): Evaluación Estructurada**

- **US-005:** Filtrar y Rankear con IA - Fase 2: Refinamiento con feedback **(5 SP)** - RICE: 18.5
- **US-008:** Programar Entrevistas **(8 SP)** - RICE: 6.0
- **US-009:** Evaluación Colaborativa - Fase 1: Scorecards básicos **(8 SP)** - RICE: 3.7
- **Optimización de Performance:** **(10 SP)**
- **Testing & Fixes:** **(9 SP)**

**Total:** 40 SP
**Entregable:** Scoring de IA refinado con feedback real. Programación de entrevistas sincronizada con Google Calendar/Outlook. Scorecards estructurados post-entrevista.

**Justificación:** US-005 se completa con feedback de beta testers. US-008 (RICE: 6.0) es importante para eficiencia pero no bloqueante - tiene menor prioridad RICE. US-009 comienza con versión básica de scorecards.

---

### **Sprint 5 (40 SP): Colaboración y Automatización**

- **US-009:** Evaluación Colaborativa - Fase 2: Colaboración en tiempo real **(5 SP)** - RICE: 3.7
- **US-007:** Comunicaciones Automáticas **(13 SP)** - RICE: 12.3
- **US-011:** Aprobar Oferta (Workflow) **(3 SP)** - RICE: 10.0
- **Deuda técnica y refactoring:** **(10 SP)**
- **Testing & Fixes:** **(9 SP)**

**Total:** 40 SP
**Entregable:** Comentarios y votaciones en tiempo real sobre candidatos. Emails automáticos a candidatos por cambio de etapa. Workflow de aprobación de ofertas.

**Justificación:** US-007 (RICE: 12.3) mejora significativamente experiencia del candidato. US-011 (RICE: 10.0) es un Quick Win (3 SP) que añade control de calidad. US-009 se completa con colaboración en tiempo real (WebSocket).

---

### **Sprint 6 (40 SP): Analytics, Pulido y Producción**

- **US-010:** Dashboard con Métricas - Versión básica **(8 SP)** - RICE: 1.0
- **Testing end-to-end completo:** **(10 SP)**
- **Bug fixing crítico:** **(10 SP)**
- **Optimización de performance:** **(7 SP)**
- **Documentación y preparación producción:** **(5 SP)**

**Total:** 40 SP
**Entregable:** Dashboard básico con métricas clave (time-to-hire, conversion rates, fuentes efectivas). Sistema completo, testeado, optimizado y documentado, listo para producción.

**Justificación:** US-010 tiene el RICE más bajo (1.0) y se implementa al final. Sprint 6 tiene buffer intencional para absorber deuda técnica y retrasos de sprints anteriores. Prioriza estabilidad sobre features nuevas.

---

## Análisis de Resultados

### Párrafo 1: User Stories con Mayor RICE y Balance Reach×Impact vs Effort

El análisis RICE revela que **US-001 (Crear Oferta con IA)** y **US-004 (Pipeline Kanban)** dominan el top del backlog con RICE de 32.0 y 30.0 respectivamente, representando el mejor balance entre valor (Reach × Impact × Confidence) y Effort. US-001 es la puerta de entrada del sistema (Reach: 100, Impact: 2) con esfuerzo contenido (5 SP), mientras que US-004 es la interfaz principal de trabajo diario (Reach: 80, Impact: 3) con complejidad moderada (8 SP). Le siguen las funcionalidades core de IA: **US-003 (Parsing de CVs, RICE: 22.9)** y **US-005 (Ranking con IA, RICE: 18.5)**, que a pesar de su alta complejidad (21 y 13 SP respectivamente) mantienen RICE elevado por su impacto masivo (Impact: 3) y alcance significativo. El factor crítico es que estas funcionalidades con alta complejidad técnica justifican la inversión porque son **diferenciadores killer del producto** - sin IA, LTI ATS sería un ATS genérico más. En contraste, **US-010 (Dashboard)** tiene el RICE más bajo (1.0) debido a su alcance limitado (Reach: 10, uso ocasional) que no compensa el esfuerzo moderado-alto (8 SP).

### Párrafo 2: Comparación con MoSCoW - Diferencias en Priorización

Comparando RICE con la priorización MoSCoW previa, encontramos **diferencias significativas que revelan insights valiosos**. El método MoSCoW clasificó US-007 (Comunicaciones Automáticas), US-008 (Programar Entrevistas) y US-009 (Evaluación Colaborativa) como "Should Have" con prioridad media-alta (posiciones 7-9 en MoSCoW), pero RICE las posiciona en el fondo del backlog (posiciones 7, 9 y 10 respectivamente) con scores bajos (12.3, 6.0 y 3.7). ¿Por qué? **El método RICE penaliza fuertemente el bajo alcance (Reach: 30)** de estas funcionalidades que solo afectan a una fracción de usuarios en etapas avanzadas del funnel. Esto desafía la intuición inicial de que "evaluación colaborativa" es crítica - en realidad, tiene RICE bajo (3.7) porque solo 1 de cada 20 candidatos llega a entrevista. En contraste, **US-006 (Perfil de Candidato)** era #6 en MoSCoW pero sube a #4 en RICE (20.0) debido a su uso diario por múltiples roles (Reach: 80) con esfuerzo contenido (8 SP). La lección clave: **RICE prioriza funcionalidades de alto tráfico y bajo esfuerzo** sobre funcionalidades de nicho aunque tengan alto impacto individual.

### Párrafo 3: Identificación de Quick Wins (RICE alto + Effort bajo)

El análisis RICE identifica **dos Quick Wins genuinos** que deben priorizarse para generar momentum y validación temprana: (1) **US-001 (Crear Oferta con IA)** con RICE de 32.0 y solo 5 SP es el Quick Win definitivo - máximo impacto con esfuerzo contenido, debe ser lo primero en Sprint 1. (2) **US-011 (Aprobar Oferta)** con RICE de 10.0 y apenas 3 SP es un Quick Win secundario que puede implementarse en Sprint 5 cuando el equipo ya tenga momentum y contexto del sistema. Notablemente, **ninguna de las funcionalidades de IA complejas (US-003, US-005) califica como Quick Win** - aunque tienen RICE alto (22.9 y 18.5), su Effort (21 y 13 SP) es demasiado elevado. Estas funcionalidades son **Strategic Bets** que requieren inversión sostenida a lo largo de múltiples sprints. La estrategia óptima es: ejecutar US-001 inmediatamente en Sprint 1 para desbloquear todo el flujo, construir las funcionalidades de IA complejas gradualmente en Sprints 2-4 dividiéndolas en fases iterativas, e intercalar US-011 en Sprint 5 como "paleta limpiadora" entre funcionalidades complejas. Esta combinación de Quick Wins tempranos + Strategic Bets graduales + Quick Wins secundarios maximiza la velocidad de entrega de valor mientras gestiona el riesgo de complejidad técnica.

---

## Resumen Ejecutivo

### Insights Clave del Método RICE

1. **Crear Oferta con IA (US-001)** es indiscutiblemente la prioridad #1 (RICE: 32.0) - combina alcance universal, alto impacto y esfuerzo contenido. Es el Quick Win definitivo.

2. **Pipeline Kanban (US-004)** es casi tan crítico (RICE: 30.0) - es la interfaz principal de trabajo diario con impacto masivo, justificando su complejidad de 8 SP.

3. **Las funcionalidades de IA (US-003, US-005)** mantienen RICE alto (22.9, 18.5) a pesar de su complejidad (21, 13 SP) porque son diferenciadores killer del producto. La inversión está justificada.

4. **Funcionalidades de evaluación colaborativa (US-008, US-009)** tienen RICE sorprendentemente bajo (6.0, 3.7) porque su alcance limitado (Reach: 30) no compensa el alto esfuerzo. Deben implementarse al final o simplificarse.

5. **Dashboard de métricas (US-010)** tiene el RICE más bajo (1.0) y debe ser versión básica en Sprint 6 o moverse a v1.1.

### Estrategia de Implementación

**Sprints 1-3 (120 SP):** Construir el "walking skeleton" del MVP con las 6 funcionalidades de mayor RICE (US-001, US-004, US-003, US-006, US-005, US-002). Al final de Sprint 3, el sistema tiene flujo end-to-end: crear oferta → publicar → recibir CVs → ver en Kanban rankeados por IA → revisar perfiles. **Este es el MVP mínimo para beta testing.**

**Sprints 4-5 (80 SP):** Añadir evaluación estructurada y automatización (US-008, US-009, US-007, US-011). Refinamiento de IA con feedback de usuarios.

**Sprint 6 (40 SP):** Analytics básico (US-010), testing exhaustivo, optimización, y preparación para producción.

**Capacidad total:** 240 SP utilizados de forma óptima con 10-15% de buffer para contingencias en Sprint 6.

### Ventaja Competitiva del Método RICE

El método RICE proporciona **decisiones basadas en datos** que desafían asunciones intuitivas. Por ejemplo, la intuición sugería que "evaluación colaborativa" era crítica, pero RICE revela que es mejor invertir ese esfuerzo en funcionalidades de mayor alcance como comunicaciones automáticas (US-007, RICE: 12.3) que afectan a todos los candidatos. RICE también valida la inversión en funcionalidades complejas de IA (US-003, US-005) demostrando que su alto impacto y alcance justifican el esfuerzo - no deben cortarse por ser "difíciles". Este backlog priorizado con RICE maximiza el ROI de los 240 Story Points disponibles, asegurando que cada sprint entrega valor incremental medible y el MVP final tiene las funcionalidades con mayor impacto por esfuerzo invertido.

---

## Matriz de Decisión: RICE vs MoSCoW

| User Story | RICE Ranking | MoSCoW Category | Diferencia | Explicación |
|------------|--------------|-----------------|------------|-------------|
| US-001 | #1 | Must Have | ✅ Alineado | Ambos métodos coinciden - es fundacional |
| US-004 | #2 | Must Have | ✅ Alineado | Interfaz principal, crítica |
| US-003 | #3 | Must Have | ✅ Alineado | Core de IA, diferenciador |
| US-006 | #4 | Must Have | ⬆️ Sube vs MoSCoW (#6) | RICE valora su uso diario (Reach: 80) |
| US-005 | #5 | Must Have | ✅ Alineado | Diferenciador de IA crítico |
| US-002 | #6 | Must Have | ⬇️ Baja vs MoSCoW (#2) | RICE penaliza su complejidad (13 SP) |
| US-007 | #7 | Should Have | ⬇️ Baja vs MoSCoW (#9) | RICE penaliza bajo alcance relativo |
| US-011 | #8 | Could Have | ⬆️ Sube vs MoSCoW (#11) | Quick Win por bajo esfuerzo (3 SP) |
| US-008 | #9 | Should Have | ⬇️ Baja vs MoSCoW (#7) | RICE penaliza fuerte por Reach limitado (30) |
| US-009 | #10 | Should Have | ⬇️ Baja vs MoSCoW (#8) | Bajo Reach + alto Effort = RICE bajo |
| US-010 | #11 | Could Have | ⬇️ Baja vs MoSCoW (#10) | RICE confirma baja prioridad (Reach: 10) |

**Conclusión:** RICE y MoSCoW coinciden en las 6 funcionalidades "Must Have" core, pero difieren en el ordenamiento de "Should Have" y "Could Have". RICE es más estricto penalizando funcionalidades de bajo alcance (US-008, US-009) y recompensando Quick Wins de bajo esfuerzo (US-011).

---

## Métricas de Éxito del Método RICE

Para validar que la priorización RICE fue correcta, mediremos:

**Post-Sprint 3 (MVP mínimo):**
- ¿Se completó el flujo end-to-end con las 6 US de mayor RICE?
- ¿El scoring de IA rankea correctamente al candidato ideal en top 3 en >70% de casos? (validación de US-005)
- ¿Los beta testers pueden usar el producto sin funcionalidades de bajo RICE (US-008, US-009)?

**Post-Sprint 6 (MVP completo):**
- ¿Se utilizaron los 240 SP disponibles con <10% de desperdicio?
- ¿Las funcionalidades de alto RICE (US-001, US-004, US-003) tienen mayor adopción que las de bajo RICE (US-010)?
- ¿Time-to-hire se redujo 40%+ validando el impacto proyectado?

**Retrospectiva:**
- ¿Fue correcta la decisión de postponer US-008, US-009, US-010 al final?
- ¿Deberían haberse simplificado US-003 o US-005 dado su alto Effort?
- ¿El método RICE entregó mejor ROI que MoSCoW?

---

**Documento elaborado por:** Product Manager LTI ATS
**Método de Priorización:** RICE Score
**Fecha:** Diciembre 2025
**Versión:** 1.0
**Total User Stories:** 11
**Total Story Points:** 132 SP estimados (vs 240 SP disponibles)
**Sprints planificados:** 6 sprints de 40 SP cada uno

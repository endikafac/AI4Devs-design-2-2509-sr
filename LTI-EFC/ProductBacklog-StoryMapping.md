# Product Backlog - LTI ATS MVP
## User Story Mapping

**Proyecto:** LTI ATS - Applicant Tracking System
**Metodo de Priorizacion:** User Story Mapping
**Fecha:** Diciembre 2025
**Timeline:** 3 meses (6 sprints de 2 semanas)
**Equipo:** 5 devs full-stack + 1 ML engineer + 1 QA

---

## Formato 1: Story Map Completo

### Mapa de User Stories por Actividad y Release

| Actividad (Backbone) | MVP (Release 1) - Sprint 1-3 | v1.1 (Release 2) - Sprint 4-5 | v2.0 (Release 3) - Futuro |
|----------------------|------------------------------|-------------------------------|---------------------------|
| **1. Publicar Oferta** | **US-001**: Crear oferta basica con formularios + IA para generacion de descripciones (5 SP) | **US-011**: Workflow de aprobacion de ofertas (draft → pending → approved) (3 SP) | **Futuro**: A/B testing de descripciones, templates por industria, SEO scoring |
| **2. Distribuir Oferta** | **US-002**: Publicar en top 4 job boards (LinkedIn, Indeed, Glassdoor, Monster) con tracking basico (13 SP) | **US-002 mejorado**: Agregar 4 job boards adicionales + multi-idioma + programacion de publicaciones | **Futuro**: Auto-repost inteligente, budget optimization por canal, social media ads |
| **3. Recibir Candidatos** | **US-003**: Parsing basico de CVs - extraccion de nombre, email, telefono, experiencia (13 SP fase 1) | **US-003 completo**: Parsing avanzado con NER de skills, experiencia estructurada, educacion (8 SP fase 2) | **Futuro**: Auto-import desde LinkedIn/GitHub, video CVs con transcripcion, enriquecimiento de perfiles |
| **4. Screening** | **US-004**: Pipeline Kanban drag-and-drop con etapas configurables (8 SP) + **US-006**: Perfil completo de candidato (3 SP) | **US-005**: Scoring predictivo con IA (0-100), ranking automatico, resumen con LLM (13 SP en Sprint 3-4) | **Futuro**: ML predictivo de retencion, bias detection, scoring calibrado por feedback historico |
| **5. Entrevistar** | Manual - Programar entrevistas via email externo | **US-008**: Integracion con Google Calendar/Outlook, auto-scheduling, invitaciones (8 SP) | **Futuro**: Video entrevistas nativas, grabacion y transcripcion con IA, preguntas sugeridas |
| **6. Evaluar/Decidir** | Revision manual en perfil | **US-009**: Scorecards estructurados con competencias, colaboracion en tiempo real (WebSocket), votaciones (13 SP en Sprint 5-6) | **Futuro**: Decision scoring con IA, prediccion de fit cultural, comparacion automatica candidatos |
| **7. Comunicar** | Emails manuales desde cliente | **US-007**: Comunicaciones automaticas por cambio de etapa, templates personalizables, SendGrid (13 SP Sprint 5) | **Futuro**: Comunicacion omnicanal (SMS, WhatsApp), chatbot para FAQs, nurturing automatizado |
| **8. Contratar** | Proceso fuera del sistema | Manual - Reclutador envia oferta por email | **Futuro**: Onboarding workflow, firma electronica de contratos, integracion con HRIS |
| **9. Medir** | No hay metricas | **US-010**: Dashboard basico con time-to-hire, conversion rates, fuentes efectivas (3-5 SP Sprint 6 si hay capacidad) | **Futuro**: Predictive analytics, ROI por fuente, benchmarking vs industria, reportes customizables |

---

## Formato 2: Walking Skeleton del MVP

### Walking Skeleton (Release 1 - Sprint 1-3, 6 semanas)

El MVP minimo viable debe permitir un flujo end-to-end completo para contratar a alguien, aunque sea con procesos manuales en etapas avanzadas:

1. **US-001: Crear Oferta de Empleo con Asistencia de IA** (5 SP - Sprint 1)
   - ✅ **Habilita:** Iniciar el proceso de reclutamiento con ofertas profesionales generadas rapidamente

2. **US-002: Publicar Oferta en Multiples Canales** (13 SP - Sprint 1-2)
   - ✅ **Habilita:** Alcance de candidatos en los 4 job boards principales (85-90% del volumen)

3. **US-003: Recibir y Parsear CVs Automaticamente** (13 SP - Sprint 2-3, fase basica)
   - ✅ **Habilita:** Ingesta automatica de candidatos con informacion estructurada, eliminando transcripcion manual

4. **US-004: Visualizar Pipeline de Candidatos Tipo Kanban** (8 SP - Sprint 2)
   - ✅ **Habilita:** Interfaz principal de trabajo para gestionar candidatos visualmente entre etapas

5. **US-006: Ver Perfil Completo de Candidato** (3 SP - Sprint 3)
   - ✅ **Habilita:** Revision detallada de candidatos para tomar decisiones informadas pre-entrevista

6. **US-005: Filtrar y Rankear Candidatos con IA** (13 SP - Sprint 3-4, fase basica)
   - ✅ **Habilita:** Diferenciador clave - scoring automatico que reduce screening time en 60%

**Total Walking Skeleton:** 55 SP → Sprint 1-3 (6 semanas)

### ¿Por que este Walking Skeleton?

Este conjunto minimo de 6 User Stories forma el "esqueleto caminante" porque permite **completar un proceso de contratacion de principio a fin**, aunque las etapas finales (entrevistas, evaluacion, comunicacion) sean manuales:

1. **Flujo completo funcional:** Un reclutador puede crear oferta → publicarla → recibir CVs automaticamente → verlos en Kanban → rankearlos con IA → revisar perfiles detallados → **decidir a quien entrevistar**

2. **Valor diferencial presente:** El scoring con IA (US-005) esta incluido porque sin el, LTI ATS seria un ATS generico. El MVP debe demostrar el valor unico desde el Sprint 3.

3. **Proceso manual aceptable post-screening:** Las etapas de entrevistas (US-008), evaluacion colaborativa (US-009) y comunicaciones (US-007) pueden hacerse manualmente en el MVP minimo usando herramientas externas (Google Calendar, email, Google Docs). No es ideal, pero **no bloquea contratar a alguien**.

4. **Validacion temprana:** Al final del Sprint 3, este walking skeleton permite hacer beta testing con clientes reales y validar la precision del parsing y scoring de IA - los mayores riesgos tecnicos.

**Estimacion:** 55 Story Points → Sprint 1-3 (6 semanas con equipo de 7 personas)

---

## Formato 3: Backlog Priorizado por Release

### Release 1 - MVP (Sprint 1-3, 6 semanas)

**Objetivo:** Sistema funcional end-to-end con diferenciador de IA para screening automatizado. Permite reclutar desde crear oferta hasta identificar top candidatos, con procesos manuales para etapas finales.

**User Stories incluidas:**

- [ ] **US-001: Crear Oferta de Empleo con Asistencia de IA** (5 SP - Sprint 1)
  - **Justificacion:** Punto de entrada del sistema. Sin ofertas no hay proceso. La asistencia de IA diferencia desde dia 1 sin complejidad excesiva (integracion con LLM madura).

- [ ] **US-002: Publicar Oferta en Multiples Canales** (13 SP - Sprint 1-2)
  - **Justificacion:** Critica para volumen de candidatos. Multiposting aumenta candidaturas 3-5x vs publicacion manual. MVP incluye top 4 job boards (LinkedIn, Indeed, Glassdoor, Monster) que cubren 85-90% del mercado.

- [ ] **US-003: Recibir y Parsear CVs Automaticamente - Fase 1** (13 SP - Sprint 2-3)
  - **Justificacion:** Core del diferenciador de IA. Automatiza la tarea mas tediosa (lectura manual de CVs). Fase 1 hace parsing basico (nombre, contacto, experiencia texto plano) suficiente para MVP. Fase 2 (skills estructurados) se mueve a Release 2.

- [ ] **US-004: Visualizar Pipeline de Candidatos Tipo Kanban** (8 SP - Sprint 2)
  - **Justificacion:** Interfaz principal del producto. Sin tablero visual, el sistema no es usable. Es el "espacio de trabajo" donde ocurre toda la gestion diaria. Tecnologia madura (react-beautiful-dnd), complejidad manejable.

- [ ] **US-006: Ver Perfil Completo de Candidato** (3 SP - Sprint 3)
  - **Justificacion:** Necesaria para revisar candidatos antes de entrevistas. Sin perfil detallado, la informacion esta fragmentada. Bajo esfuerzo (3 SP), alto valor. Enabler para tomar decisiones informadas.

- [ ] **US-005: Filtrar y Rankear Candidatos con IA - Fase 1** (13 SP - Sprint 3-4)
  - **Justificacion:** Killer feature diferenciador. Scoring predictivo (0-100) y ranking automatico es lo que vende el producto. Aunque complejo (13 SP), es indispensable para propuesta de valor unica. Fase 1 implementa scoring basico con embeddings + keyword matching. Refinamiento con feedback se hace en Release 2.

**Total Release 1:** 55 SP | **Timeline:** 6 semanas (Sprint 1-3) | **Entregable:** MVP con flujo end-to-end de screening automatizado con IA

**Funcionalidades excluidas del MVP (Release 1):**

- **US-007 (Comunicaciones Automaticas):** Importante para experiencia del candidato pero no bloquea el proceso. Reclutador puede enviar emails manualmente via Gmail/Outlook en fase MVP. Se automatiza en Release 2.

- **US-008 (Programar Entrevistas):** Ahorra tiempo administrativo pero hay workaround facil (usar Google Calendar directamente). La integracion automatica se añade en Release 2 cuando el flujo core ya este validado.

- **US-009 (Evaluacion Colaborativa):** Mejora la colaboracion del equipo pero los scorecards pueden hacerse en Google Docs/Notion temporalmente. La feature nativa con colaboracion en tiempo real se implementa en Release 2.

- **US-010 (Dashboard):** Valioso para management pero no para operaciones diarias. El MVP puede funcionar sin analytics sofisticado. Se añade version basica en Release 2 Sprint 6.

- **US-011 (Aprobar Oferta):** Añade friccion y es valorado solo en organizaciones enterprise. El MVP target son startups/scale-ups que prefieren velocidad. Se mueve a Release 2 o v2.0 basado en demanda.

---

### Release 2 - v1.1 (Sprint 4-6, +6 semanas)

**Objetivo:** Agregar capacidades de evaluacion colaborativa, automatizacion de comunicaciones, y refinamiento de IA para diferenciacion competitiva completa.

**User Stories incluidas:**

- [ ] **US-003: Parsear CVs - Fase 2 Avanzada** (8 SP - Sprint 4)
  - **Justificacion:** Mejora precision del parsing con NER avanzado para skills, experiencia estructurada por empresa/fechas, educacion. Eleva la precision de 80% a 90%+ incorporando feedback de Release 1.

- [ ] **US-005: Scoring IA - Fase 2 Refinamiento** (5 SP - Sprint 4)
  - **Justificacion:** Refina el modelo de scoring con feedback real de beta testers. Añade explicabilidad ("Por que este candidato es 95% compatible") y ajuste de pesos por competencia.

- [ ] **US-008: Programar Entrevistas con Integracion de Calendario** (8 SP - Sprint 4)
  - **Justificacion:** Elimina "ping-pong" de emails para encontrar horarios. Integracion con Google Calendar y Outlook ahorra 20 min por entrevista. Mejora significativa de eficiencia operativa.

- [ ] **US-009: Evaluacion Colaborativa con Scorecard** (13 SP - Sprint 5-6)
  - **Justificacion:** Core de colaboracion en tiempo real. Scorecards estructurados + comentarios sincronizados (WebSocket) + votaciones mejoran calidad de decisiones. Diferenciador clave vs ATS tradicionales.

- [ ] **US-007: Comunicaciones Automaticas a Candidatos** (13 SP - Sprint 5)
  - **Justificacion:** Mejora drasticamente experiencia del candidato y employer branding. Emails automaticos por cambio de etapa (aplicado, screening, entrevista, rechazo, oferta). Reduce carga administrativa 30 min/dia.

- [ ] **US-010: Dashboard con Metricas - Version Basica** (3-5 SP - Sprint 6 si hay capacidad)
  - **Justificacion:** Metricas clave para management: time-to-hire promedio, conversion rates por etapa, fuentes mas efectivas. Version ultra-simplificada solo si Sprint 6 tiene buffer. Si no, se pospone a v2.0.

**Total Release 2:** 50-52 SP | **Timeline:** +6 semanas (Sprint 4-6) | **Entregable:** Sistema completo con evaluacion colaborativa, automatizacion, y analytics basico

---

### Release 3 - v2.0 (Futuro, post-MVP)

**Objetivo:** Features de diferenciacion avanzada, scale, y expansion de mercado (enterprise)

**Features planificadas (no incluidas en las 11 US actuales):**

**Expansion de capacidades de IA:**
- ML predictivo de retencion de candidatos (scoring de fit a largo plazo)
- Bias detection automatico en descripciones de ofertas y evaluaciones
- Scoring calibrado por feedback historico (learning continuo)
- Auto-sugerencia de preguntas de entrevista basadas en role y skills gap

**Experiencia del candidato:**
- Portal del candidato (area privada para ver status, subir documentos, comunicarse)
- Video entrevistas nativas con grabacion y transcripcion automatica con IA
- Chatbot para FAQs frecuentes de candidatos
- Comunicacion omnicanal (SMS, WhatsApp, no solo email)

**Escalabilidad enterprise:**
- **US-011 mejorado:** Workflows de aprobacion complejos (multi-nivel, condicionales)
- Integracion con HRIS (Workday, BambooHR) para onboarding automatizado
- API abierta para integraciones custom
- SSO (Single Sign-On) con SAML/OAuth para empresas grandes
- Multi-tenancy robusto con aislamiento de datos

**Analytics avanzado:**
- Predictive analytics: tiempo estimado para llenar posicion
- ROI por fuente de candidatos con costo por contratacion
- Benchmarking vs industria (anonimizado)
- Reportes customizables con export a PDF/Excel

**Diferenciadores competitivos:**
- Talent Pool inteligente: base de datos de candidatos pasivos con re-engagement automatizado
- A/B testing de descripciones de ofertas para optimizar conversion
- Auto-repost inteligente en job boards basado en performance
- Social media ads integration (LinkedIn Ads, Facebook Jobs)

**Timeline estimado:** Release 3 comienza en mes 4-5 post-MVP (despues de validacion en produccion con clientes reales)

---

## Formato 4: Justificacion del Mapa

### Parrafo 1: Orden de actividades - ¿Por que este flujo?

El User Story Map sigue el **flujo natural del proceso de reclutamiento** que cualquier reclutador experimentado reconoce inmediatamente: (1) **Publicar Oferta** es la actividad inicial obligatoria - sin una posicion definida no hay proceso. (2) **Distribuir Oferta** amplifica el alcance para generar volumen de candidatos en multiples canales. (3) **Recibir Candidatos** es la entrada de datos al sistema (aplicaciones + CVs). (4) **Screening** es la etapa mas intensiva donde se filtra y rankea candidatos (el core del valor de IA). (5) **Entrevistar** ocurre solo con candidatos pre-seleccionados (1 de cada 20). (6) **Evaluar/Decidir** consolida feedback del equipo para la decision final. (7) **Comunicar** es un proceso transversal que ocurre en todas las etapas. (8) **Contratar** cierra el ciclo con la oferta formal. (9) **Medir** es meta-actividad para optimizacion continua. Este flujo representa **pasos secuenciales y paralelos**: las actividades 1-6 son secuenciales (no puedes entrevistar antes de recibir candidatos), mientras que Comunicar (7) y Medir (9) son paralelas y transversales a todo el journey. La estructura del Story Map permite visualizar dependencias y priorizar por "capas" horizontales (releases) asegurando que cada release entrega valor end-to-end.

### Parrafo 2: Definicion del MVP - ¿Como se definio la "primera fila"?

La **"primera fila" del Story Map (Release 1 - MVP)** se definio con el criterio de **"walking skeleton" - la version mas delgada del producto que permite completar el journey de principio a fin**, aunque sea con procesos manuales en etapas finales. Los criterios especificos fueron: (1) **Incluir al menos 1 US por actividad critica** para tener flujo end-to-end: Publicar (US-001) → Distribuir (US-002) → Recibir (US-003) → Screening (US-004, US-005, US-006). (2) **Maximizar el valor diferencial de IA temprano** incluyendo parsing (US-003) y scoring (US-005) aunque sean complejos, porque sin IA el producto es generico. (3) **Aceptar gaps manuales en actividades de bajo volumen**: Entrevistar (5% de candidatos), Evaluar (3%), y Comunicar pueden hacerse manualmente en MVP porque no bloquean el flujo y hay workarounds faciles (Google Calendar, Gmail, Google Docs). (4) **Excluir features "indifferent" Kano** (US-010, US-011) que no generan satisfaccion en core users. (5) **Limitar scope a 6 semanas (55 SP)** para lanzar rapido y validar. Resultado: El MVP permite screening automatizado completo (el 70% del valor del producto) en 6 semanas, dejando automatizacion de colaboracion y comunicaciones para Release 2 cuando el core ya este validado.

### Parrafo 3: Dependencias criticas - ¿Que debe construirse primero?

Las **dependencias tecnicas criticas** dictaron gran parte del ordenamiento: (1) **US-001 (Crear Oferta) es bloqueante total** - todas las demas US dependen de que existan ofertas activas. Debe ser Sprint 1. (2) **US-002 (Publicar) depende de US-001** - no puedes publicar lo que no existe. Comienza Sprint 1, termina Sprint 2. (3) **US-003 (Parsing) y US-004 (Kanban) dependen de US-002** - necesitan que lleguen candidatos. Se construyen en paralelo Sprint 2-3. (4) **US-005 (Scoring IA) depende de US-003 y US-001** - necesita datos parseados del CV y criterios de la oferta para calcular compatibilidad. Sprint 3-4. (5) **US-006 (Perfil) depende de US-003 y US-004** - muestra datos parseados dentro del Kanban. Sprint 3. (6) **US-008 (Entrevistas) depende de US-006** - se programa desde el perfil del candidato. Sprint 4. (7) **US-009 (Evaluacion) depende de US-006 y US-008** - scorecards post-entrevista. Sprint 5-6. (8) **US-007 (Comunicaciones) depende de US-004** - se dispara con cambios de etapa en pipeline. Sprint 5. (9) **US-010 (Dashboard) depende de todas las anteriores** - agrega datos de todo el proceso. Sprint 6. (10) **US-011 (Aprobaciones) solo depende de US-001** - es ortogonal al flujo principal pero de baja prioridad. Hay una dependencia tecnica adicional critica: **el ML engineer debe trabajar secuencialmente** en US-003 (parsing) y luego US-005 (scoring), no puede paralelizarlos. Esta restriccion de recurso fuerza el orden Sprint 2-3 (parsing) → Sprint 3-4 (scoring).

---

## Formato 5: Comparacion con Metodos Anteriores

### Tabla Comparativa de Priorizacion

| Metodo | US Priorizadas Sprint 1-3 (MVP) | Diferencias con Story Mapping | Ventaja/Desventaja |
|--------|--------------------------------|-------------------------------|-------------------|
| **MoSCoW** | US-001, US-002, US-003, US-004, US-005, US-006 (Must Have - 6 US) | ✅ **Identico al Story Map** - Las 6 US coinciden porque son bloqueantes para flujo end-to-end | **Ventaja MoSCoW:** Simple y rapido, facil de explicar a stakeholders. **Desventaja:** No visualiza el journey, dificil ver gaps en el flujo. |
| **RICE** | US-001, US-004, US-003, US-006, US-005, US-002 (Top 6 por score) | ✅ **Identico al Story Map** pero orden interno diferente. RICE prioriza US-004 (Kanban) antes que US-002 (Publicar) por menor Effort (8 vs 13 SP) | **Ventaja RICE:** Datos cuantitativos (score numerico), facil justificar ROI. **Desventaja:** No considera dependencias tecnicas (US-004 depende de US-002), puede romper el flujo logico. Story Mapping mantiene orden secuencial. |
| **Kano** | US-001, US-004, US-006, US-007 (Quick Wins) + US-002, US-003, US-005 (Big Bets) | ⚠️ **Difiere en US-007 (Comunicaciones)** - Kano lo incluye en Sprint 1-3 como Quick Win (Performance, 5 SP). Story Mapping lo mueve a Release 2 Sprint 5 porque no es bloqueante para walking skeleton. | **Ventaja Kano:** Identifica drivers de satisfaccion (Basic, Performance, Excitement), ayuda priorizar features que "wow". **Desventaja:** No garantiza flujo end-to-end, puede priorizar Quick Wins que no son criticos para MVP minimo. |
| **Story Mapping** | US-001, US-002, US-003, US-004, US-005, US-006 (Walking Skeleton - 6 US) | **Ventaja unica:** Visualiza el journey completo del usuario (reclutador) horizontalmente. Garantiza que el MVP tiene "1 US por actividad critica" = flujo end-to-end funcional. Las releases son "capas" que añaden profundidad sin romper el flujo. | **Ventaja Story Mapping:** Garantiza valor end-to-end por release, facil explicar a usuarios ("asi es como trabajaras con el producto"). Perfecto para productos complejos con journeys largos. **Desventaja:** Requiere mas tiempo de setup (definir actividades del backbone) y puede ser complejo para equipos junior. |

### Insight Clave: Story Mapping vs Otros Metodos

**Story Mapping destaca porque prioriza por "valor de journey completo" en lugar de "valor de feature individual".** Por ejemplo:

- **RICE priorizaria US-004 (Kanban, score 30.0) sobre US-002 (Publicar, score 12.3)** porque Kanban tiene menor Effort. Pero esto romperia el flujo logico: no puedes tener Kanban sin candidatos, y no hay candidatos sin publicacion.

- **Kano incluiria US-007 (Comunicaciones) en MVP** porque es Quick Win Performance (5 SP, valor 7/10). Pero Story Mapping lo mueve a Release 2 porque el walking skeleton no lo necesita - puedes contratar sin emails automaticos usando Gmail manualmente.

- **MoSCoW es el mas alineado con Story Mapping** porque ambos priorizan flujo end-to-end. La diferencia es que MoSCoW es una lista plana (Must/Should/Could) mientras Story Mapping visualiza el journey en 2D (actividades horizontales × releases verticales), haciendo mas facil detectar gaps.

**Conclusion:** Story Mapping es ideal para **productos complejos con journeys multi-etapa** como un ATS, donde el valor esta en completar el proceso de principio a fin, no en features aisladas. Es mas visual y orientado al usuario que MoSCoW, mas consciente del flujo que RICE, y mas estructurado que Kano.

---

## Metricas de Exito del Story Mapping

### Release 1 (Sprint 1-3) - Validacion del Walking Skeleton

**Metricas funcionales:**
- ✅ Un reclutador puede completar el flujo: crear oferta → publicar → recibir CVs → ver en Kanban → rankear con IA → revisar perfil
- ✅ Los CVs se parsean con ≥80% precision en campos criticos (nombre, email, telefono, experiencia)
- ✅ El scoring de IA rankea al candidato ideal en top 3 en ≥70% de casos (validado con 10+ ofertas reales)
- ✅ El Kanban carga en <2 seg con 100 candidatos

**Metricas de negocio:**
- ✅ 3-5 beta testers pueden usar el producto sin training extensivo (≤1 hora onboarding)
- ✅ Time-to-screen (revisar 50 CVs) se reduce de 4 horas a 1 hora (75% mejora vs manual)
- ✅ NPS de beta testers ≥40 (product-market fit inicial)

**Metricas de desarrollo:**
- ✅ Se completo el walking skeleton en 55 SP / 6 semanas (sin retrasos mayores)
- ✅ Deuda tecnica controlada: <10% del tiempo en Sprint 4 se usa para refactoring

---

### Release 2 (Sprint 4-6) - Validacion del Sistema Completo

**Metricas funcionales:**
- ✅ Los reclutadores programan entrevistas en <2 min con sincronizacion automatica de calendarios
- ✅ Los equipos completan scorecards colaborativos en <5 min con comentarios en tiempo real
- ✅ El sistema envia emails automaticos en <1 min tras cambio de etapa (≥95% deliverability)

**Metricas de negocio:**
- ✅ Time-to-hire se reduce 40% vs proceso manual (meta: de 30 dias a 18 dias)
- ✅ Candidatos screeneados por reclutador/dia incrementa 3x (de 10 a 30)
- ✅ NPS ≥50, expansion de beta testers a 10-15 empresas
- ✅ ≥1 cliente beta dispuesto a pagar (validacion de willingness to pay)

**Metricas de desarrollo:**
- ✅ Sistema completo listo para produccion en 12 semanas (timeline cumplido)
- ✅ Uptime ≥99% en ultimas 2 semanas de Sprint 6
- ✅ Todos los datos cumplen GDPR (consentimiento, derecho al olvido, encriptacion)

---

## Riesgos y Mitigaciones por Release

### Riesgos Release 1 (MVP)

| Riesgo | Probabilidad | Impacto | Mitigacion |
|--------|--------------|---------|------------|
| **Precision del parsing de CVs no alcanza 80%** | Alta | Critico | Empezar con modelos pre-entrenados robustos (SpaCy, Transformers). Permitir correccion manual. Iterar con feedback. Target inicial 75%, mejorar a 85% en Release 2. |
| **Scoring de IA percibido como "caja negra"** | Media | Alto | Añadir explicabilidad desde Sprint 3: mostrar "Por que este candidato es 85% compatible" con keywords matched. Permitir ajuste manual de ranking. |
| **Integraciones con job boards fallan** | Media | Alto | Implementar top 2 (LinkedIn, Indeed) primero con circuit breakers. Fallback manual: copiar/pegar oferta si API falla. No bloqueante para flujo core. |
| **ML engineer es cuello de botella** | Alta | Medio | Paralelizar trabajo: devs hacen US-001, US-002, US-004, US-006 mientras ML engineer se enfoca 100% en US-003 y US-005. Plan B: usar parsing rule-based si ML no esta listo. |

---

### Riesgos Release 2 (v1.1)

| Riesgo | Probabilidad | Impacto | Mitigacion |
|--------|--------------|---------|------------|
| **WebSocket (tiempo real) tiene bugs de concurrencia** | Media | Medio | Testing exhaustivo con 10+ usuarios simultaneos. Fallback: polling cada 5 seg si WebSocket falla. No critico - comentarios se sincronizan eventualmente. |
| **APIs de calendario (Google, Outlook) fallan** | Media | Alto | Implementar fallback manual robusto: si integracion falla, mostrar link "Crear evento manualmente" que pre-llena datos. No bloquea scheduling. |
| **Sprint 6 acumula deuda tecnica de sprints anteriores** | Alta | Medio | Sprint 6 tiene buffer intencional (solo 16-19 SP planificados vs 40 SP capacidad). US-010 es opcional. Priorizar estabilidad sobre features nuevas. |

---

## Evolucion del Story Map (Releases Futuras)

### Como Crece el Story Map en v2.0

El Story Map es una **herramienta viva** que evoluciona con el producto:

**Expansion horizontal (nuevas actividades):**
- Añadir columna **"10. Onboarding"** para workflows post-contratacion
- Añadir columna **"11. Talent Pool"** para gestion de candidatos pasivos

**Expansion vertical (profundidad en actividades existentes):**
- **Screening (columna 4)** añade: bias detection, scoring predictivo de retencion, calibracion automatica
- **Entrevistar (columna 5)** añade: video entrevistas nativas, transcripcion con IA, preguntas sugeridas
- **Comunicar (columna 7)** añade: SMS, WhatsApp, chatbot, nurturing automatizado

**Releases adicionales:**
- **Release 3 (v2.0):** Fila completa de "features avanzadas de IA"
- **Release 4 (Enterprise):** Fila completa de "escalabilidad enterprise" (SSO, HRIS, workflows complejos)

**Regla de oro:** Cada release debe seguir siendo "horizontal" (añade valor a multiples actividades del journey) en lugar de "vertical" (profundiza solo 1 actividad). Esto garantiza que cada release mejora la experiencia end-to-end.

---

## Proximos Pasos

### Sprint Planning Sprint 1

1. **Grooming detallado de US-001 (Crear Oferta con IA):**
   - Story splitting: formulario basico (2 SP) + integracion LLM (3 SP)
   - Acceptance criteria con ejemplos: "Dado un titulo 'Senior Software Engineer', cuando hago clic en 'Generar Descripcion', entonces obtengo una descripcion de 200-300 palabras con seccion de responsabilidades, requisitos, y beneficios"
   - Definir prompts de IA y temperatura para generacion

2. **Grooming detallado de US-002 (Publicar Multicanal):**
   - Story splitting por job board: LinkedIn (4 SP), Indeed (3 SP), Glassdoor (3 SP), Monster (3 SP)
   - Investigacion de APIs: documentacion, rate limits, costos, webhooks
   - Diseño de arquitectura: job queue para publicaciones asincronas, retry logic, tracking de fuentes

3. **Setup tecnico:**
   - Repos: decision monorepo vs multi-repo (recomendacion: monorepo con Turborepo/Nx)
   - CI/CD pipeline: GitHub Actions con tests automatizados, deploy a staging en cada PR
   - Entornos: dev local, staging (Vercel/Railway), produccion (AWS/GCP)
   - Setup de integraciones: OpenAI API key, SendGrid account, job board developer accounts

4. **Estimacion con planning poker:**
   - Sesion de 2 horas con todo el equipo para estimar US-001 y US-002 en story points
   - Calibracion: definir que significa 1 SP, 3 SP, 5 SP, 8 SP para el equipo

5. **Kickoff Sprint 1** 🚀
   - Daily standups a las 10am
   - Sprint review viernes semana 2
   - Retro + planning Sprint 2 lunes semana 3

---

## Conclusion

Este backlog priorizado con **User Story Mapping** asegura que:

1. **Flujo end-to-end garantizado:** Cada release entrega valor completo del journey, no features aisladas. El MVP permite screening automatizado de principio a fin.

2. **Visualizacion clara del producto:** El Story Map es la herramienta mas visual de todos los metodos probados (MoSCoW, RICE, Kano). Stakeholders no tecnicos (inversores, board) entienden el flujo inmediatamente.

3. **Diferenciador de IA presente desde Release 1:** US-005 (Scoring IA) esta en el MVP aunque sea complejo, porque sin el, LTI ATS seria un ATS generico. Story Mapping equilibra "walking skeleton minimo" con "valor diferencial unico".

4. **Releases incrementales coherentes:** Release 1 (screening automatizado) → Release 2 (evaluacion colaborativa + automatizacion) → Release 3 (features avanzadas + enterprise). Cada release es vendible por si sola.

5. **Balance pragmatico:** El MVP acepta gaps manuales en actividades de bajo volumen (entrevistas, comunicaciones) para lanzar en 6 semanas, pero asegura que el core de alto volumen (screening) esta completamente automatizado.

La estrategia de Story Mapping es ideal para **productos complejos con journeys largos como un ATS**, donde el valor esta en completar el proceso completo, no en features individuales aisladas. Es mas consciente del flujo del usuario que los otros metodos y facilita la comunicacion con stakeholders.

---

**Documento elaborado por:** Product Manager LTI ATS
**Metodo de Priorizacion:** User Story Mapping
**Fecha:** Diciembre 2025
**Version:** 3.0 (Story Mapping)
**Total User Stories:** 11 en backlog inicial
**Releases planificadas:** 3 (MVP en 6 semanas, v1.1 en +6 semanas, v2.0 futuro)

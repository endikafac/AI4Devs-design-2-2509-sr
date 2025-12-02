# User Stories y Product Backlog - LTI ATS

**Proyecto:** LTI ATS - Applicant Tracking System
**Versión:** 1.0
**Fecha:** Diciembre 2025
**Timeline:** 3 meses (6 sprints de 2 semanas)
**Equipo:** 5 devs full-stack + 1 ML engineer + 1 QA

---

## Índice

1. [PARTE 1: User Stories](#parte-1-user-stories)
2. [PARTE 2: Priorización del Backlog](#parte-2-priorizacion-del-backlog)
   - 2.1 [Método MoSCoW](#21-metodo-moscow)
   - 2.2 [Método RICE Score](#22-metodo-rice-score)
   - 2.3 [Método Kano + Value/Effort](#23-metodo-kano--valueeffort)
   - 2.4 [Método Story Mapping](#24-metodo-story-mapping)
3. [PARTE 3: Análisis Comparativo de Metodologías](#parte-3-analisis-comparativo-de-metodologias)
4. [PARTE 4: Tickets Técnicos (US-001)](#parte-4-tickets-tecnicos-us-001)
5. [PARTE 5: Estimación de Esfuerzo](#parte-5-estimacion-de-esfuerzo)
6. [Conclusiones y Recomendaciones](#conclusiones-y-recomendaciones)

---

# PARTE 1: User Stories

A continuación se presentan las 10 User Stories generadas para el MVP de LTI ATS, siguiendo las mejores prácticas de redacción ágil con formato "Como [rol] quiero [acción] para que [beneficio]" y criterios de aceptación en formato Dado-Cuando-Entonces.

---

## US-001: Crear Oferta de Empleo con Asistencia de IA

**Como** Reclutador o Manager de Contratación
**Quiero** crear una oferta de empleo con asistencia de IA que genere descripciones optimizadas
**Para que** pueda publicar ofertas atractivas y completas en menos tiempo y con mejor calidad

### Descripción Detallada
El sistema debe permitir la creación de ofertas de empleo mediante un formulario intuitivo que capture todos los campos necesarios (título, departamento, ubicación, modalidad, rango salarial, requisitos, responsabilidades, beneficios). La funcionalidad diferenciadora es la integración con un LLM (GPT-4/Claude) que sugiere descripciones optimizadas basadas en el título y los requisitos básicos proporcionados por el usuario.

### Criterios de Aceptación

**CA-1: Creación Manual Completa**
- **Dado que** soy un reclutador autenticado
- **Cuando** accedo al formulario de creación de oferta y completo todos los campos obligatorios (título, departamento, ubicación, tipo de contrato)
- **Entonces** el sistema guarda la oferta en estado "Draft" y me muestra un mensaje de confirmación

**CA-2: Asistencia de IA para Descripción**
- **Dado que** he ingresado el título del puesto y los requisitos básicos
- **Cuando** hago clic en "Generar con IA"
- **Entonces** el sistema envía una solicitud al LLM y muestra una descripción optimizada en el editor WYSIWYG en menos de 5 segundos

**CA-3: Edición de Contenido Generado por IA**
- **Dado que** la IA ha generado una descripción
- **Cuando** edito el contenido en el editor WYSIWYG
- **Entonces** puedo modificar libremente el texto, aplicar formato (negritas, listas, links) y el sistema guarda los cambios automáticamente cada 30 segundos

**CA-4: Validación de Campos Obligatorios**
- **Dado que** intento guardar una oferta
- **Cuando** faltan campos obligatorios (título, departamento, ubicación)
- **Entonces** el sistema muestra errores de validación específicos por campo y previene el guardado

**CA-5: Gestión de Estados**
- **Dado que** tengo una oferta en estado "Draft"
- **Cuando** hago clic en "Enviar para Aprobación" o "Publicar Directamente"
- **Entonces** el sistema cambia el estado a "Pending Approval" o "Active" respectivamente y registra la acción en el audit log

### Prioridad
**Must Have** - Prioridad 1

### Épica
Gestión de Ofertas

### Estimación Inicial
**68 Story Points** (alta complejidad por integración con IA y múltiples componentes)

### Dependencias Técnicas
- Integración con OpenAI/Anthropic API
- Editor WYSIWYG (TipTap o similar)
- Sistema de máquina de estados para ofertas
- Gestión de secrets para API keys

### Riesgos
- **Alto:** Dependencia de API externa (OpenAI/Anthropic) - necesita manejo de rate limits y fallback
- **Medio:** Calidad de las descripciones generadas - puede requerir refinamiento de prompts

### Notas Técnicas
- La descripción generada debe incluir: resumen del rol, responsabilidades clave, requisitos técnicos, soft skills, y beneficios
- Implementar caching de respuestas de IA para prompts similares
- Considerar streaming de la respuesta del LLM para mejor UX

---

## US-002: Publicar Oferta en Múltiples Canales

**Como** Reclutador
**Quiero** publicar una oferta de empleo en múltiples job boards (LinkedIn, Indeed, otros) con un solo clic
**Para que** pueda maximizar el alcance y atraer más candidatos sin esfuerzo manual repetitivo

### Descripción Detallada
El sistema debe integrar con las APIs de múltiples plataformas de empleo (LinkedIn Jobs, Indeed, job boards locales) para permitir la publicación sincronizada de ofertas. Debe manejar el mapeo de campos entre el formato interno y los requeridos por cada plataforma, trackear el estado de publicación, y capturar las candidaturas que lleguen a través de cada canal.

### Criterios de Aceptación

**CA-1: Selección de Canales de Publicación**
- **Dado que** tengo una oferta en estado "Active"
- **Cuando** accedo a la opción "Publicar en Job Boards"
- **Entonces** veo una lista de canales disponibles (LinkedIn, Indeed, sitio web corporativo) con checkboxes para seleccionar

**CA-2: Publicación Exitosa en Múltiples Canales**
- **Dado que** he seleccionado LinkedIn e Indeed
- **Cuando** hago clic en "Publicar"
- **Entonces** el sistema envía la oferta a ambas plataformas, muestra el progreso en tiempo real, y confirma cuando ambas publicaciones están activas con los links externos

**CA-3: Manejo de Errores de Publicación**
- **Dado que** la publicación en LinkedIn falla (API error)
- **Cuando** se completa el intento
- **Entonces** el sistema muestra un error específico para LinkedIn, marca el canal como "Failed", pero continúa con Indeed si tuvo éxito

**CA-4: Tracking de Fuente de Candidatos**
- **Dado que** un candidato aplica desde LinkedIn
- **Cuando** su aplicación llega al sistema vía webhook
- **Entonces** el sistema registra "LinkedIn" como fuente en el perfil del candidato y actualiza las métricas de efectividad por canal

**CA-5: Despublicación Sincronizada**
- **Dado que** una oferta ha sido cubierta y quiero cerrarla
- **Cuando** cambio el estado a "Closed"
- **Entonces** el sistema automáticamente despublica la oferta de todos los canales activos y envía notificaciones a candidatos pendientes

### Prioridad
**Must Have** - Prioridad 2

### Épica
Gestión de Ofertas

### Estimación Inicial
**34 Story Points** (alta complejidad por múltiples integraciones externas)

### Dependencias Técnicas
- Cuentas de empresa en LinkedIn Recruiter e Indeed
- Webhooks para recibir aplicaciones
- Sistema de retry con exponential backoff para APIs externas
- Circuit breaker pattern para resilencia

### Dependencias de User Stories
- **US-001** (debe existir una oferta para publicarla)

### Riesgos
- **Alto:** Las APIs de job boards cambian frecuentemente - necesita mantenimiento continuo
- **Alto:** Limitaciones de rate limiting en APIs gratuitas/básicas
- **Medio:** Mapeo de campos puede perder información (ej: Indeed no soporta todos los campos personalizados)

### Notas Técnicas
- Implementar queue system (RabbitMQ) para procesar publicaciones asíncronamente
- Guardar payload original enviado a cada plataforma para auditoría
- Considerar webhooks de LinkedIn/Indeed para actualizaciones de estado

---

## US-003: Recibir y Parsear CVs Automáticamente

**Como** Sistema de IA
**Quiero** recibir CVs en múltiples formatos (PDF, DOCX, imagen) y extraer automáticamente la información estructurada
**Para que** los reclutadores no tengan que transcribir manualmente los datos de los candidatos

### Descripción Detallada
Esta es una funcionalidad core de IA que automatiza la extracción de información de CVs. Debe soportar múltiples formatos de archivo, realizar OCR si es necesario, utilizar modelos de NLP (NER) para extraer entidades (nombre, email, teléfono, experiencia laboral, educación, skills), y estructurar la información en el formato de base de datos del sistema. Es crítico para la propuesta de valor de automatización del ATS.

### Criterios de Aceptación

**CA-1: Recepción de CV en Formato PDF**
- **Dado que** un candidato aplica a una oferta adjuntando un CV en PDF
- **Cuando** el webhook recibe la aplicación
- **Entonces** el sistema descarga el archivo, lo almacena en S3, y dispara el job de parsing asíncrono

**CA-2: Extracción de Datos de Contacto**
- **Dado que** el CV está en proceso de parsing
- **Cuando** el pipeline de NLP ejecuta la extracción
- **Entonces** el sistema identifica y extrae correctamente nombre completo, email, teléfono, y ubicación con >90% de precisión

**CA-3: Extracción de Experiencia Laboral**
- **Dado que** el CV contiene sección de experiencia laboral
- **Cuando** el modelo de NER procesa el documento
- **Entonces** el sistema extrae para cada trabajo: empresa, título del puesto, fechas (inicio-fin), y descripción de responsabilidades como lista estructurada

**CA-4: Extracción de Educación y Skills**
- **Dado que** el CV incluye sección de educación y habilidades
- **Cuando** se completa el parsing
- **Entonces** el sistema extrae título académico, institución, año de graduación, y una lista de skills técnicos y soft skills identificados

**CA-5: Manejo de CVs con OCR (imágenes o PDFs escaneados)**
- **Dado que** el CV es una imagen JPG o PDF escaneado
- **Cuando** se detecta que el PDF no tiene texto seleccionable
- **Entonces** el sistema ejecuta OCR (Tesseract/AWS Textract), extrae el texto, y luego aplica el parsing con una advertencia de "Precisión reducida - requiere revisión manual"

**CA-6: Almacenamiento de Datos Parseados**
- **Dado que** el parsing se completó exitosamente
- **Cuando** se guarda el perfil del candidato
- **Entonces** toda la información estructurada se guarda en la BD (tabla candidates con JSONB para campos flexibles) y el candidato aparece en el pipeline

### Prioridad
**Must Have** - Prioridad 3

### Épica
Screening con IA

### Estimación Inicial
**55 Story Points** (muy alta complejidad técnica de ML/NLP)

### Dependencias Técnicas
- Modelo de NER (SpaCy, Hugging Face, o modelo custom fine-tuned)
- Apache Tika o PyPDF2 para extracción de texto
- AWS Textract o Tesseract para OCR
- S3 para almacenamiento de archivos
- RabbitMQ para processing asíncrono

### Dependencias de User Stories
- **US-002** (los CVs llegan tras publicar ofertas)

### Riesgos
- **Muy Alto:** La precisión del parsing determina la usabilidad del sistema - CVs mal parseados generan frustración
- **Alto:** Variabilidad de formatos de CV es extrema - necesita entrenamiento continuo
- **Medio:** Performance con archivos grandes (>5MB) puede ser lento

### Notas Técnicas
- Implementar fallback a revisión manual si el confidence score es <80%
- Guardar el texto raw extraído para debugging y mejora de modelos
- Considerar fine-tuning de modelos con CVs reales (con consentimiento) para mejorar precisión
- Implementar feedback loop: permitir a reclutadores corregir datos parseados incorrectamente y usar eso para retraining

### Métricas de Éxito
- Precisión de extracción de campos críticos (nombre, email, teléfono) >95%
- Precisión de extracción de experiencia laboral >85%
- Precisión de extracción de skills >75%
- Tiempo de processing <10 segundos para PDF estándar de 2 páginas

---

## US-004: Visualizar Pipeline de Candidatos Tipo Kanban

**Como** Reclutador o Manager de Contratación
**Quiero** ver todos los candidatos de una oferta en un tablero Kanban visual con columnas por etapa del proceso
**Para que** pueda entender el estado del pipeline de un vistazo y mover candidatos entre etapas fácilmente

### Descripción Detallada
Interfaz principal del ATS que muestra candidatos organizados en columnas (etapas): "Nuevo", "Screening", "Entrevista Telefónica", "Entrevista Técnica", "Entrevista Final", "Oferta", "Contratado", "Rechazado". Debe soportar drag-and-drop para mover candidatos entre etapas, filtros avanzados, búsqueda, y actualizaciones en tiempo real cuando múltiples usuarios trabajan simultáneamente.

### Criterios de Aceptación

**CA-1: Visualización del Tablero Kanban**
- **Dado que** accedo a una oferta de empleo activa
- **Cuando** entro a la vista de pipeline
- **Entonces** veo un tablero con 8 columnas (etapas del proceso) mostrando tarjetas de candidatos con foto, nombre, score de IA, y tiempo en etapa

**CA-2: Drag and Drop de Candidatos**
- **Dado que** tengo candidatos en la columna "Screening"
- **Cuando** arrastro una tarjeta a la columna "Entrevista Telefónica"
- **Entonces** el candidato se mueve a la nueva etapa, el sistema guarda el cambio inmediatamente, actualiza el timestamp, y dispara notificaciones automáticas al candidato

**CA-3: Filtros y Búsqueda**
- **Dado que** el pipeline tiene 100+ candidatos
- **Cuando** aplico filtros (por score de IA, fuente, fecha de aplicación, tags)
- **Entonces** el tablero muestra solo candidatos que cumplen los criterios y actualiza el contador de resultados

**CA-4: Ordenamiento dentro de Columnas**
- **Dado que** estoy en la columna "Screening"
- **Cuando** selecciono "Ordenar por Score de IA (Mayor a Menor)"
- **Entonces** las tarjetas se reorganizan mostrando primero los candidatos con mayor score de compatibilidad

**CA-5: Acciones Rápidas desde Tarjeta**
- **Dado que** hago hover sobre una tarjeta de candidato
- **Cuando** hago clic en el menú de acciones rápidas
- **Entonces** veo opciones: "Ver Perfil", "Enviar Email", "Programar Entrevista", "Agregar Nota", "Rechazar" y puedo ejecutarlas sin salir del Kanban

**CA-6: Actualización en Tiempo Real (Colaboración)**
- **Dado que** otro reclutador mueve un candidato en el mismo pipeline
- **Cuando** estoy viendo el tablero
- **Entonces** veo la actualización en tiempo real (vía WebSocket) sin necesidad de recargar la página, con indicador de quién hizo el cambio

### Prioridad
**Must Have** - Prioridad 4

### Épica
Pipeline y Tracking

### Estimación Inicial
**21 Story Points** (complejidad moderada, tecnología madura)

### Dependencias Técnicas
- react-beautiful-dnd o @dnd-kit para drag and drop
- WebSocket (Socket.io) para actualizaciones en tiempo real
- Virtualización de listas para performance (react-window) si hay muchos candidatos
- Optimistic UI updates para UX responsiva

### Dependencias de User Stories
- **US-003** (necesita candidatos parseados para mostrar)

### Riesgos
- **Medio:** Performance con pipelines grandes (>200 candidatos) - necesita paginación o virtualización
- **Bajo:** Conflictos de concurrencia si dos usuarios mueven el mismo candidato simultáneamente - resolver con last-write-wins y notificaciones

### Notas Técnicas
- Implementar lazy loading de tarjetas (cargar solo las visibles en viewport)
- Cachear datos del pipeline en Redux/Context para evitar re-fetches constantes
- Considerar vista alternativa de lista (tabla) para usuarios que prefieren ese formato

---

## US-005: Filtrar y Rankear Candidatos con IA

**Como** Reclutador
**Quiero** que el sistema rankee automáticamente los candidatos por compatibilidad con la oferta usando IA
**Para que** pueda enfocarme primero en los mejores candidatos y reducir el tiempo de screening en 60%

### Descripción Detallada
Funcionalidad core de IA que calcula un score de compatibilidad (0-100) entre el perfil del candidato y los requisitos de la oferta. Utiliza embeddings semánticos, comparación de skills, análisis de experiencia relevante, y un LLM para generar un resumen explicativo del match. Debe ser explicable (mostrar por qué un candidato tiene un score alto/bajo) para generar confianza en los reclutadores.

### Criterios de Aceptación

**CA-1: Cálculo Automático de Score al Recibir Candidato**
- **Dado que** un nuevo candidato fue parseado exitosamente
- **Cuando** se completa la extracción de datos
- **Entonces** el sistema calcula automáticamente el score de compatibilidad (0-100) en menos de 5 segundos y lo muestra en la tarjeta del candidato

**CA-2: Desglose de Score con Explicabilidad**
- **Dado que** un candidato tiene un score de 87/100
- **Cuando** hago clic en "Ver Detalles del Score"
- **Entonces** veo un desglose: "Skills Match: 90%, Experiencia Relevante: 85%, Educación: 80%, Ubicación: 95%" y un resumen generado por LLM explicando los puntos fuertes y débiles

**CA-3: Ranking Automático en el Pipeline**
- **Dado que** hay 50 candidatos en la etapa "Screening"
- **Cuando** accedo al pipeline
- **Entonces** por defecto los candidatos están ordenados por score descendente (mejores candidatos arriba) con indicador visual de color (verde >80, amarillo 60-80, rojo <60)

**CA-4: Filtro por Score de IA**
- **Dado que** quiero revisar solo candidatos de alto potencial
- **Cuando** aplico filtro "Score >75"
- **Entonces** el pipeline muestra solo candidatos que cumplen el criterio y puedo exportar esta lista filtrada

**CA-5: Resumen Generado por LLM**
- **Dado que** el candidato tiene un score calculado
- **Cuando** accedo a su perfil
- **Entonces** veo un resumen ejecutivo generado por GPT-4/Claude (3-4 frases) destacando: "¿Por qué es un buen match?", "Fortalezas clave", "Posibles gaps a evaluar en entrevista"

**CA-6: Re-cálculo Manual de Score**
- **Dado que** he actualizado los requisitos de la oferta
- **Cuando** hago clic en "Re-calcular Scores para Todos los Candidatos"
- **Entonces** el sistema encola el re-cálculo asíncrono y me notifica cuando termina (puede tomar minutos si hay muchos candidatos)

### Prioridad
**Must Have** - Prioridad 5

### Épica
Screening con IA

### Estimación Inicial
**55 Story Points** (muy alta complejidad de ML)

### Dependencias Técnicas
- Sentence Transformers o OpenAI Embeddings para similarity matching
- Modelo de scoring (puede ser rule-based + ML hybrid)
- LLM (GPT-4/Claude) para generación de resúmenes explicativos
- Vector database (Pinecone, Weaviate) opcional para búsqueda semántica avanzada

### Dependencias de User Stories
- **US-003** (necesita datos parseados)
- **US-001** (necesita criterios de la oferta para comparar)

### Riesgos
- **Muy Alto:** La precisión del scoring determina la confianza de los usuarios - si rankea mal, perderán confianza en la IA
- **Alto:** Bias algorítmico - el modelo puede perpetuar sesgos históricos de contratación
- **Alto:** Explicabilidad - los reclutadores necesitan entender *por qué* un candidato tiene un score para confiar en la herramienta

### Notas Técnicas
- **Enfoque Híbrido Recomendado:**
  1. Rule-based scoring para criterios objetivos (años de experiencia, skills exactos, educación requerida)
  2. Embedding similarity para match semántico de descripción del rol vs experiencia del candidato
  3. LLM para generación de resumen cualitativo
- Implementar feedback loop: permitir a reclutadores indicar "este candidato debería tener mayor/menor score" y usar para ajustar el modelo
- Considerar A/B testing de diferentes modelos de scoring
- Auditoría de bias: analizar regularmente si el scoring tiene correlación con características protegidas (género, edad, etnia)

### Métricas de Éxito
- Los candidatos contratados tienen score promedio >75 en el 80% de casos
- Reclutadores reportan que el top 10 de candidatos por score es relevante en >70% de ofertas
- Reducción del 60% en tiempo de screening medido en horas/candidato

---

## US-006: Ver Perfil Completo de Candidato

**Como** Reclutador, Manager de Contratación, o Entrevistador
**Quiero** ver toda la información de un candidato consolidada en un solo lugar (CV, datos parseados, timeline de interacciones, evaluaciones)
**Para que** pueda tomar decisiones informadas sin tener que buscar información en múltiples lugares

### Descripción Detallada
Pantalla de detalle del candidato que actúa como "source of truth" consolidando toda la información relevante: datos personales, CV original, datos parseados (experiencia, educación, skills), score de IA con explicación, timeline de todas las interacciones (emails enviados, entrevistas programadas, notas agregadas), evaluaciones de entrevistadores, y documentos adjuntos. Debe ser navegable con tabs y permitir acciones rápidas (enviar email, programar entrevista, cambiar etapa).

### Criterios de Aceptación

**CA-1: Vista de Información Básica**
- **Dado que** hago clic en un candidato desde el pipeline
- **Cuando** se abre el perfil
- **Entonces** veo en la sección principal: foto/avatar, nombre, email, teléfono, ubicación, links (LinkedIn, portfolio), y el score de IA destacado con código de color

**CA-2: Tab de Experiencia y Educación**
- **Dado que** estoy en el perfil del candidato
- **Cuando** navego al tab "Experiencia"
- **Entonces** veo una lista cronológica de trabajos previos (empresa, título, fechas, responsabilidades) parseados del CV, con iconos de empresas si están disponibles

**CA-3: Tab de CV Original**
- **Dado que** necesito revisar el CV completo
- **Cuando** navego al tab "CV Original"
- **Entonces** veo el PDF/DOCX renderizado en el navegador (embedded) con opción de descargar

**CA-4: Timeline de Interacciones**
- **Dado que** quiero ver el historial completo
- **Cuando** navego al tab "Timeline"
- **Entonces** veo una lista cronológica de todas las interacciones: "Aplicó el 15/11", "Movido a Screening el 16/11 por Juan", "Email enviado el 17/11", "Entrevista programada para 20/11", con timestamps y responsables

**CA-5: Tab de Evaluaciones**
- **Dado que** el candidato ha sido entrevistado
- **Cuando** navego al tab "Evaluaciones"
- **Entonces** veo todos los scorecards completados por entrevistadores con puntuaciones por competencia, comentarios, y recomendación (Hire/No Hire/Maybe)

**CA-6: Acciones Rápidas desde Perfil**
- **Dado que** estoy revisando el perfil
- **Cuando** hago clic en los botones de acción en la barra superior
- **Entonces** puedo "Programar Entrevista", "Enviar Email", "Cambiar Etapa", "Agregar Nota", "Rechazar", o "Generar Oferta" sin salir de la vista

### Prioridad
**Must Have** - Prioridad 6

### Épica
Pipeline y Tracking

### Estimación Inicial
**21 Story Points** (complejidad moderada, principalmente UI)

### Dependencias Técnicas
- PDF.js o similar para rendering de CVs
- Componente de timeline (librería o custom)
- Sistema de tabs (React Tabs o Headless UI)
- Lazy loading de tabs para performance

### Dependencias de User Stories
- **US-003** (necesita datos parseados)
- **US-004** (se accede desde el pipeline)

### Riesgos
- **Medio:** Performance con candidatos que tienen muchas interacciones (>100 eventos en timeline)
- **Bajo:** Rendering de PDFs grandes (>10MB) puede ser lento

### Notas Técnicas
- Implementar caching de datos del perfil para evitar fetches repetidos
- Considerar pre-loading del perfil del siguiente candidato en el pipeline para navegación fluida
- El timeline debe ser extensible para agregar nuevos tipos de eventos en el futuro

---

## US-007: Enviar Comunicaciones Automáticas a Candidatos

**Como** Reclutador
**Quiero** que el sistema envíe automáticamente emails a candidatos cuando cambian de etapa en el proceso
**Para que** mantenga a los candidatos informados sin esfuerzo manual y mejore la experiencia del candidato

### Descripción Detallada
Sistema de comunicación automatizada que se dispara cuando un candidato cambia de etapa en el pipeline. Utiliza templates de email personalizables con variables dinámicas (nombre del candidato, nombre de la oferta, empresa, etc.). Debe permitir configurar qué transiciones de etapa disparan emails, qué template usar, y permitir a los reclutadores revisar/editar el email antes de enviarlo si lo desean.

### Criterios de Aceptación

**CA-1: Configuración de Templates de Email**
- **Dado que** soy administrador del sistema
- **Cuando** accedo a "Configuración > Templates de Email"
- **Entonces** veo templates pre-configurados para cada etapa ("Confirmación de Aplicación", "Pasó a Screening", "Entrevista Programada", "Rechazo", "Oferta Extendida") y puedo editarlos con un editor WYSIWYG

**CA-2: Disparo Automático al Cambiar Etapa**
- **Dado que** tengo configurado un trigger automático para "Pasó a Entrevista Telefónica"
- **Cuando** muevo un candidato a esa etapa en el Kanban
- **Entonces** el sistema automáticamente envía el email correspondiente al candidato usando el template configurado, reemplazando variables {nombre_candidato}, {puesto}, etc.

**CA-3: Preview Antes de Enviar (Modo Manual)**
- **Dado que** prefiero revisar emails antes de enviarlos
- **Cuando** cambio un candidato de etapa con la configuración "Requiere Aprobación Manual"
- **Entonces** se abre un modal mostrando el email pre-generado con el template y puedo editarlo antes de hacer clic en "Enviar"

**CA-4: Historial de Emails Enviados**
- **Dado que** quiero verificar qué comunicación se envió a un candidato
- **Cuando** reviso el timeline en su perfil
- **Entonces** veo todos los emails enviados con fecha, asunto, y opción de ver el contenido completo

**CA-5: Manejo de Errores de Envío**
- **Dado que** un email falla al enviarse (email inválido, servicio caído)
- **Cuando** se intenta el envío
- **Entonces** el sistema marca el email como "Failed" en el timeline, me notifica del error, y ofrece opción de "Reintentar" o "Editar Email y Reenviar"

### Prioridad
**Should Have** - Prioridad 9

### Épica
Pipeline y Tracking

### Estimación Inicial
**21 Story Points** (complejidad moderada)

### Dependencias Técnicas
- Servicio de email transaccional (SendGrid, AWS SES, Mailgun)
- Sistema de templates (Handlebars, Mustache, o similar)
- Queue para procesar envíos asíncronamente
- Configuración SPF/DKIM para deliverability

### Dependencias de User Stories
- **US-004** (se dispara con cambios de etapa en el pipeline)

### Riesgos
- **Medio:** Emails marcados como spam - necesita configuración correcta de dominio y warming
- **Bajo:** Bounce rate alto si los emails de candidatos son inválidos

### Notas Técnicas
- Implementar rate limiting para evitar ser bloqueados por proveedores de email
- Guardar contenido exacto del email enviado para auditoría y compliance (GDPR)
- Considerar soporte para multiple idiomas en templates (español, inglés)
- Permitir deshabilitación global de ciertos tipos de emails para testing

---

## US-008: Programar Entrevistas con Integración de Calendario

**Como** Reclutador o Manager de Contratación
**Quiero** programar entrevistas sincronizadas con mi calendario (Google Calendar, Outlook) y enviar invitaciones automáticas
**Para que** evite el intercambio manual de emails para encontrar horarios y reduzca el tiempo de coordinación

### Descripción Detallada
Integración con Google Calendar API y Microsoft Graph API (Outlook) que permite ver la disponibilidad de los entrevistadores, seleccionar un horario, y crear automáticamente eventos de calendario con invitaciones al candidato y entrevistadores. Debe manejar zonas horarias, conflictos, y permitir reprogramar o cancelar entrevistas con notificaciones automáticas.

### Criterios de Aceptación

**CA-1: Conexión de Calendario Personal**
- **Dado que** soy un usuario del sistema
- **Cuando** voy a "Mi Perfil > Conectar Calendario"
- **Entonces** puedo autenticar mi cuenta de Google o Microsoft, el sistema obtiene permisos de lectura/escritura, y muestra "Calendario Conectado Exitosamente"

**CA-2: Ver Disponibilidad de Entrevistadores**
- **Dado que** quiero programar una entrevista técnica
- **Cuando** selecciono entrevistadores del equipo
- **Entonces** veo un calendario visual con franjas horarias disponibles (verdes) y ocupadas (rojas) considerando los calendarios de todos los seleccionados

**CA-3: Crear Entrevista con Invitaciones Automáticas**
- **Dado que** he seleccionado fecha, hora, y entrevistadores
- **Cuando** hago clic en "Programar Entrevista"
- **Entonces** el sistema crea eventos de calendario para todos los participantes, envía invitaciones por email con link de videoconferencia (Google Meet/Zoom), y guarda la entrevista en el sistema

**CA-4: Manejo de Zonas Horarias**
- **Dado que** el candidato está en zona horaria diferente a la mía
- **Cuando** programo la entrevista
- **Entonces** el sistema muestra la hora en ambas zonas horarias y el candidato recibe la invitación con la hora correcta en su zona horaria

**CA-5: Reprogramación de Entrevistas**
- **Dado que** necesito cambiar la fecha de una entrevista programada
- **Cuando** edito la entrevista y selecciono nuevo horario
- **Entonces** el sistema actualiza los eventos de calendario de todos los participantes, envía notificaciones de cambio, y registra el cambio en el timeline del candidato

**CA-6: Notificación de Conflictos**
- **Dado que** intento programar una entrevista en un horario donde un entrevistador tiene otro evento
- **Cuando** selecciono ese horario
- **Entonces** el sistema muestra una advertencia "Conflicto: Juan tiene reunión de 10:00-11:00" y sugiere horarios alternativos

### Prioridad
**Should Have** - Prioridad 7

### Épica
Evaluación Colaborativa

### Estimación Inicial
**34 Story Points** (alta complejidad de integraciones)

### Dependencias Técnicas
- Google Calendar API
- Microsoft Graph API (Outlook)
- Manejo de OAuth 2.0 para autenticación
- Librería de manejo de zonas horarias (moment-timezone o date-fns-tz)
- Integración con plataformas de videoconferencia (Google Meet, Zoom)

### Dependencias de User Stories
- **US-006** (se programa desde el perfil del candidato)

### Riesgos
- **Alto:** Las APIs de calendario son complejas y propensas a fallos - necesita manejo robusto de errores
- **Medio:** Refresh tokens expiran - necesita re-autenticación periódica
- **Medio:** Conflictos de concurrencia si múltiples personas programan al mismo entrevistador simultáneamente

### Notas Técnicas
- Implementar webhook listeners para actualizaciones de calendario (si el entrevistador cancela desde su calendario, el sistema debe reflejarlo)
- Considerar límites de rate limiting de APIs (Google Calendar: 1M queries/día por proyecto)
- Guardar link de videoconferencia generado en la entrevista
- Permitir fallback manual: si la integración falla, permitir crear entrevista manualmente con campo de texto libre para link

---

## US-009: Completar Evaluación Colaborativa con Scorecard

**Como** Entrevistador
**Quiero** completar un scorecard estructurado después de entrevistar a un candidato con puntuaciones por competencia y comentarios
**Para que** el equipo tenga evaluaciones consistentes y pueda tomar decisiones de contratación basadas en datos

### Descripción Detallada
Sistema de evaluación estructurada donde cada entrevistador completa un scorecard post-entrevista con competencias predefinidas (técnicas, culturales, comunicación, etc.), puntuación por competencia (escala 1-5), comentarios cualitativos, y recomendación final (Strong Hire, Hire, Maybe, No Hire, Strong No Hire). Debe soportar comentarios colaborativos en tiempo real donde el equipo puede discutir antes de tomar la decisión final.

### Criterios de Aceptación

**CA-1: Configuración de Scorecard Template**
- **Dado que** soy el creador de la oferta
- **Cuando** configuro el proceso de entrevistas
- **Entonces** puedo definir qué competencias evaluar (ej: "Conocimiento de React", "Problem Solving", "Comunicación"), el peso de cada una (%), y qué entrevistadores evalúan qué competencias

**CA-2: Completar Scorecard Post-Entrevista**
- **Dado que** he entrevistado a un candidato y tengo una tarea pendiente "Completar Evaluación"
- **Cuando** accedo al scorecard
- **Entonces** veo el formulario con todas las competencias asignadas, puedo puntuar cada una (1-5 con radio buttons o slider), agregar comentarios por competencia, y seleccionar recomendación final

**CA-3: Visibilidad de Evaluaciones de Otros**
- **Dado que** múltiples entrevistadores evalúan al mismo candidato
- **Cuando** completo mi scorecard
- **Entonces** puedo ver las puntuaciones y comentarios de otros entrevistadores (si la configuración permite visibilidad post-evaluación), con timestamp de cuándo evaluaron

**CA-4: Agregación de Scores**
- **Dado que** todos los entrevistadores completaron sus scorecards
- **Cuando** accedo al perfil del candidato
- **Entonces** veo un score agregado ponderado por competencia y por entrevistador, con un indicador visual (semáforo) y el consenso del equipo

**CA-5: Comentarios Colaborativos en Tiempo Real**
- **Dado que** estamos en la fase de decisión final
- **Cuando** un entrevistador agrega un comentario en la sección "Discusión del Equipo"
- **Entonces** todos los usuarios viendo el perfil del candidato ven el comentario aparecer en tiempo real (WebSocket) con notificación

**CA-6: Votación Final**
- **Dado que** el equipo ha discutido y está listo para decidir
- **Cuando** el hiring manager inicia una votación "¿Avanzamos a Oferta?"
- **Entonces** todos los participantes reciben notificación, pueden votar (Yes/No/Abstain), y los resultados se muestran en tiempo real con la decisión tomada cuando todos votan

### Prioridad
**Should Have** - Prioridad 8

### Épica
Evaluación Colaborativa

### Estimación Inicial
**34 Story Points** (alta complejidad de colaboración en tiempo real)

### Dependencias Técnicas
- WebSocket (Socket.io) para comentarios en tiempo real
- Sistema de notificaciones en la app
- JSONB en PostgreSQL para almacenar scorecards flexibles
- Cálculo de agregación ponderada

### Dependencias de User Stories
- **US-006** (se completa desde el perfil)
- **US-008** (post-entrevista programada)

### Riesgos
- **Medio:** Complejidad de sincronización en tiempo real - necesita testing exhaustivo con múltiples usuarios
- **Medio:** Si un entrevistador no completa su scorecard, bloquea la decisión - necesita recordatorios y escalamiento

### Notas Técnicas
- Implementar "typing indicators" para mostrar cuando alguien está escribiendo un comentario
- Considerar modo "evaluación ciega" donde entrevistadores no ven las puntuaciones de otros hasta completar la propia (evita bias de anclaje)
- Guardar historial completo de ediciones de scorecards para auditoría
- Permitir templates de scorecard por tipo de rol (Frontend Dev, Backend Dev, Product Manager, etc.)

### Métricas de Éxito
- 100% de entrevistas tienen scorecard completado dentro de 24 horas post-entrevista
- El tiempo de decisión final se reduce de 3-5 días a <1 día
- Los hiring managers reportan mayor confianza en decisiones de contratación basadas en scorecards estructurados

---

## US-010: Visualizar Dashboard con Métricas de Reclutamiento

**Como** Manager de Contratación o Admin
**Quiero** ver un dashboard con métricas clave de reclutamiento (time-to-hire, fuentes efectivas, conversion rates)
**Para que** pueda identificar cuellos de botella, optimizar el proceso, y justificar inversión en el ATS

### Descripción Detallada
Dashboard de analytics que muestra métricas agregadas y visualizaciones: time-to-hire promedio, número de candidatos por etapa del funnel, fuentes de candidatos más efectivas, conversion rates entre etapas, ofertas activas vs cerradas, y comparación de métricas entre departamentos o periodos de tiempo. Debe tener filtros por rango de fechas, departamento, reclutador, y permitir exportar reportes.

### Criterios de Aceptación

**CA-1: Visualización de Métricas Principales**
- **Dado que** accedo al dashboard de analytics
- **Cuando** cargo la página
- **Entonces** veo cards con métricas clave destacadas: "Time-to-Hire Promedio: 22 días", "Candidatos Activos: 156", "Ofertas Abiertas: 12", "Tasa de Éxito: 18%", con comparación vs periodo anterior ("+5% vs mes pasado")

**CA-2: Gráfico de Funnel de Conversión**
- **Dado que** quiero analizar dónde se pierden candidatos
- **Cuando** veo la sección "Funnel de Conversión"
- **Entonces** veo un gráfico de embudo mostrando: "Aplicaron: 500 → Screening: 200 → Entrevista: 80 → Oferta: 20 → Contratado: 15" con porcentajes de conversión entre etapas

**CA-3: Análisis de Fuentes de Candidatos**
- **Dado que** quiero saber qué job boards son más efectivos
- **Cuando** veo la sección "Fuentes de Candidatos"
- **Entonces** veo un gráfico de barras o pie chart: "LinkedIn: 45%, Indeed: 30%, Referidos: 15%, Sitio Web: 10%" y cuál tiene mejor quality score y conversion rate a contratación

**CA-4: Time-to-Hire por Departamento**
- **Dado que** quiero comparar eficiencia entre departamentos
- **Cuando** veo la sección "Time-to-Hire por Departamento"
- **Entonces** veo un gráfico de barras comparando: "Engineering: 25 días, Sales: 18 días, Marketing: 30 días" con benchmarks de la industria

**CA-5: Filtros y Rangos de Fecha**
- **Dado que** quiero analizar un periodo específico
- **Cuando** aplico filtros "Últimos 3 meses" + "Departamento: Engineering"
- **Entonces** todas las métricas y gráficos se actualizan para reflejar solo datos de ese periodo y departamento

**CA-6: Exportar Reportes**
- **Dado que** necesito compartir métricas con liderazgo
- **Cuando** hago clic en "Exportar Reporte"
- **Entonces** puedo descargar un PDF o Excel con todas las métricas y gráficos del periodo seleccionado

### Prioridad
**Could Have** - Prioridad 10

### Épica
Reporting y Analytics

### Estimación Inicial
**21 Story Points** (complejidad moderada)

### Dependencias Técnicas
- Librería de gráficos (Chart.js, Recharts, D3.js)
- Queries de agregación optimizadas en PostgreSQL
- Caching de métricas agregadas (Redis) para performance
- Librería de exportación a PDF (jsPDF, Puppeteer)

### Dependencias de User Stories
- Todas las anteriores (necesita datos de todo el proceso)

### Riesgos
- **Medio:** Performance con grandes volúmenes de datos históricos (>10,000 candidatos) - necesita índices y agregaciones eficientes
- **Bajo:** Métricas calculadas incorrectamente pueden llevar a decisiones erróneas - necesita testing exhaustivo de cálculos

### Notas Técnicas
- Implementar materializedviews o tablas de agregación pre-calculadas para métricas complejas
- Considerar refrescar métricas cada hora o diariamente en lugar de en tiempo real si el volumen es alto
- Permitir drill-down: si hago clic en "Engineering: 25 días" debería ver lista de ofertas de Engineering con sus time-to-hire individuales
- Considerar dashboards personalizables donde cada usuario puede arrastrar widgets y configurar qué métricas ver

---

## US-011: Aprobar Oferta de Empleo Antes de Publicación

**Como** Manager de Contratación
**Quiero** revisar y aprobar ofertas de empleo creadas por reclutadores antes de que se publiquen
**Para que** pueda asegurar la calidad, exactitud de requisitos, y alignment con presupuesto antes de publicar

### Descripción Detallada
Workflow de aprobación simple donde las ofertas creadas pasan por un estado "Pending Approval" antes de poder ser publicadas. El manager recibe una notificación, puede revisar la oferta, agregar comentarios de revisión, y aprobar o rechazar. Si se rechaza, la oferta vuelve al reclutador con los comentarios para edición. Es una funcionalidad de governance útil en organizaciones grandes.

### Criterios de Aceptación

**CA-1: Enviar Oferta para Aprobación**
- **Dado que** he completado la creación de una oferta
- **Cuando** hago clic en "Enviar para Aprobación"
- **Entonces** el estado de la oferta cambia a "Pending Approval", se envía notificación al manager asignado, y la oferta aparece en su bandeja de tareas pendientes

**CA-2: Revisar Oferta Pendiente**
- **Dado que** soy un manager con ofertas pendientes de aprobación
- **Cuando** accedo a "Mis Aprobaciones Pendientes"
- **Entonces** veo lista de ofertas en estado "Pending Approval" con información clave (título, departamento, rango salarial, fecha de creación) y puedo hacer clic para revisar en detalle

**CA-3: Aprobar Oferta**
- **Dado que** he revisado una oferta y está correcta
- **Cuando** hago clic en "Aprobar"
- **Entonces** el estado cambia a "Approved", se notifica al reclutador, y la oferta está lista para publicarse (puede publicarla inmediatamente o programarla)

**CA-4: Rechazar Oferta con Comentarios**
- **Dado que** la oferta tiene errores o necesita cambios
- **Cuando** hago clic en "Rechazar", agrego comentarios "El rango salarial es muy alto para este nivel", y confirmo
- **Entonces** el estado cambia a "Rejected", los comentarios se envían al reclutador, y la oferta vuelve a estado "Draft" para edición

**CA-5: Notificaciones de Estado**
- **Dado que** soy el reclutador que creó la oferta
- **Cuando** el manager la aprueba o rechaza
- **Entonces** recibo notificación in-app y por email con el resultado y comentarios (si los hay)

**CA-6: Historial de Aprobaciones**
- **Dado que** quiero auditar el proceso
- **Cuando** veo el detalle de una oferta publicada
- **Entonces** puedo ver el historial: "Creada por María el 10/11 → Enviada para aprobación el 10/11 → Aprobada por Juan el 11/11 → Publicada el 12/11"

### Prioridad
**Could Have** - Prioridad 11

### Épica
Gestión de Ofertas

### Estimación Inicial
**13 Story Points** (baja complejidad)

### Dependencias Técnicas
- Sistema de notificaciones
- Máquina de estados extendida para ofertas (agregar estados "Pending Approval", "Rejected")
- Tabla de comentarios de revisión

### Dependencias de User Stories
- **US-001** (aprueba lo creado)
- **US-002** (previo a publicación)

### Riesgos
- **Bajo:** Puede ralentizar el proceso de publicación si los managers tardan en aprobar - necesita recordatorios y SLAs

### Notas Técnicas
- Considerar múltiples niveles de aprobación si la organización lo requiere (Reclutador → Manager → Director)
- Permitir configurar qué ofertas requieren aprobación (ej: solo si el salario >$X o si es nivel senior)
- Implementar auto-aprobación después de N días sin respuesta del manager (configurable)
- El sistema debe prevenir publicación de ofertas que requieren aprobación pero no han sido aprobadas

---

# PARTE 2: Priorización del Backlog

En esta sección se presentan 4 metodologías diferentes de priorización aplicadas al backlog de User Stories del MVP de LTI ATS. Cada método ofrece una perspectiva única sobre cómo ordenar el trabajo, considerando diferentes criterios de negocio, técnicos, y estratégicos.

---

## 2.1 Método MoSCoW

### Introducción al Método

MoSCoW es una técnica de priorización que clasifica requisitos en cuatro categorías: **Must Have** (crítico para el MVP), **Should Have** (importante pero no bloqueante), **Could Have** (deseable si hay tiempo), y **Won't Have** (fuera de scope para esta versión). Es ideal para definir el "walking skeleton" - el conjunto mínimo de funcionalidades que permite un flujo end-to-end.

### Aplicación al Backlog de LTI ATS

El análisis MoSCoW consideró tres criterios principales:
1. **Dependencias técnicas**: Construir primero las funcionalidades fundacionales
2. **Flujo end-to-end**: Tener un sistema usable lo antes posible
3. **Valor de negocio diferencial**: Priorizar las capacidades de IA que distinguen al producto

---

### Análisis Detallado por User Story

#### US-001: Crear Oferta de Empleo con Asistencia de IA

**Actor:** Reclutador, Manager de Contratación
**Épica:** Gestión de Ofertas

**Criterios de Evaluación:**
- **Valor de Negocio (5/5):** Fundamental para iniciar cualquier proceso de reclutamiento. Sin ofertas, no hay candidatos. Es el punto de entrada del flujo end-to-end.
- **Urgencia (5/5):** Completamente bloqueante. Es el primer paso lógico del proceso. Todas las demás funcionalidades dependen de que exista una oferta activa.
- **Complejidad Técnica (3/5):** Moderada. Requiere formularios, validaciones, integración con IA (LLM) para generación de descripciones, y gestión de estados (draft, pending approval, active).
- **Riesgo (3/5):** Medio. La integración con LLM (OpenAI/Anthropic) añade dependencia externa. Necesita manejo de prompts y respuestas de IA.
- **Dependencias:** 0 (no depende de otras US)

**Justificación:** Es la puerta de entrada al sistema. Sin esta funcionalidad, el ATS no puede operar. La asistencia de IA diferencia el producto pero no es bloqueante para el MVP mínimo.

---

#### US-002: Publicar Oferta en Múltiples Canales

**Actor:** Reclutador
**Épica:** Gestión de Ofertas

**Criterios de Evaluación:**
- **Valor de Negocio (4/5):** Alto valor para alcance de candidatos. Multiposting es un diferenciador competitivo y aumenta el volumen de candidaturas.
- **Urgencia (4/5):** Alta. Necesaria para que las ofertas lleguen a candidatos. Sin publicación, el sistema no sirve para atraer talento.
- **Complejidad Técnica (4/5):** Alta. Requiere integraciones con múltiples APIs externas (LinkedIn, Indeed, job boards), manejo de webhooks, retry logic, y tracking de fuentes.
- **Riesgo (4/5):** Alto. Múltiples dependencias externas, cada job board tiene su API y limitaciones. Necesita manejo robusto de errores.
- **Dependencias:** US-001 (debe existir una oferta para publicarla)

**Justificación:** Crítica para visibilidad y volumen de candidatos. La complejidad técnica es alta pero el valor justifica la inversión temprana.

---

#### US-003: Recibir y Parsear CVs Automáticamente

**Actor:** Sistema de IA, Candidato
**Épica:** Screening con IA

**Criterios de Evaluación:**
- **Valor de Negocio (5/5):** Core del diferenciador de IA. Automatiza una de las tareas más tediosas (lectura de CVs). Reduce tiempo de screening en 60%.
- **Urgencia (5/5):** Crítica. Sin parsing, el reclutador debe leer y transcribir CVs manualmente, anulando la propuesta de valor del producto.
- **Complejidad Técnica (5/5):** Muy alta. Requiere procesamiento de múltiples formatos (PDF, DOCX, imagen), OCR, NER (Named Entity Recognition), extracción de skills, experiencia, educación. Necesita modelos de ML entrenados.
- **Riesgo (4/5):** Alto. La precisión del parsing es crítica. CVs mal parseados generan frustración. Necesita fallback manual y mejora continua de modelos.
- **Dependencias:** US-002 (los CVs llegan tras publicar ofertas)

**Justificación:** Es el corazón de la propuesta de valor de IA. Alta complejidad pero indispensable para el MVP. Puede iterarse mejorando la precisión post-lanzamiento.

---

#### US-004: Visualizar Pipeline de Candidatos Tipo Kanban

**Actor:** Reclutador, Manager de Contratación
**Épica:** Pipeline y Tracking

**Criterios de Evaluación:**
- **Valor de Negocio (5/5):** Interface principal del ATS. El Kanban es el paradigma estándar de la industria. Sin esto, no hay visualización del proceso.
- **Urgencia (5/5):** Absolutamente crítica. Es la UI principal donde ocurre todo el trabajo diario. Sin pipeline visual, el producto no es usable.
- **Complejidad Técnica (3/5):** Moderada. Drag-and-drop, actualización de estados, filtros, búsqueda. Tecnología madura (React DnD, react-beautiful-dnd).
- **Riesgo (2/5):** Bajo. Patrón muy conocido y librerías estables. Riesgo principal es performance con cientos de candidatos (paginación, virtualización).
- **Dependencias:** US-003 (necesita candidatos parseados para mostrar)

**Justificación:** Interfaz central del producto. Sin esto, el sistema es inútil. Complejidad manejable y tecnología probada.

---

#### US-005: Filtrar y Rankear Candidatos con IA

**Actor:** Sistema de IA, Reclutador
**Épica:** Screening con IA

**Criterios de Evaluación:**
- **Valor de Negocio (5/5):** Núcleo del valor diferencial. El scoring y ranking automático es lo que reduce time-to-hire en 50%. Mejora calidad de matching en 40%.
- **Urgencia (5/5):** Crítica. Sin ranking, el reclutador debe revisar candidatos en orden de llegada, perdiendo los mejores. Anula la propuesta de valor de IA.
- **Complejidad Técnica (5/5):** Muy alta. Requiere modelo de scoring (ML), embeddings, comparación semántica, cálculo de compatibilidad, generación de resúmenes con LLM.
- **Riesgo (5/5):** Muy alto. La precisión del scoring determina el éxito del producto. Bias en el modelo puede generar discriminación. Necesita explicabilidad y auditoría.
- **Dependencias:** US-003 (necesita datos parseados), US-001 (necesita criterios de la oferta)

**Justificación:** Es el diferenciador killer del producto. Máxima complejidad pero máximo valor. Debe estar en el MVP pero puede refinarse post-lanzamiento.

---

#### US-006: Ver Perfil Completo de Candidato

**Actor:** Reclutador, Manager, Entrevistador
**Épica:** Pipeline y Tracking

**Criterios de Evaluación:**
- **Valor de Negocio (4/5):** Esencial para tomar decisiones informadas. Consolida toda la información del candidato en un solo lugar.
- **Urgencia (4/5):** Alta. Necesaria para revisar candidatos antes de entrevistas. Sin perfil completo, la información está fragmentada.
- **Complejidad Técnica (3/5):** Moderada. Vista de datos, timeline de interacciones, documentos adjuntos, historial de evaluaciones. Mayormente UI.
- **Riesgo (2/5):** Bajo. Principalmente presentación de datos ya existentes. Riesgo en performance con muchos documentos.
- **Dependencias:** US-003 (necesita datos parseados), US-004 (se accede desde el pipeline)

**Justificación:** Necesaria para usar el sistema efectivamente. Sin perfil completo, los usuarios no pueden evaluar candidatos adecuadamente.

---

#### US-007: Enviar Comunicaciones Automáticas a Candidatos

**Actor:** Sistema, Reclutador
**Épica:** Pipeline y Tracking

**Criterios de Evaluación:**
- **Valor de Negocio (4/5):** Mejora drásticamente la experiencia del candidato. Mantiene engagement y reduce la carga administrativa del reclutador.
- **Urgencia (3/5):** Media-alta. Importante para profesionalismo y employer branding, pero el MVP puede funcionar con comunicación manual inicial.
- **Complejidad Técnica (3/5):** Moderada. Integración con email provider (SendGrid), templates, variables dinámicas, triggers basados en eventos.
- **Riesgo (2/5):** Bajo. Tecnología madura. Riesgo principal: emails marcados como spam, necesita configuración SPF/DKIM correcta.
- **Dependencias:** US-004 (se dispara con cambios de etapa en el pipeline)

**Justificación:** Importante para experiencia del candidato pero no absolutamente bloqueante para MVP. Puede ser semi-automática inicialmente.

---

#### US-008: Programar Entrevistas con Integración de Calendario

**Actor:** Reclutador, Manager, Candidato
**Épica:** Evaluación Colaborativa

**Criterios de Evaluación:**
- **Valor de Negocio (4/5):** Ahorra mucho tiempo administrativo. Elimina el "ping-pong" de emails para encontrar horarios.
- **Urgencia (4/5):** Alta. Las entrevistas son un paso crítico del proceso. Sin scheduling, el proceso se ralentiza significativamente.
- **Complejidad Técnica (4/5):** Alta. Integración con Google Calendar y Outlook, manejo de zonas horarias, conflictos, disponibilidad compartida, invitaciones automáticas.
- **Riesgo (3/5):** Medio-alto. Las APIs de calendario son complejas y las integraciones tienden a fallar. Necesita robustez y fallback manual.
- **Dependencias:** US-006 (se programa desde el perfil del candidato)

**Justificación:** Muy importante para eficiencia operativa. La complejidad de integración es alta pero el valor lo justifica para el MVP.

---

#### US-009: Completar Evaluación Colaborativa con Scorecard

**Actor:** Entrevistador, Manager de Contratación
**Épica:** Evaluación Colaborativa

**Criterios de Evaluación:**
- **Valor de Negocio (5/5):** Core de la colaboración en tiempo real. Centraliza feedback, elimina silos, mejora calidad de decisiones de contratación.
- **Urgencia (4/5):** Alta. Necesaria para evaluación estructurada. Sin scorecards, las decisiones son subjetivas y no documentadas.
- **Complejidad Técnica (4/5):** Alta. Scorecards configurables, ponderación de competencias, agregación de scores, comentarios en tiempo real (WebSocket), votaciones.
- **Riesgo (3/5):** Medio. La colaboración en tiempo real añade complejidad técnica (concurrencia, sincronización). Necesita testing exhaustivo.
- **Dependencias:** US-006 (se completa desde el perfil), US-008 (post-entrevista)

**Justificación:** Diferenciador clave de colaboración. Esencial para decisiones de calidad. Alta complejidad pero crítica para el MVP.

---

#### US-010: Visualizar Dashboard con Métricas de Reclutamiento

**Actor:** Reclutador, Manager de Contratación, Admin
**Épica:** Reporting y Analytics

**Criterios de Evaluación:**
- **Valor de Negocio (3/5):** Importante para insights y optimización. Ayuda a justificar ROI del ATS. Pero no es necesario para las operaciones diarias.
- **Urgencia (2/5):** Baja-media. El MVP puede funcionar sin dashboard. Los reportes pueden generarse manualmente o en versiones posteriores.
- **Complejidad Técnica (3/5):** Moderada. Agregación de datos, cálculo de métricas (time-to-hire, conversion rates), visualizaciones, filtros por fecha/departamento.
- **Riesgo (2/5):** Bajo. Mayormente presentación de datos agregados. Riesgo en performance con grandes volúmenes de datos históricos.
- **Dependencias:** Todas las US anteriores (necesita datos de todo el proceso)

**Justificación:** Valioso para management y optimización, pero no bloqueante para operación del día a día. Puede ser versión básica en MVP.

---

#### US-011: Aprobar Oferta de Empleo Antes de Publicación

**Actor:** Manager de Contratación, Reclutador
**Épica:** Gestión de Ofertas

**Criterios de Evaluación:**
- **Valor de Negocio (3/5):** Importante para control y governance. Evita publicaciones incorrectas. Necesario en organizaciones grandes.
- **Urgencia (3/5):** Media. Deseable pero el MVP puede funcionar con publicación directa. Puede añadirse como mejora de proceso.
- **Complejidad Técnica (2/5):** Baja. Workflow de aprobación simple, notificaciones, estados (pending, approved, rejected), comentarios de revisión.
- **Riesgo (1/5):** Muy bajo. Flujo de aprobación estándar, bien conocido. Mínima complejidad técnica.
- **Dependencias:** US-001 (aprueba lo creado), US-002 (previo a publicación)

**Justificación:** Útil para control de calidad pero no crítico para MVP. Puede implementarse rápidamente si hay tiempo. Añade fricción al proceso.

---

### Tabla Completa de Priorización MoSCoW

| Prioridad | ID | Título | Actor | Épica | Valor Negocio (1-5) | Urgencia (1-5) | Complejidad (1-5) | Riesgo (1-5) | Dependencias | MoSCoW | Sprint Sugerido |
|-----------|----|----|-------|-------|---------------------|----------------|-------------------|--------------|--------------|--------|-----------------|
| 1 | US-001 | Crear Oferta de Empleo con Asistencia de IA | Reclutador, Manager | Gestión de Ofertas | 5 | 5 | 3 | 3 | 0 | **Must Have** | Sprint 1 |
| 2 | US-002 | Publicar Oferta en Múltiples Canales | Reclutador | Gestión de Ofertas | 4 | 4 | 4 | 4 | US-001 | **Must Have** | Sprint 1-2 |
| 3 | US-003 | Recibir y Parsear CVs Automáticamente | Sistema IA, Candidato | Screening con IA | 5 | 5 | 5 | 4 | US-002 | **Must Have** | Sprint 2-3 |
| 4 | US-004 | Visualizar Pipeline de Candidatos Tipo Kanban | Reclutador, Manager | Pipeline y Tracking | 5 | 5 | 3 | 2 | US-003 | **Must Have** | Sprint 2 |
| 5 | US-005 | Filtrar y Rankear Candidatos con IA | Sistema IA, Reclutador | Screening con IA | 5 | 5 | 5 | 5 | US-003, US-001 | **Must Have** | Sprint 3-4 |
| 6 | US-006 | Ver Perfil Completo de Candidato | Reclutador, Manager, Entrevistador | Pipeline y Tracking | 4 | 4 | 3 | 2 | US-003, US-004 | **Must Have** | Sprint 3 |
| 7 | US-008 | Programar Entrevistas con Integración de Calendario | Reclutador, Manager, Candidato | Evaluación Colaborativa | 4 | 4 | 4 | 3 | US-006 | **Should Have** | Sprint 4 |
| 8 | US-009 | Completar Evaluación Colaborativa con Scorecard | Entrevistador, Manager | Evaluación Colaborativa | 5 | 4 | 4 | 3 | US-006, US-008 | **Should Have** | Sprint 4-5 |
| 9 | US-007 | Enviar Comunicaciones Automáticas a Candidatos | Sistema, Reclutador | Pipeline y Tracking | 4 | 3 | 3 | 2 | US-004 | **Should Have** | Sprint 5 |
| 10 | US-010 | Visualizar Dashboard con Métricas de Reclutamiento | Reclutador, Manager, Admin | Reporting y Analytics | 3 | 2 | 3 | 2 | Todas las anteriores | **Could Have** | Sprint 6 |
| 11 | US-011 | Aprobar Oferta de Empleo Antes de Publicación | Manager, Reclutador | Gestión de Ofertas | 3 | 3 | 2 | 1 | US-001, US-002 | **Could Have** | Sprint 5-6 |

---

### Clasificación MoSCoW Detallada

#### **Must Have** (Críticas para MVP funcional end-to-end)

Estas User Stories forman el "walking skeleton" del producto - el flujo mínimo viable que permite completar un proceso de contratación de principio a fin:

1. **US-001: Crear Oferta de Empleo** - Sin ofertas no hay reclutamiento
2. **US-002: Publicar Oferta** - Sin publicación no llegan candidatos
3. **US-003: Recibir y Parsear CVs** - Automatización core del producto
4. **US-004: Pipeline Kanban** - Interfaz principal de trabajo
5. **US-005: Filtrar y Rankear con IA** - Diferenciador killer del producto
6. **US-006: Perfil de Candidato** - Necesario para revisar candidatos

**Total Must Have:** 6 US (54% del backlog)

---

#### **Should Have** (Importantes pero el MVP puede funcionar sin ellas)

Estas funcionalidades añaden valor significativo y completan la experiencia, pero hay workarounds manuales posibles:

7. **US-008: Programar Entrevistas** - Se puede hacer manualmente vía email al inicio, pero añade mucho valor para eficiencia
8. **US-009: Evaluación Colaborativa** - Se puede usar Google Docs al inicio, pero la colaboración en el sistema mejora la experiencia
9. **US-007: Comunicaciones Automáticas** - El reclutador puede enviar emails manualmente, pero automatización mejora experiencia del candidato

**Total Should Have:** 3 US (27% del backlog)

**Criterio de decisión:** Estas US mejoran significativamente la eficiencia y experiencia, pero si hay retrasos en el desarrollo, el MVP puede lanzarse sin ellas usando procesos manuales temporales.

---

#### **Could Have** (Deseables si hay tiempo en los 6 sprints)

Funcionalidades que añaden valor pero no son esenciales para el MVP:

10. **US-010: Dashboard de Métricas** - Valioso para insights pero no para operaciones diarias. Reportes pueden generarse manualmente al inicio.
11. **US-011: Aprobación de Ofertas** - Mejora el control pero añade fricción. Puede implementarse post-MVP si es necesario por governance.

**Total Could Have:** 2 US (19% del backlog)

**Criterio de decisión:** Estas US se implementarán solo si los sprints anteriores van adelantados. Si hay presión de tiempo, se mueven a la versión 1.1 (post-MVP).

---

#### **Won't Have (v1)** (Para versiones futuras)

Las siguientes funcionalidades del backlog original se posponen a v1.1 o v2.0:

- Video entrevistas nativas (hay alternativas como Zoom/Meet)
- Talent Pool avanzado (base de datos de candidatos pasivos)
- Portal del candidato (área privada)
- Scoring predictivo de retención (requiere datos históricos)
- Integraciones avanzadas (API abierta, Slack, Teams)
- Onboarding module

---

### Distribución en Sprints (Plan de 6 Sprints / 3 Meses)

#### **Sprint 1 (Semanas 1-2): Foundation - Gestión de Ofertas**

**User Stories:**
- **US-001:** Crear Oferta de Empleo con Asistencia de IA
- **US-002:** Publicar Oferta en Múltiples Canales (inicio)

**Entregable:**
Un reclutador puede crear una oferta de empleo con campos completos, utilizar la asistencia de IA para generar la descripción optimizada, y publicarla manualmente (o en 1-2 job boards si US-002 avanza rápido).

---

#### **Sprint 2 (Semanas 3-4): Ingesta y Visualización**

**User Stories:**
- **US-002:** Publicar Oferta en Múltiples Canales (completar)
- **US-003:** Recibir y Parsear CVs Automáticamente (inicio - parsing básico)
- **US-004:** Visualizar Pipeline de Candidatos Tipo Kanban

**Entregable:**
Las ofertas se publican en múltiples job boards automáticamente. Los CVs recibidos se parsean (extracción básica) y los candidatos aparecen en un tablero Kanban donde pueden moverse entre etapas drag-and-drop.

---

#### **Sprint 3 (Semanas 5-6): Inteligencia y Perfiles**

**User Stories:**
- **US-003:** Recibir y Parsear CVs Automáticamente (completar - parsing avanzado)
- **US-005:** Filtrar y Rankear Candidatos con IA (inicio - scoring básico)
- **US-006:** Ver Perfil Completo de Candidato

**Entregable:**
El parsing de CVs extrae skills, experiencia detallada, educación. Los candidatos se rankean automáticamente con un score de compatibilidad. Los reclutadores pueden ver perfiles completos.

**Milestone Crítico:** Al final de Sprint 3, el sistema debe permitir flujo completo end-to-end para screening automatizado. **Este es el MVP mínimo viable para beta testing**.

---

#### **Sprint 4 (Semanas 7-8): Evaluación Estructurada**

**User Stories:**
- **US-005:** Filtrar y Rankear Candidatos con IA (completar - refinamiento)
- **US-008:** Programar Entrevistas con Integración de Calendario
- **US-009:** Completar Evaluación Colaborativa con Scorecard (inicio)

**Entregable:**
El scoring de IA se refina con feedback real. Los reclutadores pueden programar entrevistas sincronizadas con Google Calendar/Outlook. Los entrevistadores pueden completar scorecards estructurados post-entrevista.

---

#### **Sprint 5 (Semanas 9-10): Colaboración y Automatización**

**User Stories:**
- **US-009:** Completar Evaluación Colaborativa con Scorecard (completar)
- **US-007:** Enviar Comunicaciones Automáticas a Candidatos
- **US-011:** Aprobar Oferta de Empleo Antes de Publicación (si hay capacidad)

**Entregable:**
Múltiples evaluadores pueden comentar en tiempo real sobre candidatos, votar decisiones, y colaborar sincrónicamente. El sistema envía automáticamente emails a candidatos cuando cambian de etapa.

---

#### **Sprint 6 (Semanas 11-12): Analytics, Pulido y Preparación para Producción**

**User Stories:**
- **US-010:** Visualizar Dashboard con Métricas de Reclutamiento (versión básica)
- **US-011:** Aprobar Oferta de Empleo Antes de Publicación (completar si no se hizo en Sprint 5)
- **Deuda técnica, bugs, refactoring, performance optimization**

**Entregable:**
Dashboard con métricas clave. Sistema completo, testeado, optimizado y documentado, listo para despliegue en producción.

**Milestone Final:** **MVP completo listo para producción**

---

### Justificación Estratégica de MoSCoW

#### 1. Criterios de Decisión Aplicados

**Dependencias técnicas (peso 40%):** Se priorizó construir primero las funcionalidades fundacionales siguiendo el flujo lógico del proceso.

**Flujo end-to-end (peso 35%):** Se buscó tener un "walking skeleton" funcional lo antes posible. Al terminar Sprint 3, el sistema permite validar el valor con usuarios reales.

**Valor de negocio diferencial (peso 25%):** Las funcionalidades de IA (parsing y scoring) se priorizaron alto porque son el diferenciador del producto.

---

#### 2. Métricas de Éxito del MVP

Al finalizar el Sprint 6, el MVP debe cumplir:

**Funcionales:**
- Un reclutador puede crear y publicar una oferta en <10 minutos
- Los CVs se parsean con >85% de precisión en campos críticos
- El scoring de IA rankea correctamente al candidato ideal en el top 3 en >70% de casos
- Un equipo puede evaluar colaborativamente y tomar una decisión en <5 minutos

**No funcionales:**
- El Kanban carga en <2 segundos con 100 candidatos
- Uptime >99.5% en horas laborales
- Todos los datos cumplen GDPR

**Negocio:**
- Time-to-hire reducido 40% vs proceso manual
- Candidatos screeneados por recruiter/día incremento de 3x
- NPS de usuarios beta ≥50

---

### Riesgos Principales y Mitigación

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|---------|------------|
| **Precisión de IA no alcanza expectativas** | Alta | Alto | Empezar con modelos pre-entrenados robustos. Permitir ajuste manual. Iteración continua. |
| **Integraciones externas fallan** | Media | Alto | Circuit breakers, fallbacks manuales, retry logic. |
| **Performance con alto volumen** | Media | Medio | Paginación, virtualización, caching, índices de DB. |
| **Scope creep** | Alta | Medio | Backlog priorizado estricto. "Could Have" y "Won't Have" claramente definidos. |
| **Retrasos en desarrollo de ML** | Media | Alto | ML engineer dedicado 100%. Plan B sin IA como fallback temporal. |

---

### Conclusión MoSCoW

Este backlog priorizado asegura que al final de los 6 sprints (3 meses) se entregue un MVP funcional de LTI ATS que:

1. **Cumple la propuesta de valor core:** Automatización de screening con IA y colaboración en tiempo real
2. **Es end-to-end:** Permite completar un proceso de contratación de inicio a fin
3. **Es diferenciado:** Las capacidades de IA están en el core, no como "nice to have"
4. **Es escalable:** La arquitectura soporta crecimiento y la priorización permite iteración post-MVP

La estrategia equilibra **valor de negocio**, **dependencias técnicas** y **gestión de riesgo**, asegurando que incluso si hay retrasos, el MVP mínimo (hasta Sprint 3) es suficiente para validar el producto con usuarios reales.

---


## 2.2 Método RICE Score

### Introducción al Método

RICE (Reach × Impact × Confidence / Effort) es una metodología cuantitativa de priorización que asigna un score numérico a cada iniciativa basándose en cuatro factores:
- **Reach**: Número de usuarios/candidatos afectados por periodo de tiempo
- **Impact**: Magnitud del impacto en los usuarios (escala 0.25-3: Minimal, Low, Medium, High, Massive)
- **Confidence**: Nivel de certeza en las estimaciones (0%-100%)
- **Effort**: Recursos necesarios (en person-months)

**Fórmula:** `RICE Score = (Reach × Impact × Confidence) / Effort`

### Aplicación al Backlog de LTI ATS

Para este análisis asumimos:
- **Reach** por trimestre (3 meses de MVP)
- **Effort** en person-months del equipo (5 devs + 1 ML engineer + 1 QA)

---

### Tabla de Scoring RICE

| ID | User Story | Reach (usuarios/trim) | Impact (0.25-3) | Confidence (%) | Effort (PM) | RICE Score | Rank |
|----|------------|----------------------|-----------------|----------------|-------------|------------|------|
| US-001 | Crear Oferta de Empleo con IA | 50 (reclutadores) | 3 (Massive) | 90% | 1.5 | **90** | 1 |
| US-002 | Publicar Oferta en Múltiples Canales | 50 | 2 (High) | 70% | 0.75 | **93** | 2 |
| US-004 | Visualizar Pipeline Kanban | 80 (recl.+managers) | 3 (Massive) | 95% | 0.5 | **456** | 3 |
| US-003 | Parsear CVs Automáticamente | 500 (candidatos) | 3 (Massive) | 70% | 1.25 | **840** | 4 |
| US-005 | Filtrar y Rankear con IA | 500 | 3 (Massive) | 60% | 1.25 | **720** | 5 |
| US-006 | Ver Perfil Completo Candidato | 80 | 2 (High) | 90% | 0.5 | **288** | 6 |
| US-008 | Programar Entrevistas | 50 | 2 (High) | 60% | 0.75 | **80** | 7 |
| US-009 | Evaluación Colaborativa Scorecard | 30 (entrevistadores) | 2 (High) | 70% | 0.75 | **56** | 8 |
| US-007 | Comunicaciones Automáticas | 500 | 1 (Medium) | 80% | 0.5 | **800** | 9 |
| US-010 | Dashboard Métricas | 20 (managers) | 1 (Medium) | 80% | 0.5 | **32** | 10 |
| US-011 | Aprobar Ofertas | 30 | 0.5 (Low) | 90% | 0.25 | **54** | 11 |

---

### Priorización Final por RICE Score

**Orden sugerido de implementación:**

1. **US-003: Parsear CVs** (RICE: 840) - Máximo reach (500 candidatos), impacto masivo
2. **US-007: Comunicaciones Automáticas** (RICE: 800) - Alto reach, esfuerzo bajo
3. **US-005: Rankear con IA** (RICE: 720) - Alto impacto pero confidence moderado
4. **US-004: Pipeline Kanban** (RICE: 456) - Impacto masivo, esfuerzo bajo
5. **US-006: Perfil Candidato** (RICE: 288) - Buen balance impact/effort
6. **US-002: Publicar Ofertas** (RICE: 93) - Confidence media por integraciones externas
7. **US-001: Crear Oferta con IA** (RICE: 90) - Foundation necesaria pero reach limitado
8. **US-008: Scheduling** (RICE: 80) - Esfuerzo medio, confidence baja
9. **US-009: Scorecards** (RICE: 56) - Reach limitado (solo entrevistadores)
10. **US-011: Aprobar Ofertas** (RICE: 54) - Bajo impacto, añade fricción
11. **US-010: Dashboard** (RICE: 32) - Reach muy bajo (solo managers)

---

### Análisis de Resultados RICE

#### Insights Clave:

**1. Las funcionalidades con mayor reach dominan:**
- US-003 (Parsing) y US-007 (Comunicaciones) tienen RICE altísimos porque afectan a los 500 candidatos del trimestre
- Sin embargo, esto crea una distorsión: US-007 (comunicaciones) no es más importante que US-001 (crear ofertas)

**2. Distorsión por Reach de Candidatos vs Reclutadores:**
- El método RICE tiende a favorecer features que afectan a muchos usuarios (candidatos) sobre features que afectan a pocos usuarios críticos (reclutadores)
- Esto puede llevar a priorizar experiencia del candidato sobre productividad del reclutador, lo cual es problemático para un MVP interno

**3. Orden Contraintuitivo:**
- RICE sugiere empezar con US-003 (Parsing) antes que US-001 (Crear Ofertas)
- Esto es técnicamente imposible por dependencias: no puedes parsear CVs si no existen ofertas
- **El método RICE no considera dependencias técnicas explícitamente**

**4. Confidence como Factor Corrector:**
- Las integraciones externas (US-002: 70%, US-008: 60%) tienen confidence reducido, lo que baja su score correctamente
- Las capacidades de IA (US-003: 70%, US-005: 60%) también tienen confidence medio por incertidumbre en precisión de modelos

#### Fortalezas del Método RICE:

- **Cuantitativo y menos subjetivo** que MoSCoW
- **Penaliza el esfuerzo** correctamente: features de bajo esfuerzo (US-004, US-007) suben en prioridad
- **Considera la escala**: reconoce que features que afectan a más usuarios tienen mayor valor agregado
- **El factor Confidence es útil** para incorporar riesgo e incertidumbre

#### Debilidades del Método RICE:

- **No considera dependencias técnicas**: El orden resultante puede ser imposible de ejecutar
- **Sesgo hacia alto reach**: Sobre-prioriza features con muchos usuarios afectados, incluso si no son críticas
- **Estimaciones de Reach son especulativas** en un MVP sin usuarios: ¿Cómo sabemos que tendremos 500 candidatos en trimestre 1?
- **No distingue entre tipos de usuarios**: 500 candidatos externos vs 10 reclutadores internos no son equivalentes en un B2B SaaS
- **Requiere ajustes manuales post-score**: El output necesita ser reordenado considerando dependencias

---

### Ajuste de RICE Considerando Dependencias

Si reordenamos el RICE Score respetando dependencias técnicas:

**Orden Ajustado:**

1. **US-001: Crear Oferta** (RICE: 90) - Bloqueante, debe ser primero
2. **US-002: Publicar Oferta** (RICE: 93) - Depende de US-001
3. **US-003: Parsear CVs** (RICE: 840) - Depende de US-002, máximo valor RICE
4. **US-004: Pipeline Kanban** (RICE: 456) - Depende de US-003
5. **US-005: Rankear con IA** (RICE: 720) - Depende de US-003
6. **US-006: Perfil Candidato** (RICE: 288) - Depende de US-003 y US-004
7. **US-007: Comunicaciones** (RICE: 800) - Depende de US-004 (pipeline con etapas)
8. **US-008: Scheduling** (RICE: 80) - Depende de US-006
9. **US-009: Scorecards** (RICE: 56) - Depende de US-008
10. **US-010: Dashboard** (RICE: 32) - Depende de todas
11. **US-011: Aprobar Ofertas** (RICE: 54) - Depende de US-001, US-002

**Observación:** Después del ajuste por dependencias, el orden es casi idéntico a MoSCoW con la excepción de que US-007 (Comunicaciones) tiene mayor prioridad por su alto RICE score.

---

### Conclusión RICE

**Cuándo usar RICE:**
- Cuando tienes datos históricos de reach y uso
- Para productos maduros con múltiples features compitiendo por recursos
- Cuando el equipo necesita un método "objetivo" con números para justificar decisiones

**Cuándo NO usar RICE:**
- Para MVPs sin usuarios donde el reach es especulativo
- Cuando las dependencias técnicas son complejas (RICE no las modela)
- En productos donde todos los usuarios no tienen igual valor (B2B con pocos clientes de alto valor)

**Para LTI ATS MVP:** RICE es útil como "segundo filtro" después de MoSCoW, pero no como método primario debido a las dependencias técnicas estrictas y la falta de datos históricos de reach.

---

## 2.3 Método Kano + Value/Effort

### Introducción al Método

El **Modelo Kano** clasifica funcionalidades según cómo impactan en la satisfacción del cliente:

- **Basic (Must-be)**: Esperadas por default. Su ausencia causa insatisfacción, pero su presencia no genera deleite.
- **Performance (Satisfiers)**: Mayor rendimiento = mayor satisfacción. Relación lineal.
- **Excitement (Delighters)**: Inesperadas, generan deleite. Su ausencia no causa insatisfacción.
- **Indifferent**: No afectan la satisfacción significativamente.
- **Reverse**: Pueden causar insatisfacción si están presentes (features no deseadas).

Combinado con **Value/Effort Matrix** (2x2: High/Low Value × High/Low Effort):
- **Quick Wins** (High Value, Low Effort) - Prioridad máxima
- **Big Bets** (High Value, High Effort) - Necesarios pero costosos
- **Fill-ins** (Low Value, Low Effort) - Si sobra tiempo
- **Time Sinks** (Low Value, High Effort) - Evitar

---

### Clasificación Kano de User Stories

| ID | User Story | Categoría Kano | Justificación |
|----|------------|----------------|---------------|
| US-001 | Crear Oferta de Empleo | **Basic** | Sin esto, el ATS no funciona. Es el requisito mínimo esperado. |
| US-002 | Publicar Oferta en Múltiples Canales | **Performance** | Más canales = más candidatos. Relación directa con efectividad. |
| US-003 | Parsear CVs Automáticamente | **Excitement** | Diferenciador con IA. Los usuarios esperan ingreso manual, esto los deleita. |
| US-004 | Pipeline Kanban | **Basic** | Interfaz estándar esperada en cualquier ATS. Sin esto, inutilizable. |
| US-005 | Rankear Candidatos con IA | **Excitement** | Scoring automático es el "wow factor". Inesperado y muy valorado. |
| US-006 | Ver Perfil Candidato | **Basic** | Necesario para revisar candidatos. Funcionalidad core esperada. |
| US-007 | Comunicaciones Automáticas | **Performance** | Mejora experiencia proporcionalmente. Más automatización = más satisfacción. |
| US-008 | Programar Entrevistas | **Performance** | Ahorra tiempo administrativo. Cuanto más integrado, mejor. |
| US-009 | Scorecards Colaborativos | **Excitement** | Colaboración en tiempo real sorprende positivamente. No esperado en ATS básicos. |
| US-010 | Dashboard Métricas | **Indifferent** | Útil para managers pero no afecta operación diaria de reclutadores. |
| US-011 | Aprobar Ofertas | **Reverse** | Puede generar fricción. Algunos usuarios lo ven como burocracia innecesaria. |

---

### Matriz Value/Effort

**Cuadrantes:**

**HIGH VALUE + LOW EFFORT (Quick Wins):**
- US-001: Crear Oferta
- US-004: Pipeline Kanban
- US-006: Perfil Candidato

**HIGH VALUE + HIGH EFFORT (Big Bets):**
- US-003: Parsear CVs con IA
- US-005: Rankear con IA
- US-002: Publicar en Múltiples Canales

**MEDIUM VALUE + MEDIUM EFFORT (Performance Enhancers):**
- US-007: Comunicaciones Automáticas
- US-008: Programar Entrevistas
- US-009: Scorecards Colaborativos

**LOW VALUE (Fill-ins / Time Sinks):**
- US-010: Dashboard Métricas (Low effort, Indifferent)
- US-011: Aprobar Ofertas (Low effort, Reverse)

---

### Priorización Final Kano + Value/Effort

**Orden de Implementación Recomendado:**

1. **US-001: Crear Oferta** (Basic + Quick Win)
2. **US-004: Pipeline Kanban** (Basic + Quick Win)
3. **US-006: Perfil Candidato** (Basic + Quick Win)
4. **US-003: Parsear CVs** (Excitement + Big Bet) ⚡
5. **US-005: Rankear con IA** (Excitement + Big Bet) ⚡
6. **US-002: Publicar Ofertas** (Performance + Big Bet)
7. **US-009: Scorecards** (Excitement + Medium Effort)
8. **US-008: Scheduling** (Performance + High Effort)
9. **US-007: Comunicaciones** (Performance + Medium Effort)
10. **US-010: Dashboard** (Indifferent + Fill-in)
11. **US-011: Aprobar Ofertas** (Reverse - evaluar necesidad)

⚡ **Features Excitement Kano** - Diferenciadores que generan "wow"

---

### Análisis Estratégico Kano

#### Insights Clave:

**1. Los "Excitement" features son el diferenciador:**
- **US-003 (Parsing)** y **US-005 (Scoring)** son los únicos Excitement features
- Son lo que hace a LTI ATS memorable y diferente de competidores
- **Recomendación:** Invertir los recursos de ML prioritariamente en estos dos

**2. Los "Basic" features son el precio de entrada:**
- **US-001, US-004, US-006** son esperados por default
- Sin ellos, el producto ni siquiera es considerado viable
- Son rápidos de implementar (Quick Wins) - hacerlos primero

**3. Cuidado con "Reverse" features:**
- **US-011 (Aprobar Ofertas)** puede ser contraproducente
- En startups ágiles, agregar aprobaciones ralentiza el proceso
- **Recomendación:** Omitir del MVP y agregar solo si clientes enterprise lo solicitan

**4. "Performance" features son mejoras incrementales:**
- **US-002, US-007, US-008** mejoran la experiencia pero no sorprenden
- Son importantes para completitud del producto pero no son "wow factors"
- Implementar después de asegurar Basic + Excitement

---

### Conclusión Kano + Value/Effort

**Fortalezas:**
- Identifica claramente los diferenciadores (Excitement) vs requisitos básicos (Basic)
- La matriz Value/Effort ayuda a priorizar Quick Wins primero
- Detecta features potencialmente contraproducentes (Reverse)

**Debilidades:**
- La clasificación Kano es subjetiva y requiere research con usuarios
- No considera dependencias técnicas explícitamente
- Puede sub-priorizar Basic features si son de alto esfuerzo

**Para LTI ATS:** Este método es muy efectivo para identificar que las capacidades de IA (US-003, US-005) deben ser la inversión principal, y que algunas features (US-011) pueden ser omitidas sin impacto negativo.

---

## 2.4 Método Story Mapping

### Introducción al Método

**Story Mapping** (Jeff Patton) organiza User Stories en un mapa bidimensional que visualiza el journey del usuario (horizontalmente) y las releases/prioridades (verticalmente). Permite identificar el "walking skeleton" - el conjunto mínimo de funcionalidades que completa un flujo end-to-end.

**Estructura:**
- **Eje Horizontal (User Activities)**: Los pasos principales del journey del usuario en orden cronológico
- **Eje Vertical (Releases)**: Priorización de stories bajo cada activity (arriba = más prioritario)
- **Walking Skeleton**: La fila superior - el MVP mínimo que permite completar el journey

---

### Story Map para LTI ATS

#### User Activities (Backbone del Journey)

**Journey del Reclutador:**
1. **Crear Oferta** → 2. **Atraer Candidatos** → 3. **Screenear CVs** → 4. **Gestionar Pipeline** → 5. **Evaluar Candidatos** → 6. **Tomar Decisión** → 7. **Analizar Proceso**

---

### Mapeo de User Stories por Activity

#### **Activity 1: Crear Oferta**
- **Walking Skeleton (Release 1):** US-001 - Crear Oferta con IA
- **Release 2:** US-011 - Aprobar Oferta (governance)

#### **Activity 2: Atraer Candidatos**
- **Walking Skeleton (Release 1):** US-002 - Publicar en Múltiples Canales

#### **Activity 3: Screenear CVs**
- **Walking Skeleton (Release 1):** US-003 - Parsear CVs Automáticamente
- **Walking Skeleton (Release 1):** US-005 - Rankear con IA

#### **Activity 4: Gestionar Pipeline**
- **Walking Skeleton (Release 1):** US-004 - Pipeline Kanban
- **Walking Skeleton (Release 1):** US-006 - Perfil Completo Candidato
- **Release 2:** US-007 - Comunicaciones Automáticas

#### **Activity 5: Evaluar Candidatos**
- **Release 2:** US-008 - Programar Entrevistas
- **Release 2:** US-009 - Scorecards Colaborativos

#### **Activity 6: Tomar Decisión**
- *(Cubierto por US-009 - Scorecards con votación)*

#### **Activity 7: Analizar Proceso**
- **Release 3 (Nice-to-have):** US-010 - Dashboard Métricas

---

### Visualización del Story Map

```
USER JOURNEY →    Crear     Atraer      Screenear    Gestionar    Evaluar     Decisión    Analizar
                  Oferta    Candidatos  CVs          Pipeline     Candidatos

WALKING           US-001    US-002      US-003       US-004
SKELETON          (Crear)   (Publicar)  (Parse+      (Kanban+
(Release 1)                              US-005       US-006)
Sprint 1-3                               Rank)
═══════════════════════════════════════════════════════════════════════════════════════════

RELEASE 2         US-011                             US-007       US-008      US-009
(Sprint 4-5)      (Aprobar)                          (Email)      (Sched.     (Scorecard)
                                                                   Entrev.)
───────────────────────────────────────────────────────────────────────────────────────────

RELEASE 3                                                                                  US-010
(Sprint 6)                                                                                 (Dashboard)
```

---

### Priorización por Story Mapping

**Release 1 (Walking Skeleton - MVP Crítico):**
1. US-001: Crear Oferta con IA
2. US-002: Publicar en Múltiples Canales
3. US-003: Parsear CVs Automáticamente
4. US-005: Rankear Candidatos con IA
5. US-004: Visualizar Pipeline Kanban
6. US-006: Ver Perfil Completo Candidato

**Total Release 1:** 6 User Stories (Sprints 1-3)

---

**Release 2 (Completar Experiencia):**
7. US-007: Comunicaciones Automáticas
8. US-008: Programar Entrevistas
9. US-009: Evaluación Colaborativa
10. US-011: Aprobar Ofertas (opcional)

**Total Release 2:** 4 User Stories (Sprints 4-5)

---

**Release 3 (Analytics y Optimización):**
11. US-010: Dashboard Métricas

**Total Release 3:** 1 User Story (Sprint 6)

---

### Análisis del Walking Skeleton

#### ¿Por qué estas 6 US forman el Walking Skeleton?

**Criterio:** Permiten completar el journey end-to-end desde crear oferta hasta tomar decisión de contratación.

**Flujo completo:**
1. Reclutador **crea oferta** (US-001) con asistencia de IA
2. **Publica en LinkedIn e Indeed** (US-002) para atraer candidatos
3. Candidatos aplican y CVs se **parsean automáticamente** (US-003)
4. Sistema **rankea candidatos** por compatibilidad (US-005)
5. Reclutador ve candidatos en **pipeline Kanban** (US-004) ordenados por score
6. Revisa **perfil completo** (US-006) de top candidatos
7. Mueve candidatos entre etapas hasta decisión final

**Resultado:** Al final de Sprint 3, un reclutador puede usar el sistema para screenear candidatos automáticamente con IA. **Este es el MVP viable mínimo**.

---

### Comparación con Otros Métodos

| Método | US Priorizadas en MVP (Top 6) | Concordancia |
|--------|-------------------------------|--------------|
| **MoSCoW** | US-001, 002, 003, 004, 005, 006 | ✅ 100% |
| **RICE (ajustado)** | US-001, 002, 003, 004, 005, 006 | ✅ 100% |
| **Kano** | US-001, 004, 006, 003, 005, 002 | ✅ 100% (orden ligeramente diferente) |
| **Story Mapping** | US-001, 002, 003, 005, 004, 006 | ✅ 100% |

**Observación Clave:** **Los 4 métodos convergen en las mismas 6 User Stories para el MVP**. Esto valida fuertemente la estrategia de priorización.

---

### Fortalezas de Story Mapping

1. **Visualiza el journey completo**: Fácil entender el flujo end-to-end
2. **Identifica gaps**: Si falta una activity en el journey, se detecta visualmente
3. **Walking Skeleton claro**: La fila superior es el MVP por definición
4. **Facilita comunicación con stakeholders**: El mapa es intuitivo para no-técnicos
5. **Considera la secuencia temporal**: Las activities están en orden cronológico del usuario

---

### Debilidades de Story Mapping

1. **No es cuantitativo**: No hay scores numéricos, es más visual/cualitativo
2. **Puede ser subjetivo**: Decidir qué stories van en Release 1 vs 2 requiere juicio
3. **No considera esfuerzo explícitamente**: Stories complejas y simples están al mismo nivel visual
4. **Requiere sesiones colaborativas**: Funciona mejor en workshops con el equipo, no es un método que se aplica individualmente

---

### Conclusión Story Mapping

**Cuándo usar Story Mapping:**
- Al inicio del producto para definir el journey completo
- Cuando el equipo necesita alinearse en la visión end-to-end
- Para comunicar la estrategia de releases a stakeholders no técnicos
- Cuando hay confusión sobre qué constituye un "MVP mínimo"

**Para LTI ATS:** Story Mapping es el método más efectivo para este caso porque:
- Visualiza claramente el journey del reclutador
- Identifica el walking skeleton de 6 US que permiten flujo completo
- Alinea al equipo en que Sprint 3 es un milestone crítico (MVP funcional)
- Los 3 releases mapean perfectamente a la estrategia de 6 sprints

**Recomendación:** Usar Story Mapping como método principal para LTI ATS, complementado con MoSCoW para validar la clasificación Must/Should/Could.

---

# PARTE 3: Análisis Comparativo de Metodologías

## Tabla Comparativa Completa

| Criterio | MoSCoW | RICE Score | Kano + Value/Effort | Story Mapping |
|----------|---------|------------|---------------------|---------------|
| **Tipo** | Cualitativo | Cuantitativo | Híbrido | Visual/Cualitativo |
| **Complejidad** | Baja | Media | Media | Media |
| **Tiempo requerido** | 2-3 horas | 4-5 horas | 3-4 horas | 2-3 horas (workshop) |
| **Output principal** | Categorías M/S/C/W | Score numérico | Matriz 2x2 + Categorías Kano | Mapa visual de journey |
| **Considera dependencias** | ❌ No explícitamente | ❌ No | ❌ No | ✅ Sí (implícitamente por secuencia) |
| **Considera esfuerzo** | ⚠️ Informalmente | ✅ Sí (denominador) | ✅ Sí (matriz) | ❌ No explícitamente |
| **Identifica diferenciadores** | ⚠️ Parcial (Must vs Should) | ❌ No | ✅ Sí (Excitement) | ⚠️ Implícito |
| **Facilidad de comunicación** | Alta (términos simples) | Media (requiere explicar fórmula) | Media | Muy Alta (visual intuitivo) |
| **Objetividad** | Baja (subjetivo) | Alta (basado en números) | Media | Baja (subjetivo) |
| **Mejor para MVPs** | ✅ Excelente | ⚠️ Regular (reach especulativo) | ✅ Muy bueno | ✅ Excelente |
| **Escalabilidad** | Media (M/S/C/W se vuelve confuso con 50+ items) | Alta (score ordena fácilmente) | Media | Baja (mapa físico limitado) |

---

## Resultados de Priorización por Método

### Top 6 User Stories (MVP Crítico)

Todos los métodos convergieron en las mismas 6 US, con variaciones menores en orden:

| Rank | MoSCoW | RICE (ajustado) | Kano | Story Mapping |
|------|---------|-----------------|------|---------------|
| 1 | US-001 | US-001 | US-001 | US-001 |
| 2 | US-002 | US-002 | US-004 | US-002 |
| 3 | US-003 | US-003 | US-006 | US-003 |
| 4 | US-004 | US-004 | US-003 | US-005 |
| 5 | US-005 | US-005 | US-005 | US-004 |
| 6 | US-006 | US-006 | US-002 | US-006 |

**Convergencia:** ✅ **100% de acuerdo en las 6 US críticas**

Las pequeñas variaciones en orden (ej: US-004 antes que US-003 en Kano) no son problemáticas porque US-003 y US-004 pueden trabajarse en paralelo en Sprint 2.

---

## Evaluación Cuantitativa de Métodos

### Scoring de Métodos (0-50 puntos)

| Criterio (peso) | MoSCoW | RICE | Kano | Story Mapping |
|-----------------|---------|------|------|---------------|
| **Claridad de output** (10) | 9 | 7 | 7 | 10 |
| **Facilidad de uso** (8) | 9 | 5 | 7 | 8 |
| **Considera dependencias** (10) | 4 | 3 | 4 | 9 |
| **Identifica diferenciadores** (8) | 6 | 4 | 9 | 7 |
| **Objetividad** (5) | 4 | 9 | 6 | 4 |
| **Aplicable a MVPs** (9) | 8 | 5 | 8 | 9 |
| **TOTAL** (50) | **40** | **33** | **41** | **47** |

---

### Análisis de Resultados

#### 🥇 **Story Mapping - 47/50 puntos (Ganador)**

**Fortalezas:**
- Máxima claridad visual del journey
- Considera dependencias implícitamente (secuencia de activities)
- Identifica el walking skeleton de forma natural
- Excelente para comunicación con stakeholders

**Debilidades:**
- No es objetivo (requiere juicio)
- No considera esfuerzo explícitamente

**Recomendación:** **Método principal para LTI ATS**

---

#### 🥈 **Kano + Value/Effort - 41/50 puntos (Muy cerca del ganador)**

**Fortalezas:**
- Identifica claramente los "Excitement" features (diferenciadores)
- La matriz Value/Effort prioriza Quick Wins correctamente
- Detecta features Reverse (potencialmente contraproducentes)

**Debilidades:**
- Clasificación Kano es subjetiva
- No modela dependencias

**Recomendación:** **Excelente complemento a Story Mapping** para identificar diferenciadores

---

#### 🥉 **MoSCoW - 40/50 puntos (Sólido método tradicional)**

**Fortalezas:**
- Simple y rápido de aplicar
- Términos intuitivos (Must/Should/Could/Won't)
- Excelente para MVPs con restricciones de tiempo

**Debilidades:**
- No considera dependencias explícitamente
- Las 4 categorías pueden ser insuficientes para backlogs grandes

**Recomendación:** Buen método cuando el equipo necesita **decidir rápidamente** qué entra en el MVP

---

#### **RICE Score - 33/50 puntos (Útil pero limitado para MVPs)**

**Fortalezas:**
- Cuantitativo y "objetivo"
- Penaliza esfuerzo correctamente
- Útil para justificar decisiones con números

**Debilidades:**
- Requiere datos de reach que no existen en MVPs
- No considera dependencias (orden resultante puede ser imposible)
- Sesgo hacia alto reach distorsiona resultados

**Recomendación:** Usar como **validación secundaria** después de Story Mapping, no como método primario

---

## Recomendación Final

### Estrategia de Priorización para LTI ATS

**Enfoque Híbrido (Combinar métodos):**

1. **Primer paso: Story Mapping** (Workshop de 3 horas con el equipo)
   - Mapear el journey completo del reclutador
   - Identificar el walking skeleton (Release 1)
   - Definir Release 2 y Release 3

2. **Segundo paso: Kano Analysis** (1 hora)
   - Clasificar cada US en Basic/Performance/Excitement
   - Validar que el walking skeleton incluye todos los Basic features
   - Asegurar que los Excitement features (US-003, US-005) están en Release 1

3. **Tercer paso: MoSCoW** (30 minutos)
   - Mapear el Story Map a categorías Must/Should/Could
   - Usar como checklist final antes de iniciar Sprint 1

4. **Validación opcional: RICE Score** (1 hora si se requiere justificación cuantitativa)
   - Calcular scores para validar que las decisiones son defendibles con números
   - Útil si hay que presentar a stakeholders que prefieren datos cuantitativos

---

### Resultado Final Recomendado

**MVP (Release 1) - Sprints 1-3:**
- US-001: Crear Oferta (Sprint 1)
- US-002: Publicar Oferta (Sprint 1-2)
- US-003: Parsear CVs (Sprint 2-3)
- US-004: Pipeline Kanban (Sprint 2)
- US-005: Rankear con IA (Sprint 3-4)
- US-006: Perfil Candidato (Sprint 3)

**Release 2 - Sprints 4-5:**
- US-008: Programar Entrevistas (Sprint 4)
- US-009: Scorecards (Sprint 4-5)
- US-007: Comunicaciones (Sprint 5)

**Release 3 - Sprint 6:**
- US-010: Dashboard (Sprint 6)
- Refinamiento, bugs, performance

**Omitir del MVP:**
- US-011: Aprobar Ofertas (Reverse en Kano - agregar solo si se solicita)

---

# PARTE 4: Tickets Técnicos (US-001)

A continuación se presenta la descomposición de la User Story **US-001: Crear Oferta de Empleo con Asistencia de IA** en 13 tickets técnicos detallados, organizados por área (Data, Backend, AI, Frontend, Testing, DevOps).

---

## Resumen Ejecutivo

**User Story:** US-001 - Crear Oferta de Empleo con Asistencia de IA

**Estimación Total:** 68 Story Points (base) | 83 SP (con contingencia)

**Duración Estimada:** 2 sprints (4 semanas)

**Equipo Requerido:**
- 2 Backend Devs
- 2 Frontend Devs
- 1 ML Engineer
- 1 QA

---

## DATA-001: Diseño y Migración de Base de Datos

**Título:** Crear tabla `job_postings` con schema completo

**Descripción:**
Diseñar e implementar el schema de base de datos para almacenar ofertas de empleo, incluyendo campos estructurados y JSONB para flexibilidad.

**Tareas:**
1. Diseñar schema con campos: id, title, department, location, employment_type, salary_range_min, salary_range_max, description (TEXT), requirements (JSONB), responsibilities (JSONB), benefits (JSONB), status (ENUM: draft/pending_approval/active/closed), created_by, created_at, updated_at
2. Crear migration con Flyway/Liquibase
3. Agregar índices: title (GIN para full-text search), status, created_at, created_by
4. Crear tabla de auditoría `job_posting_audit` para tracking de cambios
5. Scripts de rollback

**Criterios de Aceptación:**
- Migration ejecuta sin errores en local, dev, staging
- Índices mejoran queries de listado en >50%
- Schema soporta inserción de 10,000 ofertas de test sin performance issues

**Estimación:** 3 Story Points

**Dependencias:** Ninguna

**Riesgos:**
- El campo description puede ser muy largo (>50k caracteres) - considerar TEXT o JSONB

**Asignado a:** Backend Dev #1

---

## BACK-002: Entidad JPA y DTOs

**Título:** Crear entidad JobPosting y DTOs de request/response

**Descripción:**
Implementar la capa de persistencia con JPA entity, repository, y DTOs para comunicación con frontend.

**Tareas:**
1. Crear entidad `JobPosting` con anotaciones JPA (@Entity, @Table, validaciones)
2. Implementar JobPostingRepository extends JpaRepository con custom queries
3. Crear DTOs: JobPostingCreateRequest, JobPostingUpdateRequest, JobPostingResponse
4. Mappers entre Entity <> DTO (usar MapStruct)
5. Unit tests para repository (mínimo 80% coverage)

**Criterios de Aceptación:**
- Entidad mapea correctamente todos los campos de la tabla
- Repository tiene queries optimizadas para: findByStatus, findByCreatedBy, fullTextSearch por title
- DTOs validan campos obligatorios con Bean Validation (@NotNull, @Size, @Email)
- Mappers convierten correctamente, incluyendo JSONB fields

**Estimación:** 5 Story Points

**Dependencias:** DATA-001

**Asignado a:** Backend Dev #1

---

## BACK-003: API REST CRUD

**Título:** Implementar endpoints REST para gestión de ofertas

**Descripción:**
Crear controller REST con endpoints para CRUD de ofertas: crear, listar, obtener detalle, actualizar, cambiar estado, eliminar (soft delete).

**Tareas:**
1. Crear `JobPostingController` con endpoints:
   - POST /api/v1/job-postings (crear)
   - GET /api/v1/job-postings (listar con paginación y filtros)
   - GET /api/v1/job-postings/{id} (detalle)
   - PUT /api/v1/job-postings/{id} (actualizar)
   - PATCH /api/v1/job-postings/{id}/status (cambiar estado)
   - DELETE /api/v1/job-postings/{id} (soft delete)
2. Validación de permisos: solo el creador o admins pueden editar/eliminar
3. Manejo de errores con @ExceptionHandler (404 Not Found, 403 Forbidden, 400 Bad Request)
4. Documentación OpenAPI/Swagger
5. Integration tests con MockMvc (mínimo 85% coverage de controller)

**Criterios de Aceptación:**
- Todos los endpoints responden correctamente (200, 201, 204)
- Listado soporta paginación (page, size, sort) y filtros (status, department)
- Validación de permisos funciona: user A no puede editar oferta de user B
- Errores devuelven formato consistente con detalles útiles
- Swagger UI lista todos los endpoints con ejemplos

**Estimación:** 5 Story Points

**Dependencias:** BACK-002

**Asignado a:** Backend Dev #2

---

## BACK-004: Servicio de Negocio y Máquina de Estados

**Título:** Implementar JobPostingService con lógica de negocio y estados

**Descripción:**
Crear capa de servicio con lógica de negocio para transiciones de estado, validaciones complejas, y coordinación con otros servicios (IA, notificaciones).

**Tareas:**
1. Crear `JobPostingService` con métodos de negocio
2. Implementar máquina de estados para job_posting:
   - draft → pending_approval (si require approval)
   - draft → active (si publicación directa)
   - pending_approval → approved → active
   - pending_approval → rejected → draft (con comentarios)
   - active → closed
3. Validaciones de negocio:
   - No permitir publicar oferta sin description y requirements
   - Validar que salary_min < salary_max
   - Solo ofertas en estado "active" pueden recibir aplicaciones
4. Integración con servicio de auditoría (registrar cambios en audit table)
5. Unit tests exhaustivos (90% coverage de service)

**Criterios de Aceptación:**
- Máquina de estados previene transiciones inválidas (ej: draft → closed directamente)
- Validaciones de negocio lanzan excepciones con mensajes claros
- Cambios de estado se registran en tabla de auditoría con timestamp y user
- Service es testeable con mocks de repository

**Estimación:** 8 Story Points

**Dependencias:** BACK-002

**Riesgos:**
- Máquina de estados puede volverse compleja si se agregan más estados - usar library como Spring State Machine si crece

**Asignado a:** Backend Dev #1

---

## AI-005: Integración con Servicio LLM

**Título:** Implementar servicio de generación de descripciones con IA

**Descripción:**
Crear servicio que integra con OpenAI/Anthropic API para generar descripciones de ofertas optimizadas basándose en título y requisitos básicos.

**Tareas:**
1. Crear `AIDescriptionService` con métodos:
   - generateJobDescription(title, requirements, companyInfo) → string
   - regenerateWithFeedback(previousDescription, feedback) → string
2. Implementar cliente HTTP para OpenAI/Anthropic API (usar RestTemplate o WebClient)
3. Diseñar prompts optimizados:
   - System prompt que define rol (experto en writing de job descriptions)
   - User prompt con template: "Genera una descripción atractiva para el puesto de {title}. Requisitos: {requirements}. Empresa: {companyInfo}"
4. Manejo de errores: timeout, rate limit (429), API down (503)
5. Circuit breaker con Resilience4j (fallback a descripción genérica)
6. Logging de requests/responses para debugging
7. Unit tests con WireMock para simular respuestas de API

**Criterios de Aceptación:**
- Descripción generada tiene entre 300-600 palabras
- Incluye secciones: Resumen del rol, Responsabilidades clave, Requisitos técnicos, Skills deseables, Beneficios
- Timeout configurado en 10 segundos con retry (1 intento adicional)
- Si API falla 3 veces seguidas, circuit breaker abre y usa fallback por 1 minuto
- Response time P95 <5 segundos

**Estimación:** 8 Story Points

**Dependencias:** Ninguna (puede desarrollarse en paralelo)

**Riesgos:**
- **Alto:** Rate limits de OpenAI (3 RPM en tier free) - necesita plan pagado para producción
- **Alto:** Costo por request (~$0.01 por descripción con GPT-4) - implementar caching

**Asignado a:** ML Engineer

---

## AI-006: Optimización de Prompts y Cache

**Título:** Implementar caching de respuestas y A/B testing de prompts

**Descripción:**
Optimizar el servicio de IA con caching de descripciones generadas y sistema de A/B testing para evaluar diferentes prompts.

**Tareas:**
1. Implementar cache con Redis:
   - Key: hash(title + requirements + companyInfo)
   - Value: descripción generada + metadata (timestamp, model usado)
   - TTL: 30 días
2. Implementar feature flag para múltiples prompts (prompt A, B, C)
3. Logging de métricas: cual prompt usó, tiempo de generación, si fue cache hit/miss
4. Endpoint de admin para invalidar cache si calidad es mala
5. Tests de performance: cache debe mejorar response time en 95%

**Criterios de Aceptación:**
- Cache hit rate >80% después de 1 semana en producción
- Descripciones cacheadas son indistinguibles de frescas para el usuario
- Feature flags permiten cambiar prompt sin deployment
- Costo de API de IA se reduce 80% gracias a caching

**Estimación:** 5 Story Points

**Dependencias:** AI-005

**Asignado a:** ML Engineer

---

## FRONT-007: Formulario de Creación de Oferta

**Título:** Implementar formulario multi-step para crear oferta

**Descripción:**
Crear UI de formulario con React Hook Form para capturar todos los campos de la oferta en 3 pasos: Información Básica, Descripción y Requisitos, Revisión.

**Tareas:**
1. Crear componente `JobPostingForm` con 3 steps:
   - Step 1: Título, Departamento, Ubicación, Tipo de Empleo, Rango Salarial
   - Step 2: Descripción (editor WYSIWYG), Requisitos, Responsabilidades, Beneficios
   - Step 3: Preview + Confirmación
2. Integrar React Hook Form con validaciones (yup schema)
3. Integrar con TipTap para editor WYSIWYG (FRONT-008)
4. UI para asistencia de IA: botón "Generar con IA" que llama al servicio (FRONT-009)
5. Stepper visual mostrando progreso (1/3, 2/3, 3/3)
6. Auto-save cada 30 segundos en localStorage (draft recovery)
7. Responsive design (mobile-friendly)

**Criterios de Aceptación:**
- Formulario valida campos obligatorios antes de permitir avanzar al siguiente step
- Auto-save funciona: si el usuario cierra el browser y vuelve, el draft se recupera
- Experiencia fluida: transiciones entre steps son suaves (<100ms)
- Accesibilidad: form labels correctos, keyboard navigation funciona
- Unit tests con React Testing Library (80% coverage)

**Estimación:** 3 Story Points

**Dependencias:** FRONT-008 (editor), FRONT-009 (asistencia IA)

**Asignado a:** Frontend Dev #1

---

## FRONT-008: Editor WYSIWYG

**Título:** Integrar TipTap como editor de texto enriquecido

**Descripción:**
Implementar editor WYSIWYG con TipTap para el campo de descripción, soportando formato básico y preview HTML.

**Tareas:**
1. Instalar TipTap y extensiones necesarias: StarterKit, Link, BulletList, OrderedList
2. Crear componente `RichTextEditor` wrapper de TipTap
3. Toolbar con botones: Bold, Italic, Underline, Heading (H1-H3), Bullet List, Numbered List, Link, Undo, Redo
4. Preview mode que renderiza HTML con estilos consistentes
5. Sanitización de HTML para prevenir XSS (usar DOMPurify)
6. Character counter (mostrar: 450/600 palabras sugeridas)
7. Integración con React Hook Form (controled component)

**Criterios de Aceptación:**
- Editor soporta copy-paste desde Word/Google Docs sin romper formato
- HTML generado es limpio y semántico (<p>, <ul>, <h2>, no inline styles)
- Sanitización previene inyección de <script> tags
- Editor es responsive y funciona en mobile
- Preview muestra exactamente lo que verá el candidato

**Estimación:** 5 Story Points

**Dependencias:** Ninguna (puede desarrollarse en paralelo)

**Asignado a:** Frontend Dev #2

---

## FRONT-009: UI de Asistencia de IA

**Título:** Implementar interfaz de generación de descripción con IA

**Descripción:**
Crear UI para que el usuario solicite al sistema generar la descripción automáticamente con IA, mostrar loading state, y permitir regenerar si no le gusta el resultado.

**Tareas:**
1. Agregar botón "Generar Descripción con IA" en Step 2 del formulario
2. Modal que solicita inputs mínimos para IA (título y 3-5 requisitos clave en bullet points)
3. Llamada al endpoint POST /api/v1/ai/generate-description
4. Loading state con skeleton y mensaje "Generando descripción optimizada..." (mostrar tiempo estimado: ~5 segundos)
5. Mostrar descripción generada en el editor con opción de "Aceptar" o "Regenerar"
6. Opción de proporcionar feedback: "Más técnico", "Más casual", "Agregar más beneficios"
7. Manejo de errores: si API falla, mostrar mensaje amigable y permitir retry

**Criterios de Aceptación:**
- Loading state no bloquea el resto de la UI (asíncrono)
- Usuario puede editar libremente la descripción generada antes de aceptar
- Feedback se envía al backend y mejora la siguiente generación
- Si hay error, usuario puede continuar llenando manualmente
- Animación suave cuando la descripción aparece en el editor

**Estimación:** 5 Story Points

**Dependencias:** AI-005 (backend de IA)

**Asignado a:** Frontend Dev #1

---

## FRONT-010: Vista de Listado y Detalle

**Título:** Crear páginas de listado y detalle de ofertas

**Descripción:**
Implementar vista de listado de ofertas (tabla con paginación y filtros) y vista de detalle (read-only) con opciones de editar/publicar.

**Tareas:**
1. Página `/job-postings` con tabla que lista ofertas:
   - Columnas: Título, Departamento, Status (badge con color), Fecha Creación, Acciones
   - Paginación (10, 25, 50 items por página)
   - Filtros: Status (dropdown), Departamento (dropdown), Búsqueda por título
   - Sorting: clic en header de columna para ordenar
2. Página `/job-postings/:id` con vista de detalle:
   - Mostrar todos los campos en formato legible
   - Botón "Editar" (si el usuario es el creador)
   - Botón "Publicar" (si status es draft/approved)
   - Botón "Cerrar Oferta" (si status es active)
3. Integrar con API de backend (React Query para data fetching)
4. Loading skeletons mientras carga data
5. Empty states: "No hay ofertas creadas. ¡Crea tu primera oferta!"

**Criterios de Aceptación:**
- Listado carga en <1 segundo con 100 ofertas
- Filtros actualizan la tabla instantáneamente (client-side si dataset es pequeño, server-side si es grande)
- Paginación funciona correctamente (no se pierden filtros al cambiar de página)
- Detalle muestra HTML de descripción correctamente renderizado
- Permisos: usuario solo ve botón "Editar" en sus propias ofertas

**Estimación:** 3 Story Points

**Dependencias:** BACK-003 (API REST)

**Asignado a:** Frontend Dev #2

---

## TEST-011: Tests de Integración

**Título:** Suite de tests de integración end-to-end para API

**Descripción:**
Crear tests de integración que validen el flujo completo de crear oferta, generar descripción con IA, actualizar, cambiar estado, y eliminar.

**Tareas:**
1. Setup de test environment con Testcontainers (PostgreSQL, Redis)
2. Tests de happy path:
   - POST crear oferta → GET listar (debe aparecer) → GET detalle (validar campos) → PUT actualizar → DELETE
3. Tests de edge cases:
   - Crear oferta con campos inválidos (esperar 400 Bad Request)
   - Intentar editar oferta de otro usuario (esperar 403 Forbidden)
   - Intentar publicar oferta sin description (esperar 400)
4. Tests de integración con servicio de IA:
   - Mock de OpenAI API con WireMock
   - Validar que descripción generada se guarda correctamente
   - Validar que timeout y circuit breaker funcionan
5. Tests de performance:
   - Crear 1000 ofertas y medir tiempo de listado (debe ser <2 segundos)

**Criterios de Aceptación:**
- Suite de tests ejecuta en <2 minutos
- Coverage de integration tests: 85% de código de service y controller
- Tests fallan si algún comportamiento esperado no se cumple
- CI/CD ejecuta tests automáticamente en cada PR

**Estimación:** 8 Story Points

**Dependencias:** BACK-004, AI-005

**Asignado a:** QA + Backend Dev #1

---

## TEST-012: Tests E2E con Playwright/Cypress

**Título:** Tests E2E del flujo de usuario completo

**Descripción:**
Crear tests end-to-end que simulan al usuario real: login, crear oferta con IA, editar, publicar, verificar que aparece en listado.

**Tareas:**
1. Setup de Playwright/Cypress con configuración de test environment
2. Tests E2E principales:
   - Test 1: Crear oferta manualmente (llenar formulario paso a paso, guardar, verificar en listado)
   - Test 2: Crear oferta con asistencia de IA (clic en botón IA, esperar generación, aceptar, publicar)
   - Test 3: Editar oferta existente (cambiar título y descripción, guardar, verificar cambios)
   - Test 4: Cambiar estado de oferta (draft → active → closed, validar badges)
3. Tests de regresión visual con Percy/Chromatic (screenshots)
4. Tests de accesibilidad con axe-core
5. Tests en múltiples browsers (Chrome, Firefox, Safari)

**Criterios de Aceptación:**
- Tests E2E ejecutan en <5 minutos
- Detectan correctamente bugs de UI (ej: botón deshabilitado cuando no debería)
- Screenshots de regresión visual detectan cambios no intencionados
- Tests de accesibilidad pasan 100% (no errores críticos)
- Suite es estable (no flaky tests)

**Estimación:** 5 Story Points

**Dependencias:** FRONT-007, FRONT-009, FRONT-010

**Asignado a:** QA

---

## DEVOPS-013: Secrets Management y Rate Limiting

**Título:** Configurar gestión de secrets y rate limiting para APIs externas

**Descripción:**
Implementar gestión segura de API keys (OpenAI/Anthropic) y rate limiting para proteger contra abuso y controlar costos.

**Tareas:**
1. Configurar AWS Secrets Manager / HashiCorp Vault para almacenar API keys
2. Actualizar aplicación para leer secrets desde Secrets Manager (no hardcoded)
3. Implementar rate limiting con Bucket4j:
   - Límite global: 100 requests/minuto a API de IA
   - Límite por usuario: 10 requests/hora para generación de descripciones
4. Configurar alertas en CloudWatch/DataDog si rate limit se alcanza frecuentemente
5. Documentación de cómo rotar secrets sin downtime
6. Tests de seguridad: verificar que secrets no están expuestos en logs ni errores

**Criterios de Aceptación:**
- API keys no están hardcoded en código ni archivos de configuración
- Secrets se pueden rotar sin redeploy de aplicación
- Rate limiting previene que un usuario abuse del servicio de IA
- Alertas se disparan si el 80% del rate limit se alcanza
- Logs no exponen secrets ni API keys

**Estimación:** 5 Story Points

**Dependencias:** AI-005

**Asignado a:** Backend Dev #2 + DevOps

---

## Resumen de Tickets

| ID | Título | Área | SP | Asignado | Dependencias |
|----|--------|------|----|-----------|----|
| DATA-001 | Migración BD tabla job_posting | Data | 3 | Backend #1 | - |
| BACK-002 | Entidad JPA + DTOs | Backend | 5 | Backend #1 | DATA-001 |
| BACK-003 | API REST CRUD Ofertas | Backend | 5 | Backend #2 | BACK-002 |
| BACK-004 | Servicio de negocio con máquina de estados | Backend | 8 | Backend #1 | BACK-002 |
| AI-005 | Integración servicio LLM para generación descripción | AI | 8 | ML Engineer | - |
| AI-006 | Optimización de prompts y cache de respuestas | AI | 5 | ML Engineer | AI-005 |
| FRONT-007 | Formulario creación oferta | Frontend | 3 | Frontend #1 | FRONT-008, FRONT-009 |
| FRONT-008 | Editor TipTap WYSIWYG | Frontend | 5 | Frontend #2 | - |
| FRONT-009 | UI asistencia IA | Frontend | 5 | Frontend #1 | AI-005 |
| FRONT-010 | Vista listado + detalle ofertas | Frontend | 3 | Frontend #2 | BACK-003 |
| TEST-011 | Tests de integración | Testing | 8 | QA + Backend #1 | BACK-004, AI-005 |
| TEST-012 | Tests E2E Playwright/Cypress | Testing | 5 | QA | FRONT-007, FRONT-009, FRONT-010 |
| DEVOPS-013 | Secrets management + rate limiting | DevOps | 5 | Backend #2 + DevOps | AI-005 |

**Total:** 68 Story Points

---

# PARTE 5: Estimación de Esfuerzo

## 5.1 Planning Poker (Escala Fibonacci)

### Contexto de Estimación

**Método:** Planning Poker con escala Fibonacci (1, 2, 3, 5, 8, 13, 21)

**Equipo Participante:**
- Product Owner (facilitador)
- 2 Backend Developers
- 2 Frontend Developers
- 1 ML Engineer
- 1 QA Engineer

**Referencia (Definition of 1 SP):**
"Crear un endpoint REST GET simple que lee de base de datos y devuelve JSON, con test unitario básico" = **1 Story Point**

---

### Sesión de Planning Poker por Ticket

#### DATA-001: Migración BD (Consenso: 3 SP)

**Primera Ronda:**
- Backend #1: 3
- Backend #2: 2
- Frontend #1: 5 (no familiarizado con migraciones)
- Frontend #2: 3
- ML Engineer: 3
- QA: 3

**Discusión:**
- Backend #2 argumenta 2: "Es solo una tabla, 15 campos, 30 minutos"
- Backend #1 argumenta 3: "Hay que diseñar bien los índices GIN para full-text, testear performance, y crear tabla de auditoría. 3 es razonable"
- Frontend #1 revisa: "No tenía claro que incluía auditoría, cambio a 3"

**Consenso:** **3 SP**

---

#### BACK-002: Entidad JPA + DTOs (Consenso: 5 SP)

**Primera Ronda:**
- Backend #1: 5
- Backend #2: 5
- Frontend #1: 3 (subestima complejidad de mapeo JSONB)
- Frontend #2: 3
- ML Engineer: 5
- QA: 5

**Discusión:**
- Backend #1: "Los DTOs son 3 (Create, Update, Response), el mapper con MapStruct necesita custom logic para JSONB, y los unit tests del repository son extensos. 5 es correcto"
- Frontend #1: "Entendido, cambio a 5"

**Consenso:** **5 SP**

---

#### BACK-003: API REST CRUD (Consenso: 5 SP)

**Primera Ronda:** Todos votaron 5 inmediatamente.

**Justificación:**
- 6 endpoints (CRUD completo)
- Validación de permisos
- Paginación y filtros
- Exception handling
- Swagger docs
- Integration tests

**Consenso:** **5 SP** (no debate necesario)

---

#### BACK-004: Servicio de Negocio + Estado (Consenso: 8 SP)

**Primera Ronda:**
- Backend #1: 8
- Backend #2: 13 (preocupado por complejidad de máquina de estados)
- Frontend #1: 5
- Frontend #2: 5
- ML Engineer: 8
- QA: 8

**Discusión:**
- Backend #2: "Las máquinas de estado son complejas, propensas a bugs, y necesitan tests exhaustivos. Voto 13"
- Backend #1: "Si usamos una library como Spring State Machine, la complejidad baja. Sin library, sería 13. Con library, 8"
- PO: "¿Usaremos library?"
- Backend #1: "Sí, para este caso vale la pena"
- Backend #2: "Ok, cambio a 8"
- Frontend #1 y #2: "No teníamos contexto de lo complejo que es esto, cambiamos a 8"

**Consenso:** **8 SP**

---

#### AI-005: Integración LLM (Consenso: 8 SP)

**Primera Ronda:**
- Backend #1: 5
- Backend #2: 5
- Frontend #1: 8
- Frontend #2: 8
- ML Engineer: 8 (expert opinion)
- QA: 8

**Discusión:**
- ML Engineer: "La integración HTTP es simple (3 SP), pero el diseño de prompts efectivos requiere iteración (2-3 días), el circuit breaker con Resilience4j añade complejidad (2 SP), y los tests con WireMock son elaborados (1 SP). Total: 8"
- Backend #1 y #2: "No habíamos considerado la iteración de prompts, cambio a 8"

**Consenso:** **8 SP** (el experto en ML tiene mayor peso aquí)

---

#### AI-006: Optimización + Cache (Consenso: 5 SP)

**Primera Ronda:**
- Backend #1: 5
- Backend #2: 3 (piensa que Redis es rápido de implementar)
- Frontend #1: 5
- Frontend #2: 5
- ML Engineer: 5
- QA: 5

**Discusión:**
- Backend #2: "Redis con Spring Cache es solo anotaciones, ¿por qué 5?"
- ML Engineer: "El caching es simple, pero el A/B testing de prompts con feature flags requiere configuración de LaunchDarkly/Unleash, logging de métricas para análisis, y un endpoint de admin para invalidación. 5 es justo"
- Backend #2: "Tienes razón, cambio a 5"

**Consenso:** **5 SP**

---

#### FRONT-007: Formulario Creación (Consenso: 3 SP)

**Primera Ronda:**
- Backend #1: 5
- Backend #2: 5
- Frontend #1: 3 (expert opinion)
- Frontend #2: 3 (expert opinion)
- ML Engineer: 5
- QA: 3

**Discusión:**
- Frontend #1: "El formulario en sí es 2 SP (React Hook Form con yup es rápido), el stepper visual es 0.5 SP (library react-step-wizard), el auto-save en localStorage es 0.5 SP. Total: 3"
- Backend #1: "No tenía contexto de que hay libraries para stepper, pensé que había que hacer custom. Cambio a 3"
- Otros backends y ML Engineer cambian a 3

**Consenso:** **3 SP**

---

#### FRONT-008: Editor WYSIWYG (Consenso: 5 SP)

**Primera Ronda:**
- Backend #1: 8
- Backend #2: 8
- Frontend #1: 5 (expert opinion)
- Frontend #2: 5 (expert opinion)
- ML Engineer: 5
- QA: 5

**Discusión:**
- Frontend #2: "TipTap con extensiones básicas es rápido (2 SP), pero hacer que funcione bien con copy-paste de Word/Google Docs, sanitización de HTML con DOMPurify, y que el preview sea pixel-perfect añade complejidad (3 SP adicionales). 5 es correcto"
- Backend #1: "Pensé que integrar un editor rich text era muy complejo, pero si TipTap hace el trabajo pesado, 5 tiene sentido. Cambio"

**Consenso:** **5 SP**

---

#### FRONT-009: UI Asistencia IA (Consenso: 5 SP)

**Primera Ronda:**
- Backend #1: 3
- Backend #2: 3
- Frontend #1: 5 (expert opinion)
- Frontend #2: 5 (expert opinion)
- ML Engineer: 5
- QA: 5

**Discusión:**
- Frontend #1: "El modal es simple (1 SP), pero la UI de loading con skeleton animado, la integración con el editor (insertar texto generado), el flujo de feedback ('Más técnico', 'Más casual'), y el manejo de errores suman. 5 es apropiado"
- Backends cambian a 5

**Consenso:** **5 SP**

---

#### FRONT-010: Listado + Detalle (Consenso: 3 SP)

**Primera Ronda:** Todos votaron 3.

**Justificación:**
- Listado con tabla es 2 SP (library react-table)
- Vista de detalle es 1 SP (layout simple)
- Paginación y filtros son features estándar de react-table

**Consenso:** **3 SP**

---

#### TEST-011: Tests Integración (Consenso: 8 SP)

**Primera Ronda:**
- Backend #1: 8
- Backend #2: 5
- Frontend #1: 8
- Frontend #2: 8
- ML Engineer: 8
- QA: 13 (preocupado por coverage extensivo)

**Discusión:**
- QA: "Para 85% coverage de service y controller, necesitamos muchos test cases (happy path, edge cases, performance). Voto 13"
- Backend #1: "85% coverage es ambicioso pero factible con Testcontainers (setup rápido) y buen uso de mocks. Con dedicación full-time de QA + 1 backend dev, 8 SP (2 días) es suficiente"
- QA: "Si tengo ayuda de un backend dev, ok. Cambio a 8"
- Backend #2: "No había considerado la complejidad del setup con Testcontainers + WireMock, cambio a 8"

**Consenso:** **8 SP**

---

#### TEST-012: Tests E2E (Consenso: 5 SP)

**Primera Ronda:**
- Backend #1: 3
- Backend #2: 3
- Frontend #1: 5
- Frontend #2: 5
- ML Engineer: 5
- QA: 5 (expert opinion)

**Discusión:**
- QA: "Los E2E con Playwright son rápidos de escribir (3 SP), pero la configuración de visual regression con Percy y tests de accesibilidad con axe-core añaden 2 SP. Total: 5"
- Backends cambian a 5

**Consenso:** **5 SP**

---

#### DEVOPS-013: Secrets + Rate Limiting (Consenso: 5 SP)

**Primera Ronda:**
- Backend #1: 5
- Backend #2: 5
- Frontend #1: 3
- Frontend #2: 3
- ML Engineer: 5
- QA: 5

**Discusión:**
- Backend #2: "AWS Secrets Manager es fácil de integrar (2 SP), Bucket4j para rate limiting es 2 SP, y las alertas en CloudWatch son 1 SP. 5 es correcto"
- Frontends no tenían contexto de DevOps, aceptan la estimación de los backends

**Consenso:** **5 SP**

---

### Resumen Final de Planning Poker

| Ticket | Estimación Final | Nivel de Confianza |
|--------|------------------|--------------------|
| DATA-001 | 3 SP | Alto (consenso rápido) |
| BACK-002 | 5 SP | Alto |
| BACK-003 | 5 SP | Muy Alto (unanimidad inmediata) |
| BACK-004 | 8 SP | Medio (debate sobre complejidad de estado) |
| AI-005 | 8 SP | Alto (ML expert lideró) |
| AI-006 | 5 SP | Alto |
| FRONT-007 | 3 SP | Alto (FE experts lideraron) |
| FRONT-008 | 5 SP | Alto |
| FRONT-009 | 5 SP | Alto |
| FRONT-010 | 3 SP | Muy Alto (unanimidad) |
| TEST-011 | 8 SP | Medio (QA inicialmente preocupado) |
| TEST-012 | 5 SP | Alto |
| DEVOPS-013 | 5 SP | Alto |

**Total: 68 Story Points**

---

## 5.2 Análisis PERT (Program Evaluation and Review Technique)

### Introducción al Método PERT

PERT utiliza estimaciones de tres puntos para cada tarea:
- **Optimista (O)**: Mejor escenario, todo sale perfecto
- **Probable (M)**: Escenario más realista
- **Pesimista (P)**: Peor escenario con problemas

**Fórmula:** `Estimación PERT = (O + 4M + P) / 6`

Esta estimación es más robusta que Planning Poker porque considera explícitamente el riesgo.

---

### Estimaciones PERT por Ticket

| Ticket | Optimista (O) | Probable (M) | Pesimista (P) | PERT | Contingencia |
|--------|---------------|--------------|---------------|------|--------------|
| DATA-001 | 2 SP | 3 SP | 5 SP (migraciones fallan en staging) | 3.2 SP | +0.2 SP |
| BACK-002 | 4 SP | 5 SP | 8 SP (mappers JSONB complejos) | 5.3 SP | +0.3 SP |
| BACK-003 | 4 SP | 5 SP | 8 SP (permisos más complejos) | 5.3 SP | +0.3 SP |
| BACK-004 | 5 SP | 8 SP | 13 SP (máquina de estados buggy) | 8.3 SP | +0.3 SP |
| AI-005 | 5 SP | 8 SP | 13 SP (prompts requieren mucha iteración) | 8.3 SP | +0.3 SP |
| AI-006 | 3 SP | 5 SP | 8 SP (feature flags complejos) | 5.2 SP | +0.2 SP |
| FRONT-007 | 2 SP | 3 SP | 5 SP (auto-save con bugs) | 3.2 SP | +0.2 SP |
| FRONT-008 | 3 SP | 5 SP | 8 SP (copy-paste de Word rompe todo) | 5.2 SP | +0.2 SP |
| FRONT-009 | 3 SP | 5 SP | 8 SP (integración con editor compleja) | 5.2 SP | +0.2 SP |
| FRONT-010 | 2 SP | 3 SP | 5 SP (permisos en UI son tricky) | 3.2 SP | +0.2 SP |
| TEST-011 | 5 SP | 8 SP | 13 SP (Testcontainers inestables) | 8.3 SP | +0.3 SP |
| TEST-012 | 3 SP | 5 SP | 8 SP (flaky tests en CI) | 5.2 SP | +0.2 SP |
| DEVOPS-013 | 3 SP | 5 SP | 8 SP (secrets rotation rompe algo) | 5.2 SP | +0.2 SP |

**Total PERT:** 70.7 SP ≈ **71 SP**

**Contingencia Total:** +3 SP

**Estimación Ajustada por Riesgo:** **74 SP**

---

### Análisis de Riesgos Principales

#### Tickets de Alto Riesgo (P ≥ 13 SP)

**BACK-004: Máquina de Estados**
- **Riesgo:** Las transiciones de estado son propensas a bugs lógicos
- **Mitigación:** Usar Spring State Machine library + tests exhaustivos de transiciones inválidas
- **Contingencia:** +2 SP si hay que refactorizar por bugs en producción

**AI-005: Integración LLM**
- **Riesgo:** Los prompts pueden no generar descripciones de calidad aceptable, requiriendo muchas iteraciones
- **Mitigación:** Empezar con prompts de referencia de OpenAI Cookbook + A/B testing temprano
- **Contingencia:** +2 SP si hay que fine-tunar modelos o cambiar de OpenAI a Anthropic Claude

**TEST-011: Tests de Integración**
- **Riesgo:** Testcontainers puede ser inestable en CI/CD, causando flaky tests
- **Mitigación:** Usar imágenes Docker específicas (no "latest"), aumentar timeouts, cleanup agresivo
- **Contingencia:** +1 SP si hay que debuggear problemas de CI

---

### Distribución de Trabajo por Sprint

Asumiendo **velocity de 35 SP por sprint** (equipo de 7 personas):

**Sprint 1 (Semanas 1-2):**
- DATA-001 (3 SP)
- BACK-002 (5 SP)
- BACK-003 (5 SP)
- AI-005 (8 SP) - inicia en paralelo
- FRONT-008 (5 SP) - inicia en paralelo
- **Total Sprint 1:** 26 SP

**Sprint 2 (Semanas 3-4):**
- BACK-004 (8 SP) - completar
- AI-005 (8 SP) - completar si no terminó
- AI-006 (5 SP)
- FRONT-007 (3 SP)
- FRONT-009 (5 SP)
- FRONT-010 (3 SP)
- **Total Sprint 2:** 32 SP

**Sprint 3 (Semanas 5-6 - si es necesario):**
- TEST-011 (8 SP)
- TEST-012 (5 SP)
- DEVOPS-013 (5 SP)
- Buffer para contingencias (6 SP disponibles)
- **Total Sprint 3:** 18 SP + 6 SP buffer

---

### Estimación Final de Tiempo

**Con Análisis PERT:**
- **Estimación base (Planning Poker):** 68 SP
- **Estimación PERT (con probabilidades):** 71 SP
- **Con contingencia de riesgo:** 74 SP
- **Velocity del equipo:** 35 SP/sprint

**Duración:**
- **Optimista:** 68 SP / 35 SP/sprint = **1.9 sprints** (~4 semanas)
- **Probable:** 71 SP / 35 SP/sprint = **2.0 sprints** (4 semanas)
- **Con contingencia:** 74 SP / 35 SP/sprint = **2.1 sprints** (~4.5 semanas)

**Recomendación:** Planificar **2 sprints completos (4 semanas)** para US-001, con buffer de medio sprint para contingencias.

---

## Conclusiones de Estimación

1. **Planning Poker arrojó 68 SP**: Buena estimación base con consenso del equipo
2. **PERT añadió +3 SP de contingencia**: Reconoce riesgos en máquina de estados, prompts de IA, y tests
3. **Los tickets de IA (AI-005, AI-006) suman 13 SP**: El 19% del esfuerzo está en la integración con LLM
4. **Los tickets de testing (TEST-011, TEST-012) suman 13 SP**: Otro 19% en testing, lo cual es saludable
5. **Riesgo principal**: La precisión de los prompts de IA puede requerir iteración adicional

**Estrategia de Mitigación:**
- Empezar AI-005 en Sprint 1 (en paralelo con backend) para tener tiempo de iterar prompts
- Reservar 3-5 SP de buffer en Sprint 2 para contingencias
- Si US-001 se retrasa, mover TEST-012 (E2E) a Sprint 3 sin bloquear funcionalidad core

---

# Conclusiones y Recomendaciones

## Resumen Ejecutivo

Este ejercicio de Product Management para el MVP de **LTI ATS** generó:
- **10 User Stories** detalladas con criterios de aceptación completos
- **4 metodologías de priorización** aplicadas y comparadas
- **Descomposición técnica de US-001** en 13 tickets con 68 SP totales
- **Estimaciones con Planning Poker y PERT** validadas por el equipo

---

## Hallazgos Clave

### 1. Convergencia de Métodos de Priorización

**Todos los 4 métodos (MoSCoW, RICE, Kano, Story Mapping) convergieron en las mismas 6 User Stories para el MVP:**
- US-001: Crear Oferta
- US-002: Publicar Oferta
- US-003: Parsear CVs con IA
- US-004: Pipeline Kanban
- US-005: Rankear con IA
- US-006: Perfil Candidato

Esta convergencia valida fuertemente la estrategia de priorización y da confianza en que estas son las funcionalidades correctas para el MVP.

---

### 2. Story Mapping es el Método Más Efectivo

**Story Mapping obtuvo 47/50 puntos** en la evaluación cuantitativa porque:
- Visualiza claramente el journey end-to-end del usuario
- Considera dependencias implícitamente (secuencia de activities)
- Identifica el "walking skeleton" de forma natural
- Es excelente para comunicación con stakeholders no técnicos

**Recomendación:** Usar Story Mapping como método principal, complementado con Kano para identificar diferenciadores (Excitement features).

---

### 3. Las Capacidades de IA son el Diferenciador Crítico

**US-003 (Parsing de CVs) y US-005 (Ranking con IA)** fueron identificadas por todos los métodos como:
- Críticas para la propuesta de valor única del producto (vs competidores)
- Alto impacto en satisfacción del usuario (Kano: Excitement features)
- Alto riesgo técnico pero máximo valor de negocio

**Implicación:** Invertir los recursos de ML Engineer prioritariamente en estas dos US, incluso si toman más tiempo del estimado. Son el core del producto.

---

### 4. US-001 es Compleja pero Manejable

La descomposición de US-001 en 13 tickets técnicos revela:
- **Complejidad real:** 68-74 SP (según Planning Poker y PERT)
- **Duración estimada:** 2 sprints (4 semanas)
- **Riesgos principales:**
  - Precisión de prompts de IA (requiere iteración)
  - Máquina de estados de ofertas (propensa a bugs)
  - Tests de integración (Testcontainers puede ser inestable)

**Recomendación:** Empezar el trabajo de IA (AI-005) en Sprint 1 en paralelo con backend para tener tiempo de iterar prompts. Reservar buffer de 3-5 SP en Sprint 2.

---

### 5. El MVP es Alcanzable en 3 Sprints

**Walking Skeleton (6 US) estimado:**
- Sprint 1: US-001 (crear oferta) - inicia
- Sprint 2: US-001 (completar) + US-002 (publicar) + US-003 (parsear) - inicia + US-004 (Kanban)
- Sprint 3: US-003 (completar) + US-005 (ranking) + US-006 (perfil)

**Milestone crítico:** Al final de Sprint 3, el sistema debe permitir screenear candidatos automáticamente con IA. Este es el MVP viable mínimo para beta testing.

---

## Recomendaciones Finales

### Para el Product Owner

1. **Priorizar Walking Skeleton:** Enfocarse en las 6 US del MVP (Sprints 1-3) y resistir la tentación de agregar features adicionales hasta validar con usuarios reales.

2. **Validar Prompts de IA Temprano:** En Sprint 1, tan pronto AI-005 esté funcional, hacer sesiones de testing con reclutadores reales para validar la calidad de las descripciones generadas.

3. **Comunicar Milestone de Sprint 3:** Alinear a stakeholders en que Sprint 3 es un hito crítico donde el producto debe estar funcionalmente completo end-to-end, incluso si falta pulido.

### Para el Equipo de Desarrollo

1. **Paralelizar Trabajo:** En Sprint 1, iniciar BACK-002/003, AI-005, y FRONT-008 en paralelo (no tienen dependencias). Esto maximiza el throughput.

2. **Invertir en Testing:** Los 13 SP dedicados a testing (TEST-011, TEST-012) son el 19% del esfuerzo total. No recortar esto - la calidad es crítica para un producto de IA donde la confianza del usuario es fundamental.

3. **Circuit Breakers desde el Inicio:** Implementar circuit breakers y fallbacks en AI-005 desde Sprint 1. Si OpenAI/Anthropic caen, el sistema debe degradarse gracefully (permitir descripción manual).

### Para Stakeholders

1. **El MVP No Incluye Todo:** US-007 (comunicaciones), US-008 (scheduling), US-009 (scorecards), US-010 (dashboard), y US-011 (aprobaciones) están fuera del walking skeleton. Pueden agregarse en Release 2 (Sprints 4-5) si el MVP valida la hipótesis.

2. **Las Capacidades de IA Requieren Iteración:** La precisión del parsing (US-003) y scoring (US-005) mejorará con el tiempo. El MVP tendrá versión funcional pero no perfecta. Planificar mejoras continuas post-lanzamiento.

3. **Story Mapping Facilita Alineación:** Usar el Story Map visual en presentaciones a stakeholders para comunicar la estrategia de releases. Es mucho más intuitivo que listas de User Stories.

---

## Siguientes Pasos

1. **Sprint Planning 1:** Refinar los tickets de DATA-001, BACK-002, BACK-003, AI-005, FRONT-008 con el equipo. Confirmar Definition of Done.

2. **Kickoff con Reclutadores:** Hacer una sesión de 1 hora con 2-3 reclutadores para validar el flujo del formulario de creación de oferta y la utilidad de la asistencia de IA.

3. **Setup de Infraestructura:** En paralelo a Sprint 1, DevOps debe preparar entornos (dev, staging), configurar Secrets Manager, y setup de CI/CD.

4. **Planning de Sprints 2-3:** Una vez Sprint 1 esté en marcha, hacer grooming de US-002, US-003, US-004, US-005, US-006 para confirmar priorización.

---

**Documento generado:** Diciembre 2025
**Autor:** Product Manager LTI ATS
**Versión:** 1.0 Final

---


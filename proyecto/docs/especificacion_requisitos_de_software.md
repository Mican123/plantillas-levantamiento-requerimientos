# ESPECIFICACIÓN DE REQUISITOS DE SOFTWARE
# MediPlus - Sistema de Gestión de Citas y Consulta Externa

## 1. Introducción

### 1.1 Propósito
Este documento proporciona una especificación completa de los requisitos para el Sistema MediPlus de Gestión de Consultas y Citas Médicas. Está dirigido a:

Equipo de desarrollo: Como base para el diseño, implementación y pruebas del sistema

Personal médico y administrativo: Para validar que las funcionalidades cubren sus necesidades operativas

Stakeholders y dirección: Para aprobación del alcance y planificación de recursos

Equipo de calidad: Para desarrollar casos de prueba y validación de criterios de aceptación
### 1.2 Alcance
El sistema permitirá la gestión integral del flujo de atención médica, desde la solicitud de cita hasta el registro de la consulta, incluyendo gestión de disponibilidad médica, recordatorios automáticos, historia clínica digital y generación de reportes estadísticos.

### 1.3 Personal involucrado
| Rol | Organización | Responsabilidad | Contacto |
|-----|-------------|-----------------|----------|
| Director Médico | Clínica MediPlus | Aprobación requisitos clínicos | dr.garcia@mediplus.com |
| Gerente Administrativo | Clínica MediPlus | Supervisión operativa | admin@mediplus.com |
| Jefe de TI | Clínica MediPlus | Implementación técnica | ti@mediplus.com |
| Director general| Clínica MediPlus | Toma de decisiones estratégicas | dr.hernan@mediplus.com |
| Director de Enfermería | Clínica MediPlus | Gestión del personal de enfermería | denfermeria@mediplus.com |
| Jefe de Recursos Humanos | Clínica MediPlus | Gestión del personal | rrhh@mediplus.com |


### 1.4 Referencias
| Término | Definición |
|---------|------------|
| EMR | Historia Clínica Electrónica (Electronic Medical Record) |
| HIPAA | Ley de Portabilidad y Seguro de Salud (EE.UU.) |
| LOPD | Ley Orgánica de Protección de Datos |
| UI | Interfaz de Usuario |
| UX | Experiencia de Usuario |
| API | Interfaz de Programación de Aplicaciones |
| SMS | Servicio de Mensajes Cortos |
| CRM | Sistema de Gestión de Relación con Pacientes |

#### 1.5 Referencias

1. **IEEE Std 830-1998** - IEEE Recommended Practice for Software Requirements Specifications
2. **LOPD** - Ley Orgánica 3/2018 de Protección de Datos Personales
3. **HIPAA** - Health Insurance Portability and Accountability Act
4. **Plantilla Base:** github.com/cfernandom/plantillas-levantamiento-requerimientos
5. **Documento de Alcance:** MEDI-ALE-001 v1.0
6. **Estándares Médicos:** Normativa SAN-2023-0456 de historiales clínicos

   #### 1.6 Resumen

El Sistema MediPlus es una plataforma web diseñada para optimizar la gestión de citas médicas en la clínica. Permitirá a los pacientes agendar citas en línea, a los médicos gestionar sus agendas, y al personal administrativo supervisar las operaciones. El sistema mejorará la eficiencia operativa reduciendo los tiempos de espera y los no-shows mediante recordatorios automáticos.


## 2. Descripción general

### 2.1 Perspectiva del producto
MediPlus es una aplicación web independiente que se integrará con el sistema de autenticación central de la URP. Reemplazará completamente el sistema actual de agendamiento en cuadernos físicos y historias clínicas en papel, proporcionando una plataforma unificada para todos los actores del centro de salud.

### 2.2 Funciones del producto
- Agendamiento online de citas 24/7 para pacientes
- Gestión de disponibilidad médica y horarios
- Sistema de recordatorios automáticos (email/SMS)
- Historia clínica electrónica integrada
- Registro de consultas médicas y tratamientos
- Control de inventario de farmacia
- Generación de reportes e indicadores en tiempo real
- Gestión de ausentismo y cancelaciones

### 2.3 Características de los usuarios
-->

| Característica | 	Usuario Tipo 1: Paciente | Usuario Tipo 2: Médico | Usuario Tipo 3: Recepcionista |
|----------------|-----------------------------------|-----------------------------------|-----------------------------------|
| **Descripción** | Persona que utiliza el sistema para gestionar sus citas médicas y consultas | Profesional de la salud que atiende pacientes y gestiona su agenda | Personal administrativo que coordina citas y atención al paciente |
| **Responsabilidades** | Agendar, cancelar y reprogramar citas; ver su historial de consultas | Gestionar disponibilidad; atender citas; revisar historiales de pacientes | Registrar pacientes; coordinar citas; manejar consultas telefónicas |
| **Nivel Técnico** | Bajo | Medio | Medio |
| **Experiencia en el Dominio** | Novato | Experto | Intermedio |
| **Frecuencia de Uso** | Ocasional | Diaria | Diaria |
| **Funciones Principales** | agendar citas/cancelar/reprogramar  |  Gestionar horarios de atención/Ver agenda de citas/Consultar historial de pacientes |   Registrar nuevos pacientes/Asignar citas manualmente/Gestionar cancelaciones |
| **Necesidades Especiales** | Interfaz intuitiva y guiada; recordatorios automáticos; acceso móvil | Acceso rápido y eficiente; integración con herramientas médicas; mínima interrupción | Vista consolidada de múltiples agendas; búsqueda rápida; multitarea|

<!
### 2.4 Restricciones
- **Legales**: Debe cumplir con Ley 1438/2011 (HCE), Ley 1581/2012 (protección de datos) y Resolución 1995/1999
- **Técnicas**: Integración con SSO universitario (OAuth 2.0), compatibilidad con navegadores Chrome 90+, Firefox 88+
- **Operacionales**: Tiempo de respuesta máximo de 3 segundos durante horas pico (200+ usuarios concurrentes)
- **Temporales**: MVP debe estar operativo en 5 meses
- **Presupuestales**: Presupuesto máximo de $62,000,000 COP
- **Seguridad**: Cifrado de datos sensibles y trazabilidad completa de accesos

### 2.5 Suposiciones y dependencias
- Se asume que los usuarios tienen acceso a internet y dispositivos digitales
- Depende del servicio de autenticación SSO de la URP
- Requiere base de datos PostgreSQL 13+ con capacidad de respaldo automático
- Supone que el personal médico recibirá 8 horas de capacitación obligatoria
- Depende de la infraestructura AWS existente en la universidad
- Asume disponibilidad de API para envío de SMS/email institucional

### 2.6 Requisitos futuros
- Módulo de telemedicina con videollamadas integradas
- App móvil nativa para iOS y Android
- Integración con laboratorio clínico para órdenes y resultados
- Sistema de receta médica electrónica con firma digital
- Módulo de inteligencia empresarial avanzado con predictivos
- Integración con EPS-U para facturación automática
- Sistema de triaje inteligente con algoritmos de priorización

## 3. Requisitos específicos

### 3.1 Requisitos funcionales

#### RF-001: Agendamiento Online de Citas Médicas
**ID:** RF-001  
**Nombre:** Agendamiento Online de Citas Médicas  
**Descripción:** El sistema debe permitir a los usuarios agendar citas médicas de forma autónoma a través de la plataforma web, seleccionando servicio, médico y horario disponible.  
**Prioridad:** Alta  
**Actor:** Usuario Paciente (Estudiante/Docente/Administrativo)  
**Precondiciones:**
- El usuario debe estar autenticado mediante SSO universitario
- El usuario debe tener estado activo en el sistema
- Debe haber disponibilidad médica configurada en el sistema

**Secuencia normal:**
1. El usuario accede al módulo de agendamiento online
2. El sistema muestra los servicios disponibles (Medicina General, Psicología, Odontología)
3. El usuario selecciona el servicio requerido
4. El sistema muestra los médicos disponibles para ese servicio
5. El usuario selecciona un médico
6. El sistema muestra los horarios disponibles para los próximos 7 días
7. El usuario selecciona fecha y horario deseado
8. El sistema valida que el horario sigue disponible
9. El usuario confirma la cita
10. El sistema registra la cita y asigna número de confirmación
11. El sistema envía correo de confirmación automática

**Postcondiciones:**
- La cita queda registrada con estado "Confirmada"
- El horario seleccionado se marca como ocupado
- Se genera recordatorio automático programado para 24 horas antes
- El usuario recibe comprobante digital de la cita

#### RF-002: Registro de Consulta Médica en Historia Clínica Electrónica
**ID:** RF-002  
**Nombre:** Registro de Consulta Médica en Historia Clínica Electrónica  
**Descripción:** El médico debe poder registrar toda la información de la consulta en la historia clínica electrónica del paciente, incluyendo anamnesis, examen físico, diagnósticos y tratamiento.  
**Prioridad:** Alta  
**Actor:** Médico General / Especialista  
**Precondiciones:**
- El médico debe haber iniciado sesión en el sistema
- El paciente debe tener cita confirmada para la fecha actual
- El paciente debe haber realizado check-in en recepción

**Secuencia normal:**
1. El médico accede a su agenda del día
2. El sistema muestra la lista de pacientes con citas programadas
3. El médico selecciona al paciente a atender
4. El sistema carga la historia clínica electrónica del paciente
5. El médico registra:
   - Motivo de consulta y anamnesis
   - Signos vitales (si no fueron tomados por enfermería)
   - Examen físico por sistemas
   - Impresión diagnóstica (con código CIE-10)
   - Tratamiento y medicamentos formulados
   - Plan de manejo y recomendaciones
6. El médico guarda el registro de la consulta
7. El sistema registra automáticamente fecha, hora y firma digital del médico
8. El sistema actualiza el estado de la cita a "Atendida"

**Postcondiciones:**
- La consulta queda registrada en la historia clínica electrónica
- Se genera alerta si se detectan alergias o contraindicaciones
- Los medicamentos formulados se envían automáticamente a farmacia
- El registro queda auditado y no editable (solo puede agregarse notas de evolución)

RF-009: Sistema de Recordatorios Automáticos Multicanal
Descripción: El sistema debe enviar recordatorios automáticos de citas a través de múltiples canales de comunicación
Prioridad: Alta
Criterios de Aceptación:

CA-009.1: Envío automático de email recordatorio 24 horas antes de la cita

CA-009.2: Envío de SMS recordatorio 2 horas antes de la cita

CA-009.3: Sistema registra confirmación de lectura cuando sea posible

CA-009.4: Configuración de horarios de envío para diferentes tipos de recordatorios

CA-009.5: Plantillas personalizables para mensajes de recordatorio

RF-010: Gestión de Cancelaciones y Reprogramaciones
Descripción: El sistema debe permitir la cancelación y reprogramación de citas por pacientes y administradores
Prioridad: Alta
Criterios de Aceptación:

CA-010.1: Paciente puede cancelar cita hasta 4 horas antes sin penalización

CA-010.2: Sistema sugiere horarios alternativos al reprogramar

CA-010.3: Administrativo puede cancelar o reprogramar citas con notificación al paciente

CA-010.4: Registro de motivo de cancelación para análisis estadístico

CA-010.5: Política de cancelaciones configurable por tipo de consulta

RF-011: Historial Básico de Consultas por Paciente
Descripción: El sistema debe mantener un historial básico de consultas realizadas por cada paciente
Prioridad: Media
Criterios de Aceptación:

CA-011.1: Registro de fecha, médico, especialidad y motivo de cada consulta

CA-011.2: Acceso al historial por parte del paciente en su portal

CA-011.3: Médico puede ver historial previo del paciente durante la consulta

CA-011.4: Búsqueda de consultas anteriores por fecha o especialidad

CA-011.5: Exportación básica del historial en formato PDF

RF-012: Sistema de Notificaciones en Tiempo Real
Descripción: El sistema debe proporcionar notificaciones en tiempo real para eventos importantes
Prioridad: Media
Criterios de Aceptación:

CA-012.1: Notificación inmediata al médico cuando se agenda nueva cita

CA-012.2: Alertas para citas canceladas o reprogramadas

CA-012.3: Notificaciones push en el dashboard administrativo para eventos críticos

CA-012.4: Sistema de notificaciones no intrusivo con diferentes niveles de prioridad

CA-012.5: Historial de notificaciones accesible para cada usuario

RF-013: Búsqueda Avanzada y Filtros
Descripción: El sistema debe proporcionar funcionalidades de búsqueda avanzada con múltiples filtros
Prioridad: Media
Criterios de Aceptación:

CA-013.1: Búsqueda de pacientes por nombre, teléfono o email

CA-013.2: Filtros de citas por fecha, médico, especialidad o estado

CA-013.3: Búsqueda de disponibilidad por rango de fechas y especialidad

CA-013.4: Guardado y reutilización de búsquedas frecuentes

CA-013.5: Exportación de resultados de búsqueda en formato Excel

RF-014: Dashboard de Métricas y Reportes
Descripción: El sistema debe generar reportes y mostrar métricas clave en un dashboard
Prioridad: Baja
Criterios de Aceptación:

CA-014.1: Dashboard con métricas de ocupación médica por especialidad

CA-014.2: Reporte de tasas de cancelación y no-shows

CA-014.3: Estadísticas de utilización de recursos por médico

CA-014.4: Generación de reportes personalizados por rango de fechas

CA-014.5: Exportación de reportes en formatos PDF y Excel

RF-015: Gestión de Especialidades y Servicios
Descripción: El sistema debe permitir la gestión de especialidades médicas y servicios ofrecidos
Prioridad: Media
Criterios de Aceptación:

CA-015.1: Creación y edición de especialidades médicas con descripción

CA-015.2: Asignación de médicos a múltiples especialidades

CA-015.3: Configuración de duración estándar de consulta por especialidad

CA-015.4: Gestión de servicios adicionales (exámenes, procedimientos)

CA-015.5: Asignación de precios y códigos a servicios (para futura facturación)

RF-016: Sistema de Backup y Recuperación
Descripción: El sistema debe realizar backups automáticos y permitir recuperación de datos
Prioridad: Alta
Criterios de Aceptación:

CA-016.1: Backup automático diario de la base de datos

CA-016.2: Backup incremental cada 4 horas durante horario comercial

CA-016.3: Sistema de recuperación ante desastres con RTO < 4 horas

CA-016.4: Verificación automática de integridad de backups

CA-016.5: Almacenamiento seguro de backups con encriptación

RF-017: Sistema de Listas de Espera Inteligentes
Descripción: El sistema debe gestionar listas de espera automáticas para horarios médicos altamente demandados
Prioridad: Media
Criterios de Aceptación:

CA-017.1: Paciente puede solicitar ingreso a lista de espera para especialidad/específico médico

CA-017.2: Sistema notifica automáticamente cuando surge disponibilidad por cancelación

CA-017.3: Ofrece horario disponible con ventana de 2 horas para confirmación

CA-017.4: Asignación automática por orden de solicitud en lista de espera

CA-017.5: Límite configurable de pacientes en lista de espera por médico

RF-018: Gestión de Documentos Adjuntos
Descripción: El sistema debe permitir adjuntar documentos a las citas y perfiles de pacientes
Prioridad: Baja
Criterios de Aceptación:

CA-018.1: Médico puede adjuntar documentos a consulta (prescripciones, notas)

CA-018.2: Paciente puede subir documentos previos a la cita (exámenes, estudios)

CA-018.3: Límite de 10MB por archivo con tipos permitidos (PDF, JPG, PNG, DOC)

CA-018.4: Encriptación de documentos sensibles en reposo y tránsito

CA-018.5: Control de versiones para documentos modificados

RF-019: Sistema de Encuestas de Satisfacción
Descripción: El sistema debe enviar encuestas de satisfacción automáticas post-consulta
Prioridad: Baja
Criterios de Aceptación:

CA-019.1: Envío automático de encuesta 2 horas después de la cita completada

CA-019.2: Encuesta máxima de 5 preguntas con escala 1-5 estrellas

CA-019.3: Campo opcional para comentarios libres del paciente

CA-019.4: Dashboard con métricas de satisfacción por médico y especialidad

CA-019.5: Alertas para puntuaciones inferiores a 3 estrellas

RF-020: Integración con Calendarios Externos
Descripción: El sistema debe sincronizar citas con calendarios externos de pacientes y médicos
Prioridad: Media
Criterios de Aceptación:

CA-020.1: Paciente puede agregar cita a Google Calendar/Outlook/Apple Calendar

CA-020.2: Médico puede sincronizar su agenda con calendario corporativo

CA-020.3: Actualización automática en calendarios externos ante cambios

CA-020.4: Formato estándar iCal para compatibilidad multiplataforma

CA-020.5: Opción de sincronización unidireccional o bidireccional configurable


## 4. Casos de uso

### 4.1 Agendar Cita Médica Online

**Caso de Uso:** UC-001  
**Nombre:** Agendar Cita Médica Online  
**Actores:** Usuario Paciente (primario), Sistema (secundario)  
**Descripción:** Este caso de uso permite a un usuario agendar una cita médica de forma autónoma a través de la plataforma web, seleccionando entre servicios y horarios disponibles.  
**Precondiciones:**
- El usuario está autenticado en el sistema mediante SSO universitario
- El usuario tiene estado activo en el centro de salud
- No tiene bloqueos por ausentismo reiterado

**Flujo Principal:**
1. El usuario selecciona la opción "Agendar Cita"
2. El sistema muestra los servicios disponibles: Medicina General, Psicología, Odontología
3. El usuario selecciona "Medicina General"
4. El sistema muestra los médicos generales disponibles con sus horarios de atención
5. El usuario selecciona un médico
6. El sistema muestra calendario con horarios disponibles para los próximos 7 días
7. El usuario selecciona fecha y horario deseado (ej: "18/Oct/2025 - 10:00 AM")
8. El sistema verifica disponibilidad en tiempo real
9. El sistema muestra resumen de la cita seleccionada
10. El usuario confirma la cita
11. El sistema:
    - Registra la cita con estado "Confirmada"
    - Bloquea el horario en la agenda del médico
    - Genera número de confirmación único
    - Envía email de confirmación con detalles
    - Programa recordatorio para 24 horas antes
12. El sistema muestra comprobante digital de la cita

**Flujos Alternativos:**
- **FA-1:** No hay horarios disponibles
  1. El sistema muestra mensaje "No hay horarios disponibles para el médico seleccionado"
  2. El sistema sugiere otros médicos del mismo servicio con disponibilidad
  3. El usuario puede seleccionar otra opción o cancelar el proceso
- **FA-2:** Usuario con ausentismo previo
  1. El sistema detecta que el usuario tiene 2 ausencias sin justificación en los últimos 30 días
  2. El sistema muestra advertencia: "Tiene historial de ausentismo. La falta a esta cita podría generar suspensión temporal"
  3. El usuario debe confirmar que comprende la política para continuar
- **FA-3:** Selección de psicología con restricciones de confidencialidad
  1. El usuario selecciona servicio de Psicología
  2. El sistema muestra advertencia de confidencialidad especial
  3. El usuario debe aceptar términos específicos de tratamiento de datos sensibles

**Postcondiciones:**
- La cita queda registrada en el sistema
- El usuario recibe confirmación por correo electrónico
- El horario queda bloqueado en la agenda del médico
- Se programa recordatorio automático


CU-007: 
**Nombre:** Gestionar Lista de Espera
**Actores:** Paciente
**Propósito:** Solicitar ingreso a lista de espera para horarios no disponibles
Horario médico deseado no disponible, paciente registrado en sistema

**Flujo Principal:**

-Paciente busca disponibilidad para médico/especialidad específica

-Sistema muestra mensaje "No hay horarios disponibles"

-Sistema ofrece opción "Unirse a lista de espera"

-Paciente confirma ingreso a lista de espera

-Sistema registra solicitud con timestamp

-Cuando surge disponibilidad por cancelación, sistema notifica al primer paciente en lista

-Paciente recibe notificación con opción de confirmar en 2 horas

-Si confirma, sistema agenda cita automáticamente

-Si no confirma, sistema notifica al siguiente en lista

**Flujos Alternativos:**

-7a: Paciente no responde en 2 horas → sistema pasa al siguiente en lista

-8a: Paciente rechaza horario → permanece en lista para próximas opciones

**Postcondiciones:** Paciente en lista de espera o cita confirmada, notificaciones enviadas

https://mapify.so/share-link/wcchew6bES

CU-008: 
**nombre:** Sincronizar con Calendario Externo
**Actores:** Paciente/Médico
**Propósito:** Sincronizar citas y agenda con calendarios personales/profesionales
**Precondiciones:** Usuario tiene cita programada o agenda configurada

**Flujo Principal:**

Usuario accede a sección "Mis Citas" o "Mi Agenda"

Sistema muestra opción "Sincronizar con Calendario"

Usuario selecciona proveedor de calendario (Google/Outlook/Apple)

Sistema genera archivo iCal o conecta via API según selección

Para API: usuario autoriza acceso a calendario

Sistema sincroniza citas existentes y agenda

Usuario confirma sincronización exitosa

Sistema programa sincronizaciones automáticas para cambios futuros

**Flujos Alternativos:**

5a: Usuario rechaza autorización → ofrecer descarga manual de archivo iCal

7a: Error en sincronización → sistema sugiere reintentar o contactar soporte

**Postcondiciones:** Citas sincronizadas con calendario externo, actualizaciones automáticas configuradas

[![](https://mapify.so/share-link/XZLQJ6hyTH)








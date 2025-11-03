# ESPECIFICACIÓN DE REQUISITOS DE SOFTWARE
# MediPlus - Sistema de Gestión de Citas y Consulta Externa

## 1. Introducción

### 1.1 Propósito
Este documento especifica los requisitos para el Sistema MediPlus, una aplicación web que automatizará los procesos de agendamiento de citas, gestión de historias clínicas electrónicas y control de consultas externas para el Centro de Salud Universitario San Rafael.

### 1.2 Alcance
El sistema permitirá la gestión integral del flujo de atención médica, desde la solicitud de cita hasta el registro de la consulta, incluyendo gestión de disponibilidad médica, recordatorios automáticos, historia clínica digital y generación de reportes estadísticos.

### 1.3 Definiciones, acrónimos y abreviaturas
- **MediPlus**: Nombre del sistema de gestión de citas y consulta externa
- **HCE**: Historia Clínica Electrónica
- **URP**: Universidad Regional del Pacífico
- **EPS-U**: Aseguradora universitaria
- **SSO**: Single Sign-On (autenticación única)
- **RIPS**: Registro Individual de Prestación de Servicios de Salud
- **MVP**: Producto Mínimo Viable

### 1.4 Referencias
- IEEE Std 830-1998
- Ley 1438 de 2011 - Historia Clínica Digital
- Ley 1581 de 2012 - Protección de Datos Personales
- Resolución 1995 de 1999 - Normativa de Historias Clínicas
- Manual de procesos del Centro de Salud San Rafael

### 1.5 Resumen
El documento describe el sistema MediPlus que reemplazará los procesos manuales actuales, mejorando la eficiencia operativa y reduciendo los riesgos médico-legales.

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
- **Estudiantes (85%)**: Usuarios principales, nativos digitales, requieren agendamiento rápido y autónomo
- **Docentes y Administrativos (15%)**: Mismas funcionalidades pero con diferentes perfiles de disponibilidad
- **Recepcionistas**: Personal administrativo que requiere interfaces eficientes para agendamiento presencial
- **Médicos Generales**: Profesionales con variada habilidad tecnológica, necesitan interfaces intuitivas
- **Especialistas (Psicólogos, Odontólogos)**: Requieren funcionalidades específicas por especialidad
- **Personal de Enfermería**: Necesitan acceso rápido para registro de signos vitales
- **Farmaceuta**: Gestión de inventario y despacho de medicamentos
- **Directores**: Acceso a dashboards y reportes gerenciales

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

## 5. Diagrama de Casos de Uso




<img width="2048" height="1080" alt="jS0_9Aajdd5zcWXEoprFa" src="https://github.com/user-attachments/assets/d2d03d93-6274-4383-a5c7-12ce7252386c" />






## 6. Diagrama de Casos de Uso Detallado


┌─────────────────────────────────────────────────────────────────┐
│ ACTORES PRINCIPALES │
├─────────────────┬─────────────────┬─────────────────┬───────────┤
│ USUARIO │ MÉDICO │ RECEPCIONISTA │ ENFERMERA │
│ PACIENTE │ │ │ │
└─────────────────┴─────────────────┴─────────────────┴───────────┘
│ │ │ │
├─ Agendar Cita ├─ Registrar ├─ Agendar ├─ Registrar
├─ Cancelar Cita │ Consulta │ Cita │ Signos
├─ Consultar ├─ Gestionar │ Presencial │ Vitales
│ Historial │ Agenda ├─ Realizar │
└─ Consultar └─ Consultar │ Check-in │
Disponibilidad Historia └─ Gestionar │
│ Lista Espera │
│ │
│ │
┌─────────────────────────────────────────────────────────────────┐
│ ACTORES SECUNDARIOS │
├─────────────────┬─────────────────┬─────────────────┬───────────┤
│ FARMACEUTA │ DIRECTOR │ SISTEMA │ SSO │
│ │ │ EXTERNO │ URP │
└─────────────────┴─────────────────┴─────────────────┴───────────┘
│ │ │ │
├─ Gestionar ├─ Generar ├─ Enviar ├─ Autenticar
│ Inventario │ Reportes │ Recordatorios│ Usuario
├─ Controlar ├─ Consultar ├─ Validar │
│ Despacho │ Indicadores │ Disponibilidad
└─ Generar └─ Exportar └─ Auditoría
Alertas Stock RIPS Accesos


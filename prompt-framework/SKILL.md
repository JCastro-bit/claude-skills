# Skill: prompt-framework

Framework de prompts para Claude Code. Aplica estas reglas automáticamente al ayudar a planear y construir proyectos.

## Cuándo activarse

- El usuario pide ayuda para **planear un proyecto** sin dar contexto suficiente
- Quiere **estructurar un prompt** o mejorar su workflow
- Pide crear un **CLAUDE.md** para un proyecto
- Describe un **bug** sin contexto estructurado
- Da **feedback vago** ("mejóralo", "no me gustó", "hazlo de nuevo")
- Quiere generar un **resumen de sesión** para retomar después

---

## Las 5 Reglas

### Regla 1 — Contexto antes de código

Antes de escribir código, asegúrate de tener tres cosas: **QUÉ** es el proyecto, **PARA QUIÉN** es, y **CUÁL** es el objetivo. Si el usuario no proporciona esta información, pregúntala antes de continuar.

**Regla mental:** Si el prompt no responde QUÉ, PARA QUIÉN y POR QUÉ — no está listo. Agregar 30 segundos de contexto ahorra 30 minutos de rehacer.

Ejemplo de prompt con contexto suficiente:
```
Voy a construir una aplicación web donde los clientes de una barbería
puedan ver los horarios disponibles y reservar una cita.

Público: hombres 25-45, mobile-first, poco pacientes (tiene que ser rápido)
Objetivo de negocio: reducir las llamadas al local y las citas perdidas
Funcionalidades principales: ver disponibilidad en calendario, reservar,
recibir confirmación, y cancelar con 24h de anticipación

Usa el stack que consideres más eficiente para este caso.
Antes de escribir código, proponme la arquitectura.
```

### Regla 2 — Divide en fases, no pidas todo de una vez

Propón siempre un plan de 5 fases con checkpoints. Si algo sale mal, solo se repite ESA fase — no se empieza todo desde cero.

| Fase | Qué se hace | Para qué sirve |
|------|-------------|-----------------|
| **1. Planificación** | Arquitectura, dependencias, modelo de datos | Validar que se entiende el proyecto antes de escribir código |
| **2. Fundación** | Setup del proyecto, configuración base | Tener una base sólida donde construir encima |
| **3. Construcción** | Una funcionalidad a la vez | Control de calidad pieza por pieza |
| **4. Integración** | Conectar las piezas entre sí | Verificar que todo funciona junto |
| **5. Pulido** | Responsive, errores, performance, SEO | Que esté listo para entregar o publicar |

Cada fase es un checkpoint. Presenta el plan al usuario y espera validación antes de avanzar a la siguiente fase.

### Regla 3 — Especifica las restricciones, no solo el resultado

Si el usuario no menciona restricciones, pregunta por:
- **Tecnologías preferidas** o las que ya usa en el proyecto
- **Servicios externos** a integrar (pagos, emails, auth, APIs)
- **Lo que NO quiere** — restricciones y límites explícitos
- **Destino** — hosting, plataforma, dispositivos principales
- **Nivel de complejidad** — MVP rápido / producción pulida / enterprise

### Regla 4 — Patrón RCF (Resultado -> Criterio -> Formato)

Cada pedido debe tener estos tres elementos. Si el usuario no los proporciona, ayúdalo a estructurarlos:

| Elemento | Pregunta que responde | Ejemplo |
|----------|----------------------|---------|
| **RESULTADO** | ¿Qué quiero que exista al final? | "Un sistema que genere cotizaciones en PDF" |
| **CRITERIO** | ¿Cómo sé que está bien hecho? | "Debe calcular impuestos, enviar por email, y guardar historial" |
| **FORMATO** | ¿Cómo me lo entregas? | "Código comentado + instrucciones de setup + datos de prueba" |

Ejemplo estructurado:
```
RESULTADO: Un endpoint que procese pagos.

CRITERIO:
- Acepta los métodos de pago más comunes
- Maneja errores (pago rechazado, fondos insuficientes, timeout)
- Retorna una respuesta clara con el status
- Guarda un registro de cada transacción
- Envía confirmación al comprador

FORMATO:
- Código comentado explicando la lógica en cada paso
- Un archivo de test con 3 casos (pago exitoso, rechazado, error de red)
- Variables de entorno documentadas
```

**Regla mental:** Si el prompt no tiene RESULTADO, CRITERIO y FORMATO, le faltan datos. No llenes los vacíos con suposiciones — pregunta.

### Regla 5 — Itera con feedback específico, nunca repitas desde cero

Cuando el usuario da feedback vago ("no me gustó", "mejóralo", "hazlo más profesional"), guíalo a ser específico:

- Pide que enumere los cambios concretos (1, 2, 3...)
- Pregunta QUÉ específicamente no le gustó
- Sugiere el formato de feedback enumerado

Ejemplo de feedback específico:
```
Funciona bien pero necesito 4 ajustes:
1. El color de fondo del header debería ser más oscuro
2. El botón principal debe decir "Reservar ahora" en vez de "Enviar"
3. Agrega un contador arriba del botón: "47 citas agendadas esta semana"
4. El subtítulo es muy largo — resúmelo a máximo 12 palabras
```

---

## Debugging estructurado

Cuando el usuario reporta un bug sin contexto suficiente, guíalo a proporcionar:

```
Tengo un error en [DÓNDE].

Qué intentaba hacer:
[La acción que disparó el error]

Qué esperaba que pasara:
[El resultado correcto]

Qué pasó en realidad:
[El error o comportamiento incorrecto]

Error exacto:
[Pega el error del terminal o la consola]

Acciones:
1. Identifica la causa raíz
2. Explícame en una oración por qué pasa
3. Corrígelo
4. Muéstrame el antes y después del cambio
5. Verifica que no rompa nada más
```

---

## Generación de CLAUDE.md

Cuando el usuario pida crear un CLAUDE.md, usa el template de `references/claude-md-template.md`. Pregunta la información necesaria para completar cada sección:

1. Nombre y descripción del proyecto
2. Stack tecnológico
3. Estructura de carpetas
4. Reglas y convenciones
5. Contexto del negocio
6. Estado actual del proyecto
7. Variables de entorno

---

## Gestión de sesiones

### Al cerrar una sesión

Cuando el usuario indique que va a cerrar la sesión o lo pida explícitamente, genera un resumen técnico con:

1. Qué archivos se crearon/modificaron y qué hace cada uno
2. Qué funcionalidades están completas
3. Qué queda pendiente
4. Decisiones técnicas tomadas y por qué
5. Bugs conocidos o cosas por revisar
6. El último cambio realizado

Formatea el resumen para que pueda pegarse al inicio de una nueva sesión.

### Al retomar una sesión

Si el usuario pega un resumen de sesión anterior o dice "retomemos donde dejamos", lee el resumen y continúa exactamente desde ese punto.

---

## Cheatsheet rápido

| Situación | Qué hacer |
|-----------|-----------|
| Empezar un proyecto | "Antes de escribir código, dame la arquitectura y el modelo de datos" |
| Pedir una feature | Usar RESULTADO -> CRITERIO -> FORMATO |
| Corregir algo | Enumerar cambios específicos (1, 2, 3...) |
| Algo no funciona | Describir: qué intenté, qué esperaba, qué pasó, error exacto |
| Cerrar sesión | Pedir resumen técnico del estado actual |
| Abrir sesión nueva | Pegar resumen + "retomemos donde dejamos" |
| Documentar | "Documenta lo que construimos en el README" |
| Revisar calidad | "Revisa el código: errores, edge cases, y optimizaciones" |
| Preparar entrega | "Prepara el proyecto para deploy: variables, config, checklist" |

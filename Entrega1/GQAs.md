---
name: generador-qas
description: Identifica atributos de calidad (QAs) en un enunciado de sistema y los refina como escenarios de 6 partes del SEI (Fuente, Estímulo, Artefacto, Ambiente, Respuesta, Medida de respuesta). Usar siempre que el usuario mencione atributos de calidad, QAs, requerimientos no funcionales, escenarios SEI, template de 6 partes, o pida refinar/convertir requerimientos en escenarios de calidad — incluso si no nombra el template explícitamente. También responde a los comandos /Refinar-QAs, "Generame los QAs", "Generame el SEI", "Refiná los requerimientos no funcionales", "Identificá los atributos de calidad de este sistema".
---

# Generador de QAs (escenarios SEI de 6 partes)

Transforma requerimientos expresados en lenguaje natural en escenarios de atributos de
calidad completos, siguiendo el template de 6 partes del SEI. Sirve tanto para descubrir
los QAs implícitos en la descripción de un sistema completo como para refinar un
requerimiento suelto que ya viene enunciado.

## 1. Objetivo

Producir escenarios de calidad **precisos y testeables**. Un atributo de calidad por sí
solo ("performance", "seguridad") no significa nada hasta que se lo describe en un
contexto operacional concreto con una medida verificable. El valor de esta skill está en
hacer esa traducción sin perder rigor.

## 2. Modos de operación

Antes de responder, determinar cuál de los dos modos aplica:

- **Modo A (descubrimiento):** la entrada es la descripción de un sistema completo
  (varios párrafos, funcionalidades, actores). Identificar *todos* los QAs relevantes que
  se desprenden del texto y generar un escenario para cada uno.
- **Modo B (refinamiento):** la entrada es un requerimiento suelto o un QA ya nombrado
  por el usuario. Generar directamente el escenario correspondiente.

Ante la duda, preferir Modo A: es peor omitir un atributo relevante que refinar de más.

## 3. Definiciones de las 6 partes

Usar **exclusivamente** estas definiciones del SEI para determinar el contenido de cada
fila. No reinterpretarlas con definiciones coloquiales o ajenas al marco.

| Parte | Qué es | Pregunta guía |
|---|---|---|
| Fuente del estímulo | Persona, sistema o componente que genera el estímulo | ¿Quién o qué lo dispara? |
| Estímulo | Evento concreto que requiere una respuesta del sistema | ¿Qué ocurre exactamente? |
| Artefacto | Parte del sistema cuyo comportamiento se caracteriza | ¿Qué componente recibe el impacto? |
| Ambiente | Estado operacional del sistema al momento del estímulo | ¿Cómo estaba el sistema cuando pasó? |
| Respuesta | Acción externamente observable que ejecuta el artefacto | ¿Qué *hace* el sistema? |
| Medida de respuesta | Criterio de éxito específico y medible | ¿Cómo sé, con un número, si salió bien? |

### Errores frecuentes a evitar (y por qué)

Estas tres confusiones son las que más degradan la calidad de un escenario:

- **Ambiente ≠ contexto de negocio.** "Crecimiento planificado de la empresa" describe el
  *motivo* por el que ocurre el estímulo, no el *estado del sistema*. Lo correcto sería
  "operación normal, con usuarios activos". Si la respuesta suena a "por qué pasa esto"
  en lugar de "cómo estaba el sistema cuando pasó", está mal. Importa porque el ambiente
  es lo que determina qué tan exigente es el escenario: no es lo mismo escalar con el
  sistema detenido que en caliente.
- **Respuesta ≠ conclusión de éxito.** "El sistema soporta el crecimiento" o "el sistema
  absorbe la carga" son juicios de valor, no acciones. Lo correcto describe qué hace el
  sistema: "registra los nuevos dispositivos y los incorpora al servicio de tracking". Si
  la frase empieza con "logra", "soporta" o "absorbe", probablemente se esté escribiendo
  la Medida disfrazada de Respuesta. Importa porque una respuesta no observable no se
  puede verificar ni implementar.
- **Medida vaga ≠ medida.** Si no se puede escribir un test que pase o falle contra ese
  valor, la medida todavía no es específica. "Rápido", "sin problemas" o "en poco tiempo"
  no sirven. Tampoco sirven las proporciones ambiguas ("un día por cada porcentaje de
  crecimiento"): hay que fijar un umbral concreto y decir desde qué momento se cuenta.

## 4. Manejo de datos faltantes (straw man)

Los enunciados casi nunca traen números. Dejar la medida vacía **no** es la solución: un
escenario sin medida no es un escenario, y un campo en blanco no dispara ninguna
conversación con los stakeholders. La técnica correcta es el *Response Measure Straw Man*:
proponer una estimación razonable que sirva de punto de partida para discutir.

Reglas:

1. **Distinguir dato de suposición.** Si el enunciado provee un valor explícito (por
   ejemplo, "una pausa de hasta 15 minutos"), usarlo tal cual y **no** marcarlo como
   suposición. Solo se marcan los valores que la skill inventa.
2. **Marcar toda suposición** en un apartado debajo de la tabla, indicando el criterio que
   la originó — no solo el número. Un valor sin criterio no se puede evaluar ni corregir
   con fundamento.
3. **Cuidado con el anclaje.** El primer número propuesto tiende a quedar fijado en la
   discusión. La estimación debe ser defendible por analogía con sistemas similares, no
   arbitraria.
4. **La skill propone, el ingeniero dispone.** Los valores generados son insumo para la
   conversación con stakeholders, nunca un compromiso cerrado.

## 5. Flujo de trabajo

1. Analizar la entrada y determinar el modo (A o B).
2. Identificar el o los atributos de calidad, apoyándose en pistas textuales concretas del
   enunciado (menciones a tiempos, fallas, crecimiento, integraciones externas, accesos,
   contexto de uso).
3. Para cada atributo, completar las 6 partes según las definiciones de la sección 3.
4. Completar los valores faltantes como straw man, según la sección 4.
5. Verificar coherencia antes de responder: que el atributo identificado se corresponda con
   la justificación, que Ambiente describa un estado operacional, que Respuesta sea una
   acción observable, y que la Medida sea testeable. Esta es una revisión de consistencia
   básica; la auditoría exhaustiva del escenario corresponde a la skill verificadora.
6. Entregar la respuesta con el formato de la sección 6.

## 6. Estructura de la respuesta

**Modo B** — un solo bloque:

```
## QA: [Nombre del atributo]

[2-3 líneas: en qué parte del enunciado se detectó y por qué corresponde ese atributo.]

| Parte | Contenido |
|---|---|
| Fuente del estímulo | ... |
| Estímulo | ... |
| Artefacto | ... |
| Ambiente | ... |
| Respuesta | ... |
| Medida de respuesta | ... |

**Suposiciones a validar:** el valor de [fila] se asumió en [X] tomando como referencia
[criterio o analogía]. Validar con stakeholders.
```

**Modo A** — un bloque como el anterior por cada atributo identificado, y al final una
sección única "Suposiciones a validar" consolidando todas las estimaciones, para que el
ingeniero pueda revisarlas de un vistazo.

## 7. Ejemplos de referencia

### Ejemplo 1 — Modo B (requerimiento suelto)

**Input:** "Se desea desarrollar un procesador de texto que sea tolerante a fallas,
particularmente en casos de errores al hacer el rendering (previsualización) de un
documento previamente a su impresión."

**Output:**

## QA: Disponibilidad

El requerimiento plantea que una falla en un módulo puntual (el renderizado) no debe
comprometer la operación del sistema completo. Esa es la definición operativa de
tolerancia a fallas, que se materializa como un escenario de disponibilidad.

| Parte | Contenido |
|---|---|
| Fuente del estímulo | Motor de renderizado, ante un documento con formato corrupto |
| Estímulo | Ocurre un error durante el renderizado de la previsualización |
| Artefacto | Módulo de renderizado del procesador de texto |
| Ambiente | Operación normal, con el usuario preparando un documento para imprimir |
| Respuesta | El sistema aísla el fallo, preserva el documento sin guardar y notifica el error al usuario |
| Medida de respuesta | El resto del procesador de texto continúa operativo, con recuperación del módulo en menos de 5 segundos y sin pérdida de cambios no guardados |

**Suposiciones a validar:** el valor de 5 segundos se asumió por analogía con tiempos
típicos de recuperación de módulos no críticos en aplicaciones de escritorio. Validar con
stakeholders.

### Ejemplo 2 — Modo A (enunciado de sistema completo)

**Input:** Una empresa va a lanzar un negocio para permitir el alquiler de monopatines eléctricos en
distintas paradas de una ciudad capital, para lo cual requiere el desarrollo de una
aplicación móvil para los usuarios del servicio, y adicionalmente una aplicación Web para
la gestión correspondiente. El servicio consiste en contar con una flota de monopatines
eléctricos, inicialmente estacionados en diferentes paradas previamente definidas.
 
Para poder utilizar el monopatín el usuario deberá crearse una cuenta en la app, asociada a
una cuenta de una billetera virtual. Previamente al uso del servicio, debe haber cargado en
su cuenta un monto de dinero, que se irá descontando en función del tiempo de uso del
monopatín.
 
Una vez que la cuenta tenga cargado dinero, el usuario podrá activar un monopatín para su
uso, mediante un lector de código QR. En ese momento se generará un viaje asociado a la
cuenta, registrando fecha y hora de inicio. El uso del monopatín es por tiempo, y comienza
a consumirse el crédito cuando se activa.
 
Si el usuario requirió detenerse durante no más de 15 minutos en algún punto intermedio del
viaje, la app contará con una opción Pausar. Con esta opción se registra una pausa asociada
al viaje, para establecer que el monopatín no está siendo utilizado, aunque aún corre el
gasto de créditos. De esta manera se puede establecer el uso real del monopatín. Una vez
finalizada la pausa el usuario lo puede indicar por la app. Si pasaran los 15 minutos
automáticamente se volverá a considerar en uso el monopatín, y se comienza a cobrar un
monto mayor de crédito hasta el final del viaje.
 
El monopatín contará con un GPS y está identificado unívocamente con un ID, por lo que en
todo momento se puede determinar dónde está cada monopatín. Para el mantenimiento se
requiere el registro del tiempo de uso y los kilómetros recorridos, así como la generación
de reportes asociados, incluyendo tiempo con pausas y sin pausas.

**Output (extracto — en Modo A se genera un bloque por cada QA identificado):**

## QA: Interoperabilidad

El enunciado indica que las cuentas del servicio se asocian a una billetera virtual externa
para cargar y consumir saldo. Eso implica intercambio de información entre dos sistemas de
organizaciones distintas a través de sus interfaces, que es la definición de
interoperabilidad.

| Parte | Contenido |
|---|---|
| Fuente del estímulo | Usuario del servicio, desde la app móvil |
| Estímulo | Carga saldo en su cuenta usando la billetera virtual externa |
| Artefacto | Módulo de integración de pagos del backend |
| Ambiente | Operación normal, con el servicio de la billetera disponible |
| Respuesta | El sistema envía la solicitud de pago, recibe la confirmación y acredita el saldo en la cuenta del usuario |
| Medida de respuesta | El 99,9% de las transacciones se sincronizan correctamente, con el saldo reflejado en la app en menos de 10 segundos |

## QA: Confiabilidad (integridad de datos)

El sistema cobra por tiempo de uso y distingue entre tiempo con y sin pausas, con una
tarifa mayor si la pausa supera los 15 minutos. De la exactitud de ese cálculo dependen
tanto la facturación al usuario como las decisiones de mantenimiento de la flota.

| Parte | Contenido |
|---|---|
| Fuente del estímulo | Usuario del servicio |
| Estímulo | Pausa el viaje y lo reanuda antes de cumplirse los 15 minutos permitidos |
| Artefacto | Módulo de cálculo de tiempo de uso y tarifas |
| Ambiente | Operación normal, dentro de la ventana de pausa permitida |
| Respuesta | El sistema registra la pausa, detiene el conteo de uso efectivo y aplica la tarifa normal al reanudar |
| Medida de respuesta | El 100% de los viajes con pausa se facturan según el tiempo real registrado, verificable contra el log de eventos |

**Suposiciones a validar:**
- El 99,9% de sincronización y los 10 segundos del escenario de interoperabilidad se
  asumieron por analogía con SLAs típicos de pasarelas de pago. Validar con stakeholders.
- El límite de 15 minutos **no** es una suposición: está especificado en el enunciado.

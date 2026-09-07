---
name: test-qas
description: Audita escenarios de atributos de calidad en formato SEI de 6 partes para determinar si están completos y correctos, y explica cómo completarlos si no lo están. Usar siempre que el usuario pida verificar, chequear, validar, revisar o corregir un escenario de calidad, o pregunte si un escenario SEI está bien formulado o completo. También responde a /Chequear-QAs, "revisá este escenario", "está completo este QA?".
---

# Check QAs(check Escenarios SEI de 6 partes)
Analiza escenarios de atributos de calidad con el formato SEI de 6 partes para decidir si estan completos o no.
En caso de no estar completos, se debe proporcionar una guia para completarlos.

## 1. Objetivo
Testear escenarios de calidad propuestos por el usuario para refinar y precisar
los requerimientos si lo es necesario o tener una confirmacion de la precision de los mismos.

## 2. Definiciones de las 6 partes  
Usar **exclusivamente** estas definiciones del SEI para testear el contenido de cada
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

## 3. Manejo de datos
Si el escenario no cumple con los estandares, o no esta completo, se debe indicar y precisar el error
en los parametros.Guiando al usuario en una mejor solucion teniendo en cuenta el contexto en el que se
desarrolla ese escenario.

reglas:
1.**Verificar formato.**Si las 6 partes del SEI no existen en la entrada(por ejemplo un escenario con 4 partes),se debe proponer un valor concreto para completarla 
2.**Verificar los valores de medida.**si el valor parece inviable o desalineado con el dominio, marcarlo como advertencia y explicar por qué.
3.**Verificar los valores del contexto.**verificar la coherencia interna: que el Artefacto sea consistente con el Estímulo, que la Respuesta sea razonable para ese Artefacto, y que la Medida mida efectivamente lo que la Respuesta produce.
4.**Verificar la jerga de la respuesta.**la redacción debe ser inequívoca: dos lectores distintos deben interpretar lo mismo. Se permite y se espera vocabulario técnico cuando aporta precisión; se rechaza la jerga que oscurece el significado o los términos vagos.

## 4. Flujo de trabajo
1.Verificar que la entrada tenga el formato de 6 partes del SEI junto a su respectivo QA.
2.Verificar que los valores de las 6 partes del SEI sean coherentes y cumplan con los estandares posteriormente dichos.
3.Verificar que el escenario en su conjunto refleje verdaderamente el atributo de calidad que referencia.
4.Entregar la respuesta con los resultados de las verificaciones anteriores.

## 5. Estructura de la respuesta:
 QA: [Nombre del atributo]
|verificacion de formato|verificacion de valores|verificacion del escenario en su conjunto|

[Respuestas: si la verificacion pasa, indicar con "correcto", sino, indicar "incorrecto" o "parcialmente incorrecto" junto el porque de dicha decision.Se debe entregar un analisis riguroso de los resultados y un escenario corregido con las modificaciones sugeridas.]

## 6. Ejemplos de referencia

### Ejemplo 1 — Escenario con defectos

**Input:**

QA: Escalabilidad

| Parte | Contenido |
|---|---|
| Fuente del estímulo | Administrador |
| Estímulo | Agrega 200 monopatines nuevos a la flota |
| Artefacto | Sistema completo |
| Ambiente | Crecimiento planificado del negocio |
| Respuesta | El sistema soporta el crecimiento |
| Medida de respuesta | Sin necesidad de cambios arquitectónicos, manteniendo los tiempos de respuesta dentro del SLA |

**Output:**

## QA: Escalabilidad — Cumple estándares: **parcialmente**

| Verificación de formato | Verificación de valores | Verificación del conjunto |
|---|---|---|
| Correcto — las 6 partes están presentes | Incorrecto — fallan Ambiente y Respuesta | Parcialmente correcto |

**Análisis:**

- **Fuente, Estímulo, Artefacto:** correctos. El estímulo es concreto y cuantificado. Como
  mejora menor, el Artefacto podría precisarse ("módulo de gestión de flota + servicio de
  tracking") en lugar de "sistema completo", para que el escenario sea más accionable.
- **Ambiente: incorrecto.** "Crecimiento planificado del negocio" describe el motivo de
  negocio, no el estado operacional del sistema. Corresponde indicar en qué condiciones
  está el sistema cuando ocurre el estímulo.
- **Respuesta: incorrecta.** "El sistema soporta el crecimiento" es una conclusión de
  éxito, no una acción observable. Hay que describir qué hace el sistema, no si le fue
  bien.
- **Medida: parcialmente correcta.** "Sin cambios arquitectónicos" es verificable, pero
  "dentro del SLA" no lo es mientras no se explicite ese SLA. Falta el umbral concreto.
- **Coherencia con el atributo:** el escenario sí corresponde a escalabilidad (aumento de
  carga absorbido con recursos, no con rediseño). No hay confusión de atributo.

**Escenario corregido sugerido:**

| Parte | Contenido |
|---|---|
| Fuente del estímulo | Administrador de monopatines |
| Estímulo | Agrega 200 monopatines nuevos a la flota |
| Artefacto | Módulo de gestión de flota y servicio de tracking |
| Ambiente | Operación normal, con usuarios activos utilizando el servicio |
| Respuesta | El sistema registra los nuevos monopatines y los incorpora al servicio de tracking, quedando visibles y disponibles en el mapa para los usuarios |
| Medida de respuesta | La incorporación se completa sin modificar componentes existentes y sin que el tiempo de respuesta del mapa supere los 2 segundos durante el proceso |

**Suposición introducida en la corrección:** los 2 segundos son un straw man, tomado como
umbral típico de respuesta en apps móviles de consumo. Validar con stakeholders.

### Ejemplo 2 — Escenario correcto

**Input:**

QA: Confiabilidad (integridad de datos)

| Parte | Contenido |
|---|---|
| Fuente del estímulo | Dos usuarios distintos, simultáneamente |
| Estímulo | Escanean el código QR del mismo monopatín al mismo tiempo |
| Artefacto | Servicio de asignación de monopatines |
| Ambiente | Operación normal, en horario pico con alta concurrencia |
| Respuesta | El sistema asigna el monopatín a un único usuario y notifica al otro que ya no está disponible |
| Medida de respuesta | 0% de casos de doble asignación sobre el total de activaciones concurrentes, verificable en el log de viajes |

**Output:**

## QA: Confiabilidad (integridad de datos) — Cumple estándares: **sí**

| Verificación de formato | Verificación de valores | Verificación del conjunto |
|---|---|---|
| Correcto | Correcto | Correcto |

**Análisis:**

- Las 6 partes están presentes y cada una responde a su pregunta guía.
- **Ambiente** describe correctamente un estado operacional ("horario pico con alta
  concurrencia"), que además es el estado bajo el cual el escenario tiene sentido: la
  condición de carrera solo se manifiesta con concurrencia.
- **Respuesta** describe dos acciones observables (asignar, notificar), sin adelantar el
  juicio de éxito.
- **Medida** es específica y testeable: se puede escribir un test de concurrencia que pase
  o falle contra el 0%, y se indica dónde verificarlo.
- El escenario refleja genuinamente confiabilidad/integridad de datos, y no se confunde con
  disponibilidad: el foco está en la corrección del dato, no en que el servicio esté arriba.

**No se detectaron correcciones necesarias.**

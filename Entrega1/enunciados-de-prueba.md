===============================================================================
ENUNCIADOS DE PRUEBA PARA LAS SKILLS DE ATRIBUTOS DE CALIDAD
===============================================================================

Este archivo reune los enunciados utilizados como casos de prueba de las skills
generador-qas, test-qas y el constructor de arbol de utilidad.

Los enunciados del BLOQUE B son requerimientos sueltos: sirven para probar el
Modo B (refinamiento de un requerimiento puntual).

El enunciado del BLOQUE A es la descripcion completa de un sistema: sirve para
probar el Modo A (descubrimiento de atributos a partir de un enunciado).


===============================================================================
BLOQUE B - REQUERIMIENTOS SUELTOS (Ejercicio 2 del TP)
Casos de prueba para el Modo B
===============================================================================

--- Caso B.1 ---------------------------------------------------------------
Un sistema de cajero automatico debe ser facil de usar por una persona mayor.

QA esperado: Usabilidad
----------------------------------------------------------------------------

--- Caso B.2 ---------------------------------------------------------------
Se desea desarrollar un procesador de texto que sea tolerante a fallas,
particularmente en casos de errores al hacer el rendering (pre-visualizacion)
de un documento previamente a su impresion.

QA esperado: Disponibilidad
(Este es el caso usado como Ejemplo 1 de la skill generador-qas)
----------------------------------------------------------------------------

--- Caso B.3 ---------------------------------------------------------------
Un sistema de monitoreo de radares debe soportar la incorporacion de varios
dispositivos (radares) con distinta tecnologia para su monitoreo.

QA esperado: Interoperabilidad (posible solapamiento con Modificabilidad)
----------------------------------------------------------------------------

--- Caso B.4 ---------------------------------------------------------------
En un sistema de seguros debe ser posible configurar distintas politicas para
el calculo de retenciones sobre las polizas emitidas, en funcion del perfil
impositivo del comprador de la poliza.

QA esperado: Modificabilidad (configurabilidad)
----------------------------------------------------------------------------

--- Caso B.5 ---------------------------------------------------------------
Una aplicacion movil para e-commerce debe ser capaz de realizar varias
busquedas geolocalizadas de forma rapida, especialmente en periodos de
promociones.

QA esperado: Performance (con el ambiente en carga pico)
----------------------------------------------------------------------------


===============================================================================
BLOQUE A - SISTEMA COMPLETO: MONOPATINES ELECTRICOS (Apendice del TP)
Caso de prueba para el Modo A
===============================================================================

DESCRIPCION DEL PROBLEMA / SISTEMA

Una empresa va a lanzar un negocio para permitir el alquiler de monopatines
electronicos en distintas paradas de una ciudad capital, para lo cual requiere
el desarrollo de una aplicacion movil para los usuarios del servicio, y
adicionalmente una aplicacion Web para la gestion correspondiente.

El servicio consiste en contar con una flota de monopatines electricos,
inicialmente estacionados en diferentes paradas previamente definidas, dentro
del centro de la ciudad y zonas cercanas. Los monopatines se buscan y se dejan
en dichas paradas, esto es una condicion basica para el funcionamiento del
servicio.

A continuacion, se describe el funcionamiento del servicio.

Para poder utilizar el monopatin el usuario debera crearse una cuenta en la
app, asociada a una cuenta de Mercado Pago. Previamente al uso del servicio,
debe haber cargado en su cuenta un monto de dinero, que se ira descontando en
funcion del tiempo de uso del monopatin. Se puede utilizar la misma cuenta de
Mercado Pago para varias cuentas del servicio.

Una cuenta podra tener asociados varios usuarios que utilizaran los creditos
cargados en la cuenta, y un usuario puede asociarse a mas de una cuenta. Cada
usuario tendra un nombre y debe registrar su numero de celular, email valido,
nombre y apellido. La cuenta tendra un numero identificatorio y una fecha de
alta.

Una vez que la cuenta tenga cargado dinero, el usuario podra activar un
monopatin para su uso, mediante un lector de codigo QR. En ese momento se
generara un viaje asociado a la cuenta del usuario que esta utilizando su app,
registrando fecha y hora de inicio. El uso del monopatin es por tiempo,
comienza a consumirse el credito cuando se activa el monopatin, y esto
permitira que se encienda en ese momento. A partir de alli el usuario del
servicio podra utilizar el monopatin, y una vez que no lo requiera mas debera
dejarlo en una parada previamente establecida. En este momento selecciona la
opcion para cortar el servicio, una vez estacionado el monopatin, finalizando
el viaje. Al finalizar el viaje se va a registrar la fecha y hora de
finalizacion y los kilometros recorridos. Cabe aclarar que la app no debe
permitir finalizar un viaje si no detecta mediante el GPS con el que cuenta el
monopatin, que se encuentra en una parada permitida.

Si el usuario requirio detenerse durante no mas de 15 minutos en algun punto
intermedio del viaje, la app contara con una opcion Pausar. Con esta opcion se
registra una pausa asociada al viaje, para establecer que el monopatin no esta
siendo utilizado, aunque aun corre el gasto de creditos. De esta manera se
puede establecer el uso real del monopatin, y la app permite apagarlo, pero no
lo desasigna a la cuenta actual. Una vez finalizada la pausa el usuario lo
puede indicar por la app, para poder encender el monopatin. Si pasaran los 15
min automaticamente se volvera a considerar en uso el monopatin, y se comienza
a cobrar un monto mayor de credito hasta el final del viaje.

El monopatin contara con un GPS y esta identificado univocamente con ID, por lo
que en todo momento se puede determinar donde esta cada monopatin. De esta
manera, si un usuario necesita un monopatin podra encontrar el mas cercano a
traves de un mapa interactivo en la app que muestra los monopatines en la zona.

Para el mantenimiento de los monopatines se va a crear una aplicacion Web para
registrar todas las acciones de mantenimiento que realizan los Encargados de
Mantenimiento de monopatines. Para establecer si un monopatin requiere de
mantenimiento se considera el tiempo de uso y los kilometros recorridos, para
lo que se requiere del registro de esta informacion, asi como la generacion de
reportes asociados al uso de monopatines, respecto a kilometros y tiempo de
uso, incluyendo tiempo con pausas y sin pausas. Es necesario saber si un
monopatin esta en mantenimiento, o se encuentra habilitado para su uso, al
estar en una parada definida luego de finalizado un mantenimiento.

Ademas, el Administrador de Monopatines es quien gestiona los monopatines y las
paradas en la aplicacion (por ej., agregando, quitando, actualizando datos
segun sea requerido), tambien establece los precios de tarifa normal y extras
por reinicio de pausas extensas. Por otro lado, es capaz de anular cuentas
cuando por algun motivo que se considere necesario.

FUNCIONALIDADES IDENTIFICADAS

- Generar reporte de uso de monopatines por kilometros
- Generar reporte de uso de monopatines por tiempo con pausas
- Generar reporte de uso de monopatines por tiempo sin pausas
- Registrar monopatin en mantenimiento
- Registrar fin de mantenimiento de monopatin
- Ubicar monopatin en parada (opcional)
- Agregar monopatin
- Quitar monopatin
- Registrar parada
- Quitar parada
- Definir precio
- Definir tarifa extra para reinicio por pausa extensa
- Anular cuenta

ATRIBUTOS DE CALIDAD ESPERADOS PARA ESTE ENUNCIADO

Disponibilidad, Performance, Escalabilidad, Seguridad, Confiabilidad
(integridad de datos), Interoperabilidad, Modificabilidad, Usabilidad.


===============================================================================
BLOQUE C - ESCENARIOS DE PRUEBA PARA LA SKILL VERIFICADORA (test-qas)
===============================================================================

--- Caso C.1: escenario CON DEFECTOS (veredicto esperado: parcialmente) ------

QA: Escalabilidad

| Parte | Contenido |
|---|---|
| Fuente del estimulo | Administrador |
| Estimulo | Agrega 200 monopatines nuevos a la flota |
| Artefacto | Sistema completo |
| Ambiente | Crecimiento planificado del negocio |
| Respuesta | El sistema soporta el crecimiento |
| Medida de respuesta | Sin necesidad de cambios arquitectonicos, manteniendo los tiempos de respuesta dentro del SLA |

Defectos que la skill debe detectar:
- Ambiente: describe el motivo de negocio, no el estado operacional.
- Respuesta: es una conclusion de exito, no una accion observable.
- Medida: "dentro del SLA" no es verificable si el SLA no se explicita.
----------------------------------------------------------------------------

--- Caso C.2: escenario CORRECTO (veredicto esperado: si) -------------------

QA: Confiabilidad (integridad de datos)

| Parte | Contenido |
|---|---|
| Fuente del estimulo | Dos usuarios distintos, simultaneamente |
| Estimulo | Escanean el codigo QR del mismo monopatin al mismo tiempo |
| Artefacto | Servicio de asignacion de monopatines |
| Ambiente | Operacion normal, en horario pico con alta concurrencia |
| Respuesta | El sistema asigna el monopatin a un unico usuario y notifica al otro que ya no esta disponible |
| Medida de respuesta | 0% de casos de doble asignacion sobre el total de activaciones concurrentes, verificable en el log de viajes |

La skill no deberia detectar correcciones necesarias en este caso.
----------------------------------------------------------------------------

--- Caso C.3: escenario INCOMPLETO (veredicto esperado: no) -----------------

QA: Performance

| Parte | Contenido |
|---|---|
| Fuente del estimulo | Usuario |
| Estimulo | Abre el mapa para buscar monopatines cercanos |
| Respuesta | El sistema muestra los monopatines disponibles |

Defectos que la skill debe detectar:
- Faltan tres partes: Artefacto, Ambiente y Medida de respuesta.
- La skill debe proponer un valor concreto para cada una de las partes
  ausentes.
----------------------------------------------------------------------------

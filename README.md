# Parcial 2 - Automatización y Control de Procesos
## Etapa de Diseño

Se procedió a realizar el diseño del sistema automatizado a partir de los temas vistos
en clase, en primer lugar se estableció cada una de las variables.

### Definición de Variables

Para la realización de este sistema se establecieron las siguientes variables:

| Nombre                        | Atributo | Tipo | Comentario                                                       |
| ----------------------------- | -------- | ---- | ---------------------------------------------------------------- |
| START                         | INPUT    | BOOL | Botón de inicio del proceso                                      |
| STOP                          | INPUT    | BOOL | Botón para parada del proceso                                    |
| MOTO_BOMBA1                   | INPUT    | BOOL | Encendido y apagado de motobomba1                                |
| MOTO_BOMBA2                   | INPUT    | BOOL | Encendido y apagado de motobomba2                                |
| SENSOR_LLENADO_1              | INPUT    | BOOL | Sensor de llenado para el tanque 1                               |
| SENSOR_LLENADO_2              | INPUT    | BOOL | Sensor de llenado para el tanque 2                               |
| VALVULA_TANQUE_1              | INPUT    | BOOL | Apertura y cierre de la válvula del tanque 1                     |
| VALVULA_TANQUE_2              | INPUT    | BOOL | Apertura y cierre de la válvula del tanque 2                     |
| MEZCLADORA_TANQUE_3           | INPUT    | BOOL | Apagado y encendido de la mezcladora del tanque 3                |
| VALVULA_TANQUE_3              | INPUT    | BOOL | Apertura y cierre de la válvula del tanque 3                     |
| SENSOR_LLENADO_3              | INPUT    | BOOL | Sensor de llenado para el tanque 3                               |
| TEMPORIZADOR_LLENADO          | OUTPUT   | TON  | Temporizador para el tiempo de llenado de los tanques 1 y 2      |
| TEMPORIZADOR_VACIADO_TANQUE_3 | OUTPUT   | TON  | Temporizador para el tiempo de vaciado del tanque 3              |
| TEMPORIZADOR_VALVULA_1        | OUTPUT   | TON  | Temporizador para la apertura de la válvula 1                    |
| TEMPORIZADOR_VALVULA_2        | OUTPUT   | TON  | Temporizador para la apertura de la válvula 2                    |
| TEMPORIZADOR_MEZCLADORA       | OUTPUT   | TON  | Temporizador para el tiempo de mezcla en el tanque 3             |
| TEMPORIZADOR_VALVULA_3        | OUTPUT   | TON  | Temporizador para la apertura de la válvula 3                    |
| TEMPORIZADOR_VACIADO_1_2      | OUTPUT   | TON  | Temporizador para el tiempo de vaciado de los tanques 1 y 2      |
| IR_ENCENDIDO_BOMBAS           | INPUT    | BOOL | Relay para realizar el encendido de las bombas                   |
| IR_APAGADO_MEZCLADORA         | INPUT    | BOOL | Relay para inicializar el sistema                                |
| IR_REINICIO_SISTEMA           | INPUT    | BOOL | Relay para detener el sistema                                    |
| IR_APAGADO_SISTEMA            | INPUT    | BOOL | Relay para el apagado del sistema                                |
| IR_CONTAR                     | INPUT    | BOOL | Relay para contar las veces que ha repetido el proeso el sistema |
| NEGADOR1                      | INPUT    | BOOL | Negador 1                                                        |
| NEGADOR2                      | INPUT    | BOOL | Negador 2                                                        |
| TIEMPO_ACTUAL_LLENADO         | OUTPUT   | TIME | Tiempo actual de llenado de los tanques 1 y 2                    |
| TIEMPO_ACTUAL_MEZCLADORA      | OUTPUT   | TIME | Tiempo actual de mezclado en el tanque 3                         |
| TIEMPO_ACTUAL_VACIADO_1_2     | OUTPUT   | TIME | Tiempo actual de vaciado para los tanques 1 y 2                  |
| TIEMPO_ACTUAL_VACIADO_3       | OUTPUT   | TIME | Tiempo actual de vaciado para el tanque 3                        |
| CONTADOR_ACTUAL_PROCESO       | OUTPUT   | WORD | Cantidad de veces que se ha repetido el proceso                  |
| CONTADOR_VECES_SISTEMA        | INPUT    | CTU  | Contador para la cantidad de veces que se repite el proceso      |
|                               |          |      |                                                                  |

### Diagrama de Actividades
### Programación en Ladder
## Etapa de Desarrollo
## Etapa de Implementación

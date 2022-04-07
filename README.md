- [Etapa de Diseño](#etapadediseño)
    - [Definición de Variables](#definiciondevariables)
    - [Diagrama de Actividades](#diagramadeactividades)
    - [Programación en Ladder](#programacionenladder)
- [Etapa de Desarrollo e Implementación](#etapadesarrolloeimplementacion)

Carlos Gutierrez
Robinson Cely
Johan Rubio

# Etapa de Diseño

Se procedió a realizar el diseño del sistema automatizado a partir de los temas vistos
en clase,ademas de iniciar un proceso de ideacion e identificacion sobre como abordar el problema, en primer lugar se estableció cada una de las variables necesarias, dividiendolas en tipo boleanas siendo entradas como relays internos, luego las tipos TON, Time refiriendose a contadores que se usaran en el sistema, para simular entradas de sensores, finalmente las tipo Time

## Definición de Variables
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
| PAUSA_SYSTEMA                 | INPUT    | BOOL | Boton de pausa temporal del sistema                              |
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
| TIEMPO_ACTUAL_LLENADO         | OUTPUT   | TIME | Tiempo actual de llenado de los tanques 1 y 2                    |
| TIEMPO_ACTUAL_MEZCLADORA      | OUTPUT   | TIME | Tiempo actual de mezclado en el tanque 3                         |
| TIEMPO_ACTUAL_VACIADO_1_2     | OUTPUT   | TIME | Tiempo actual de vaciado para los tanques 1 y 2                  |
| TIEMPO_ACTUAL_VACIADO_3       | OUTPUT   | TIME | Tiempo actual de vaciado para el tanque 3                        |
| CONTADOR_ACTUAL_PROCESO       | OUTPUT   | WORD | Cantidad de veces que se ha repetido el proceso                  |
| CONTADOR_VECES_SISTEMA        | INPUT    | CTU  | Contador para la cantidad de veces que se repite el proceso      |
|                               |          |      |                                                                  |

## Diagrama funcional
En el diagrama de actvidades, iniciamos identificando los procesos clave del sistema. Como el sistema es un proceso lineal repetitivo usamos la representacion de tipo funcional, de esta manera aclaramos el flujo del proceso.
Tenemos que el proceso es inicia cuando las motobombas 1 y 2 son activadas, luego verificamos si los tanques han sido llenados, luego de estar llenos los tanques abrimos las valvulas y encendemos el sensor de nivel de nivel del tanque 3, en caso de estar lleno iniciamos la mezcladora y como paso funcional final abrimos la valvula del tanque 3.
<p align="center">
  <img width="139" height="600" src="https://raw.githubusercontent.com/SadPac/Parcial2/main/Diagrama.png">
</p>


## Diagrama de actividades
<p align="center">
  <img width="1399" height="750" src="https://raw.githubusercontent.com/SadPac/Parcial2/main/tablascrum.png">
</p>




# Etapa de Desarrollo
La etapa de desarrollo se dividio en 2 partes, la programacion en lenguaje Ladder tanto en Codesys como en OpenPlc

## Pasos programacion Ladder

1. Inicio del sistema, verificamos si esta presionado el boton stop y si el boton start esta iniciado. La variable Continuacion_Systema se encarga de hacer reinicio de variables para volver a iniciar el proceso, esta es usada en el reinicio de sistema cuando se cuenta una ejecucion
2. Verificamos si las bombas fueron iniciadas y comenzamos el proceso de conteo, despues de 10 segundos activamos los 2 sensores de llenado de cada uno de los tanques
3. Verificamos si los sensores estan activados, apagamos las motobombas, luego usamos la variable "Continuacion_systema" para preparar el reinicio con conteo, finalmente encendemos las valvulas de los 2 tanques
4. Verificamos si las valvulas fueron encendidas, y comenzamos a contar 10 segundos refiriendonos a el vaciado de los tanques, cuando pasan los 10 segundos, apagamos los sensores de llenado y cerramos las valvulas, por ultimo le decimos al sensor del tanque 3 que ya se vaciaron los tanques anteriores
5. Verificamos si el sensor de llenado esta activo, e iniciamos la mezcladora del tanque 3, en caso de que la mezcladora este activa, se inicia el conteo de 100 segundos, despues de ese tiempo apagamos la mezcladora y utilizamos el internal relay "apagado_mezcladora" para mantener el estado
6. Cuando se apaga la mezcladora abrimos la valvula de vaciado. En el momento de abrir la valvula de vaciado del tanque 3, esperamos 20 segundos, despues de los 20 segundos, cerramos la valvula de vaciado y apagamos el sensor de llenado, luego avisamos por medio de "IR_CONTAR" que se debe contar un ciclo
7. Este bloque es encargado de hacer el conteo de cuantas veces se ha realizado el proceso, y en caso de que el proceso llegue a 10 veces, se para todo el proceso, Al mismo tiempo usamos el estado del boton stop para, cuando se presione, hagamos el reinicio completo del sistema
8. Cuando verifiquemos que debemos contar, encendemos "IR_REINICIO SISTEMA" para comenzar un nuevo ciclo, sin reiniciar la cantidad de conteos que lleva el sistema


## Programación en Ladder

### Codesys
A continuacion se adjuntan capturas de pantalla de como fue diseñado el sistema en Codesys
![1](https://github.com/SadPac/Parcial2/blob/main/codesys1.jpg?raw=true)
![2](https://github.com/SadPac/Parcial2/blob/main/codesys2.jpg?raw=true)
![3](https://github.com/SadPac/Parcial2/blob/main/codesys3.jpg?raw=true)
![4](https://github.com/SadPac/Parcial2/blob/main/codesys4.jpg?raw=true)
![5](https://github.com/SadPac/Parcial2/blob/main/codesys5.jpg?raw=true)
### OPENPLC
A continuacion se adjuntan capturas de pantalla de como fue diseñado el sistema en OpenPlc
![1](https://github.com/SadPac/Parcial2/blob/main/openplc1.jpg?raw=true)
![2](https://github.com/SadPac/Parcial2/blob/main/openplc2.jpg?raw=true)
![3](https://github.com/SadPac/Parcial2/blob/main/openplc3.jpg?raw=true)
![4](https://github.com/SadPac/Parcial2/blob/main/openplc4.jpg?raw=true)



## Diagrama HMI Codesys
En el diagrama, se simulo el llenado de los tanques por medio de cambio de color de las tuberias, ademas de mostrar por medio de leds, los diferentes estados tanto de los sensores como de los actuadores, es decir cuando el sensor de nivel de algun tanque fue activado, se ecendera su correspondiente led, ademas, se implementaron 3 botones, uno para inicio del proceso, otro para la pausa momentanea y otro del reinicio total del sistema.
<p align="center">
  <img width="1399" height="750" src="https://github.com/SadPac/Parcial2/blob/main/HMI.jpg?raw=true">
</p>

## Diagrama circuito electrico
El circuito fue diagramado por medio de TinkerCad, haciendo uso de su capacidad de replicar las conexione de una manera mas presentable y distinguible, ademas de mostrar como se veria teoricamente el montaje del sistema simulado.
<p align="center">
  <img width="1399" height="750" src="https://github.com/SadPac/Parcial2/blob/main/Diagrama%20de%20circuito.jpeg?raw=true">
</p>

# Etapa de implementacion







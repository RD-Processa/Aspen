## Reexpedición de tarjeta anónima

Asocia un nuevo número de tarjeta a un cliente que ya existe

Verbo | Endpoint | Requiere autenticación
:---: | -------- | :------------:
POST | /app/ext/TUP/Comfahuila/Finance/AnonymousCards/Reissues | [x]

## Precondiciones

- El cliente debe existir (DocType y DocNumber)
- El número de tarjeta debe existir (Pan)
- El número de tarjeta no debe tener asociado un cliente (Pan, DocType y DocNumber)
- El cliente debe tener asociada una tarjeta (Pan, DocType y DocNumber)

## Datos de la solicitud

```json
{
	"DocNumber": "201810180044",
	"DocType": "CE",
	"Pan": "************3292630",
	"CorrelationalId": "aeccc385-19de-4b1d-aa3a-df44d6981564"
}
```

### Valores de la solicitud

Campo | Tipo de dato | Descripción | Requerido
:---: | :--------: | ------------ | :-----:
Correlationalld | String | Identificador unívoco de la solicitud. Debe ser único por cada  solicitud/request  que se haga al servicio. | [x]
DocNumber | String | Número de documento del cliente que se va a asociar con el nuevo número de la tarjeta. | [x]
DocType | String | Tipo de documento del cliente que se va a asociar con el nuevo número de la tarjeta.
Pan | String | Nuevo número de tarjeta que se va a asociar con el cliente. | [x]

## Datos de la respuesta

```json
{
	"Date": "2018-10-22T11:13:44.6013424-05:00",
	"CorrelationalId": "aeccc385-19de-4b1d-aa3a-df44d6981564",
	"ResponseCode": 200.0,
	"ResponseMessage": "",
	"Successful": true,
	"Empty": false,
	"MachineName": "PDP017"
}
```

### Valores de la respuesta

Campo | Tipo de dato | Descripción
:---: | :--------: | ------------
Correlationalld | String | Identificador de la solicitud para la que se genera la respuesta.
ResponseCode | lnt | Entero que representa el resultado de la operación. Por convención se utilizan los códigos de respuesta HTTP para facilitar su comprensión. En general un código en el rango 200 indica que la operación terminó satisfactoriamente.
ResponseMessage | String | Describe el código de respuesta en ResponseCode.
Successful | Bool | Cuando es true indica que la ejecución de la operación terminó de forma satisfactoria.
Empty | Bool | Para uso interno. No es necesario procesar esta información.
MachineName | String | Para uso interno. No es necesario procesar esta información.
Date | DateTime | Fecha y hora que en que se procesó la operación.

## Información relacionada

- [Personalización de tarjeta anónima](Comfahuila-AnonimousCardReissue.md)
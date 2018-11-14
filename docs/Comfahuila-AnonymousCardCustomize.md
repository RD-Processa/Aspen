# Comfamiliar Huila
## Personalización de tarjeta anónima

Asocia una tarjeta anónima con un cliente.

Verbo | Endpoint | Requiere autenticación
:---: | -------- | :------------:
POST | /app/ext/TUP/Comfahuila/Finance/AnonymousCards/Customizations | [x]

## Precondiciones

- El cliente no debe existir (DocType y DocNumber)
- El número de tarjeta debe existir (Pan)
- El número de tarjeta no debe tener asociado un cliente (Pan, DocType y DocNumber)
- El identificador del cliente no debe existir (PersonCode)

## Datos de la solicitud

```json
{
	"CorrelationalId": "298ccbb0-04fb-44bb-affa-c53dbc41a988",
	"DocNumber": "201810180045",
	"DocType": "CE",
	"Pan": "6094580032681230000",
	"FirstName": "ALEX",
	"LastName": "MATRINEZ REDONDO",
	"PersonCode": "201810180045",
	"CardLabel": "ALEX MATRINEZ REDONDO",
	"Address": "TV 9 85 D 15",
	"Telephone": "3015324",
	"Email": "ENF.PEP_19@gmail.com",
	"CityCode": "11001",
}
```

### Valores de la solicitud

Campo | Tipo de dato | Descripción | Requerido
:---: | :--------: | ------------ | :-----:
DocNumber | String | Número de documento del cliente al que se asocia la tarjeta. | [x]
DocType | String | Tipo de documento del cliente al que se asocia la tarjeta. Cualquier valor de "Acrónimo" en la tabla de tipos de documento.
Pan | String | Número de tarjeta que se debe asociar con el cliente. | [x]
FirstName | String | Nombre(s) del cliente que va a asociar con la tarjeta. | [x]
LastName | String | Apellido(s) del cliente que se va a asociar con la  tarjeta. | [x]
PersonCode | String | Código que se debe establecer para identificar al cliente en el emisor. | [x]
CardLabel | String | Nombre que se utilizará  para imprimir en el plástico. Si no se envía se concatenan los campos de nombres y apellidos.
Address | String | Dirección de contacto del cliente.
Telephone | String | Número de teléfono de contacto del cliente.
Email | String | Dirección de correo electrónico del cliente.
CityCode | String | Identificación del  municipio de residencia del cliente de acuerdo a los códigos del Departamento Administrativo Nacional de Estadística DANE. | [x]

## Datos de la respuesta

```json
{
	"AuthorizationNumber": "",
	"Date": "2018-10-22T11:12:33.9132313-05:00",
	"CorrelationalId": "298ccbb0-04fb-44bb-affa-c53dbc41a988",
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
ResponseCode | Int | Entero que representa el resultado de la operación. Por convención se utilizan los códigos de respuesta HTTP para facilitar su comprensión. En general un código en el rango 200 indica que la operación terminó satisfactoriamente.
ResponseMessage | String | Describe el código de respuesta en ResponseCode.
Successful | Bool | Cuando es true indica que la ejecución de la operación terminó de forma satisfactoria.
Empty | Bool | Para uso interno. No es necesario procesar esta información.
MachineName | String | Para uso interno. No es necesario procesar esta información.
AuthorizationNumber | String | Número de autorización emitido para la operación, o ceros si la operación no se pudo completar.
Date | DateTime | Fecha y hora que en que se procesó la operación.

## Anexos

### Tipos de documento

Acrónimos a usar en el campo DocType de los datos de solicitud.

Acrónimo | Descripción | ¿Es valor predeterminado?
:------: | :---------: | :----------------------:
CC | CÉDULA DE CIUDADANÍA | Si
CE | CÉDULA DE EXTRANJERÍA | No
CF | CODIGO DE FENALCO | No
DI | PASE  DIPLOMATICO | No
NI | No. ÚNICO TRIBUTARIO | No
NJ | NIT EMPRESARIAL | No
NT | NIT PERSONA NATURAL | No
NU | No. ÚNICO DE IDENTIFICACIÓN | No
PS | PASAPORTE | No
RC | REGISTRO CIVIL | No
TI | TARJETA DE IDENTIDAD | No

## Información relacionada

- [Reexpedición de tarjeta anónima](Comfahuila-AnonimousCardReissue.md)

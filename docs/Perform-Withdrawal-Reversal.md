# Reverso: Retiro con token transaccional

Procesa una solicitud financiera de reverso de un retiro.

| Verbo | Endpoint                                      | Requiere autenticación |
| :---: | --------------------------------------------- | :--------------------: |
| PATCH  | http://localhost/api/app/financial/withdrawal |          [ Si ]           |

[^Segmentos de URL]: La información entre corchetes en la URL se denomina segmentos de URL y aplican solo para algunas operaciones. Cuando aparezcan en un ejemplo, deben ser reemplazados por sus valores correspondientes omitiendo los corchetes. Por ejemplo, sin en la URL de ejemplo apareciera http://localhost/api/operation/value/{value}, para establecer el valor de  `value` en la solicitud a la cadena `abc`, la URL final se vería de la siguiente forma: http://localhost/api/operation/value/abc 

## Datos de la solicitud (body)

```json
{
  "TransactionId": "OriginalNonceValue",
  "DocType": "CC",
  "DocNumber": "123456789",
  "AccountType": "80",
  "Amount": 99999
}
```

### Valores de la solicitud

Campo | Tipo de dato | Descripción | Requerido
:---: | :--------: | ------------ | :-----:
TransactionId | string | Identificador de la transacción que se  intenta reversar. Corresponde con el valor del campo [Nonce](JWT-Request#Nonce) de la solicitud en la transacción original de retiro. | [ Si ]
DocType | string | [Tipo de documento](Inquiries-CustomerAccounts.md#DocTypes) del usuario para el que se procesó la transacción original. | [ Si ]
DocNumber | string | Número de documento del usuario para el que se procesó la transacción original. | [ Si ]
AccountType | string | Identificador del tipo de cuenta de la transacción original. | [ Si ]
Amount | int | Valor de la transacción original. | [ Si ] 
Tags | string | Colección de claves y valores con información asociada, que se enviaron en la transacción original [Tags](#tags). | [Opcional]

<a name="Tags"></a>
### Tags
Una colección de claves y valores (ambos de tipo string), que representan información relacionada con la transacción. Todos los valores son opcionales, pero si se envian, deben cumplir con los siguientes formatos:

Claves admitidas | Descripción | Formato admitido | Requerido
:---: | -------- | :---: | :-----:  
TerminalId | Código que el adquiriente asigna al punto dentro del comercio desde donde se realiza la transacción. | ^\w{1,8}$ | [ No ]
CardAcceptorId | Código que el adquiriente asigna al comercio desde donde se realiza la transacción. | ^\w{1,15}$ | [ No ]
CustomerGroup | Identificador del grupo familiar al que pertenece el afiliado. | ^\d{1,2}$ | [ No ]
Pan | Últimos 4 dígitos del número de tarjeta utilizado para la transacción. | ^\d{4}$ | [ No ]

> Cuando se utiliza el campo Tags en una solicitud, es necesario establecer la cabecera [Content-Type]( https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) al valor application/json

#### Ejemplo de Tags

```json
{
  "TerminalId": "XXXXXXXX",
  "CardAcceptorId": "XXXXXXXXXXXXXXX",
  "CustomerGroup": "00",
  "Pan": "1234"
}
```


## Datos de la respuesta

> Si al procesar la respuesta del servicio está utilizando un serializador que distinga mayúsculas y minúsculas, tenga en cuenta que Aspen genera todas sus respuestas utilizando el formato conocido como [LowerCamelCase](https://en.wikipedia.org/wiki/Camel_case)

Esta operación no retorna información adicional al código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html). Si la respuesta no es `HttpStatus` 200, en el campo  `ReasonPhrase` de la respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación.

### Valores de respuesta más utilizados

HttpStatus | Tipo | Descripción
:---: | :--------: | ------------
200 | int | La solicitud se proceso satisfactoriamente. 
400 | int | La información proporcionada para la transacción original está errada. El campo `ReasonPhrase` contiene un mensaje que describe de forma detallada los datos que no pudieron ser procesados.
404 | int | No se encontró la transacción original. 

## Información relacionada

- [Tipos de documentos reconocidos](Inquiries-CustomerAccounts.md#DocTypes)

- [Pago con token](Perform-Payment.md)

- [Retiro con token](Perform-Withdrawal.md)

- [Reverso: Compra con token transaccional](Perform-Payment-Reversal.md)

- [Mensajes de respuesta](Responses.md)

# Validación de un token de pago

Permite a un adquirente o comercio, verificar la validez de un token transaccional que fue generado a través de la aplicación de movilidad del emisor o enviado a un tarjetahabiente a través de un mensaje SMS u otro medio.

> Esta operación no conecta con el autorizador financiero. Se expone aquí con la intención de facilitar la comprobación (generalmente a través de la automatización) de un token generado o enviado a un tarjetahabiente. 

Verbo | Endpoint | Requiere autenticación
:---: | -------- | :------------:
PUT | http://localhost/api/app/tokens/{Token} | [x]

> [^Segmentos de URL]: La información entre corchetes en la URL se denomina segmentos de URL y aplican solo para algunas operaciones. Cuando aparezcan en un ejemplo, deben ser reemplazados por sus valores correspondientes omitiendo los corchetes. Por ejemplo, sin en la URL de ejemplo apareciera http://localhost/api/operation/value/{value}, para establecer el valor de  `value` en la solicitud a la cadena `abc`, la URL final se vería de la siguiente forma: http://localhost/api/operation/value/abc 

## Datos de la solicitud

```json
{
  "DocType": "CC",
  "DocNumber": "0000000000",
  "Metadata": "RANDOM_DATA_BY_ACQUIRER",
  "Amount" : 12345
}
```

### Valores de la solicitud

Campo | Tipo de dato | Descripción | Requerido
:---: | :--------: | ------------ | :-----:
{Token} | string | Token de pago que se desea verificar. Valor en la URL sin corchetes | [ Si ]
DocType | string | Tipo de documento del usuario para el que se genera el token | [ Si ]
DocNumber | string | Número de documento del usuario para el que se genera el token | [ Si ]
Amount | int | Valor de la operación financiera para el que se intenta comprobar la validez del token. | [ Si ]
Metadata | string | Metadatos asociados personalizados para el [TPS](Tokenization.md#tps) | [ No ]

## Datos de la respuesta

Código de estado de HTTP de acuerdo con la especificación [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

> Si al procesar la respuesta del servicio está utilizando un serializador que distinga mayúsculas y minúsculas, tenga en cuenta que Aspen genera todas sus respuestas utilizando el formato conocido como [LowerCamelCase](https://en.wikipedia.org/wiki/Camel_case)

### Valores de respuesta más utilizados

HttpStatus | Tipo de dato | Descripción
:---: | :--------: | ------------
200 | int | El token de pago se validó satisfactoriamente
404 | int | El token de pago no existe, no es válido o ya expiró

## Información relacionada

- [Tokenización: Concepto general](Tokenization.md)

- [Generación de un token transaccional](Generate-PaymentToken.md)

- [Proveedor de servicios de tokens (TSP)](Tokenization.md#tps)

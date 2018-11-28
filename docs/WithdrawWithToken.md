# Retiro con token de pago

Permite a un adquirente o comercio, realizar un retiro en efectivo mediante el uso de un token de pago que fue generado a través de la aplicación de movilidad del emisor.

> Cuando la validación es exitosa, se hace un débito en la cuenta asociada con el token de pago.

Verbo | Endpoint | Requiere autenticación
:---: | -------- | :------------:
PUT | http://localhost/api/app/tokens/{Token} | [x]

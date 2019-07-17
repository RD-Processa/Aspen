# Conceptos importantes

## Segmentos de URL

La información entre corchetes en los ejemplos de URL se denomina `segmentos` y podría aplicar para algunas operaciones. Cuando aparezcan en algún ejemplo, los segmentos deben ser reemplazados por sus valores correspondientes omitiendo los corchetes. Por ejemplo, si en la URL de ejemplo apareciera http://localhost/api/operation/value/{value}, para establecer el valor de `value` en la solicitud a la cadena `abc`, la URL final se verÃ­a de la siguiente forma: http://localhost/api/operation/value/abc

## Distinción de mayúsculas y minúsculas en respuestas

Si al procesar la respuesta del servicio está utilizando un [serializador](https://en.wikipedia.org/wiki/Serialization) que distinga mayúsculas y minúsculas, tenga en cuenta que Aspen genera todas sus respuestas utilizando el formato conocido como [LowerCamelCase](https://en.wikipedia.org/wiki/Camel_case)

## Identificador de eventos

Si la respuesta a cualquier operación es diferente a un HttpStatus 200 de acuerdo con el [RFC 2616](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html), en el campo ReasonPhrase de la respuesta encontrará un mensaje que describe de forma detallada el resultado de la operación. Este campo incluye un identificador de evento con la forma `EventId: (0000000)` que podrí­a utilizar si necesita personalizar alguna respuesta utilizando una expresión regular donde se busque la palabra EventId, seguida de dos puntos y una seguidilla de dígitos. La siguiente expresión regular puede servirle como inspiración, pero tendrá que ajustarla de acuerdo a su lenguaje de programación preferido.

```c#
string reasonPhrase = "Lorem ipsum dolor sit amet, consectetur adipiscing elit EventId: (9999999)";
string pattern = @"(EventId:\s+\((?<event_id>\d*)\))";
RegexOptions options = RegexOptions.IgnoreCase | RegexOptions.Singleline;
Match match = Regex.Match(reasonPhrase, pattern, options);
if (match.Success)
{
	string eventId = match.Groups["event_id"].Value;
	Console.WriteLine(eventId);
}
```

Puede encontrar mayor detalle al respecto de los identificadores de eventos en la sección de [Mensajes de respuesta](Responses.md)
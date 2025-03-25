# Clarity Value Types

When specifying function arguments or decoding values, you can use the following Clarity value types:

| Type | Description | Example |
|------|-------------|---------|
| `uint` | Unsigned integer | `{"type": "uint", "value": "123"}` |
| `int` | Signed integer | `{"type": "int", "value": "-123"}` |
| `bool` | Boolean | `{"type": "bool", "value": true}` |
| `principal` | Principal (address) | `{"type": "principal", "value": "ST252TFQ08T74ZZ6XK426TQNV4EXF1D4RMTTNCWFA"}` |
| `buffer` | Byte buffer | `{"type": "buffer", "value": "0x68656c6c6f"}` |
| `string` or `stringascii` | ASCII string | `{"type": "string", "value": "hello"}` |
| `stringutf8` | UTF-8 string | `{"type": "stringutf8", "value": "hello 世界"}` |
| `list` | List of values | `{"type": "list", "value": [{"type": "uint", "value": "1"}, {"type": "uint", "value": "2"}]}` |
| `tuple` | Key-value pairs | `{"type": "tuple", "value": {"key1": {"type": "uint", "value": "1"}}}` |
| `none` | Optional none | `{"type": "none"}` |
| `some` or `optional` | Optional some | `{"type": "some", "value": {"type": "uint", "value": "123"}}` |
| `ok` or `responseok` | Response OK | `{"type": "ok", "value": {"type": "uint", "value": "123"}}` |
| `err` or `responseerr` | Response Error | `{"type": "err", "value": {"type": "uint", "value": "123"}}` |

# openapi-builder

openapi-builder is a library that build openapi schema and definations from a given GO value(struct/array/...).

## Example

```go
type Inner struct {
    Count int `json:"count,omitempty"`
}

type SimpleStruct struct {
    Name  string      `json:"name,omitempty"`
    Value interface{} `json:"value,omitempty"`
}

schema := Build(SimpleStruct{Value: Inner{}})
fmt.Println(JsonStr(schema))
// Output:
// {
//   "allOf": [
//    {
//     "$ref": "#/definitions/openapibuilder.SimpleStruct"
//    },
//    {
//     "type": "object",
//     "properties": {
//      "value": {
//       "$ref": "#/definitions/openapibuilder.Inner"
//      }
//     }
//    }
//   ],
//   "definitions": {
//    "openapibuilder.Inner": {
//     "type": "object",
//     "properties": {
//      "count": {
//       "type": "integer",
//       "format": "int64"
//      }
//     }
//    },
//    "openapibuilder.SimpleStruct": {
//     "type": "object",
//     "properties": {
//      "name": {
//       "type": "string"
//      },
//      "value": {
//       "type": "object"
//      }
//     }
//    }
//   }
//  }
```

# jsondiff

Equal takes as its input two JSON byte slices and causes tests to fail as appropriate
if the JSON doesn't match. Values are considered to be equivalent if they are:
  1. Both the same data type and values match
  2. One value is nil and the other is the default value for its data type. This is done since Go may
     not serialize JSON the same way as other languages. Go is very strict and consistent, but the JSON
     you have may not be. To make that easier, these values are considered equal:
     	a. "" and nil
     	b. 0.0 and nil
     	c. false and nil
     	d. empty slice and nil

According to the JSON spec, there are 6 different types

| JSON data type | Go equivalent |
|----------------|------------------------|
| string         | string                 |
| number         | float64                |
| object         | map[string]interface{} | 
| array          | slice (any data)       |
| bool           | bool                   | 
| null           | nil                    |             
## Usage
```Go
import (
  "github.com/mypricehealth/jsonassert"
)

func TestJSON(t *testing.T) {
  json1 := []byte(`{"a": "1", "b": ""}`)
  json2 := []byte(`{"a": "1"})`)
  jsonassert.Equal(t, json1, json2)
}
```

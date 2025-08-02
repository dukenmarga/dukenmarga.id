---
# Common-Defined
title: "Convert map[string]interface{} to Struct as Generic Function in Go"
date: 2025-08-02T00:00:00+07:00
lastmod: 2025-08-02T00:00:00+07:00
draft: false
tags: ["go"]
categories: ["Programming", "index"]
author: "Duken Marga"

# User-Defined
# You can close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
# You can also define another contentCopyright
contentCopyright: '<a rel="license noopener" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank">CC BY-NC-ND 4.0</a>'
reward: false
mathjax: true
---

### Several Methods to Convert

There are several methods to convert `map[string]interface{}` to a `struct`
in Go.
- Using `reflect`. This is the fastest. But, it will produce complicated long
code. If not well coded, it will have problems with
nested map. I will not discuss this method.
- **Using `json` standard library**. First we marshal the map as json string
and after that unmarshal it as a struct. **This is what I will be talking about.**
It is slow, but reliable. Nested map are handled performantly.
- Using external library such as  [mitchellh/mapstructure](https://github.com/mitchellh/mapstructure). It is not maintained anymore. But, you can still use
it, since it is stable and has achieved its original intention.
- Using simple loop and check one by one using `switch`-`case`. You need to
hard-coded all the map properties, hence it's not practical since it
can't be reused for different struct type.

### Converting to Struct

The code below is the original non-generic method that can be used to
convert any map to string. Don't forget to include the json tag as per your
intention, so the `json` library can convert it correctly.

Try it on Go Playground: https://go.dev/play/p/gSKSk_t16MI
```go
package main

import (
	"encoding/json"
	"fmt"
)


type Profile struct {
	Name struct {
		First string `json:"first"`
		Last string  `json:"last"`
	} `json:"name"`
	PhoneNumber string   `json:"phoneNumber"`
	Status      string   `json:"status"`
	Emails      []string `json:"emails"`	
}

func main() {
	mapping := map[string]any{
		"name": map[string]string{
			"first": "Duken",
			"last": "Marga",
		},
		"phoneNumber": "08000000000",
		"status": "active",
		"emails": []string{
			"myemail@gmail.com",
			"my2ndemail@gmail.com",
		},
	}

	// Marshal the map to a JSON byte slice
	jsonBytes, err := json.Marshal(mapping)
	if err != nil {
		fmt.Printf("json.Marshal: %v", err)
	}

	// Inspecting json
	fmt.Printf("jsonBytes: %+v\n", string(jsonBytes))

	// Unmarshal the JSON byte slice into the struct
	var myStruct Profile
	err = json.Unmarshal(jsonBytes, &myStruct)
	if err != nil {
		fmt.Printf("json.Unmarshal: %v", err)
	}

	fmt.Printf("Struct: %+v\n", myStruct)
}

Output:
jsonBytes: {"emails":["myemail@gmail.com","my2ndemail@gmail.com"],"name":{"first":"Duken","last":"Marga"},"phoneNumber":"08000000000","status":"active"}
Struct: {Name:{First:Duken Last:Marga} PhoneNumber:08000000000 Status:active Emails:[myemail@gmail.com my2ndemail@gmail.com]}
```

### Generic Function

But, what if you need to reuse this code into a function that can handle
any struct type? We can utilize generic in Go. This is a modified version
using generic function. Original map is not necessarily `map[string]any`,
but it literally can use `map[any]any`. But, the former is more common.

Try on Go Playground: https://go.dev/play/p/_qnY0HqLABO
```go
package main

import (
	"encoding/json"
	"fmt"
)

type Profile struct {
	Name struct {
		First string `json:"first"`
		Last  string `json:"last"`
	} `json:"name"`
	PhoneNumber string   `json:"phoneNumber"`
	Status      string   `json:"status"`
	Emails      []string `json:"emails"`
}

func main() {
	mapping := map[string]any{
		"name": map[string]string{
			"first": "Duken",
			"last":  "Marga",
		},
		"phoneNumber": "08000000000",
		"status":      "active",
		"emails": []string{
			"myemail@gmail.com",
			"my2ndemail@gmail.com",
		},
	}

	// Profile is passed as the type
	// Now myStruct type is Profile
	myStruct, err := ConvertTo[Profile](mapping)
	if err != nil {
		fmt.Printf("Error converting to struct: %v", err)
	}

	fmt.Printf("Struct: %+v\n", myStruct)
}

// Generic function to convert map to any struct
func ConvertTo[T any](mapping map[string]any) (T, error) {
	var myStruct T

	// Marshal the map to a JSON byte slice
	jsonBytes, err := json.Marshal(mapping)
	if err != nil {
		fmt.Printf("json.Marshal: %v", err)
	}

	// Unmarshal the JSON byte slice into the struct
	err = json.Unmarshal(jsonBytes, &myStruct)
	if err != nil {
		fmt.Printf("json.Unmarshal: %v", err)
	}

	return myStruct, nil
}

Output:
Struct: {Name:{First:Duken Last:Marga} PhoneNumber:08000000000 Status:active Emails:[myemail@gmail.com my2ndemail@gmail.com]}
```

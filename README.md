# env
Tag-based environment configuration for structs.

[![Godoc](https://godoc.org/github.com/nicklanng/env?status.svg)](https://godoc.org/github.com/nicklanng/env)
[![](https://github.com/nicklanng/env/workflows/CI/badge.svg)](https://github.com/nicklanng/env/actions)
[![Go Report Card](https://goreportcard.com/badge/github.com/nicklanng/env)](https://goreportcard.com/report/github.com/nicklanng/env)

## Installation

``` bash
$ go get -u github.com/nicklanng/env
```

## Usage

``` go
package main

import (
	"fmt"
	"log"
	"time"

	"github.com/nicklanng/env"
)

type config struct {
	Secret            []byte        `env:"SECRET" required:"true"`
	Region            string        `env:"REGION"`
	Port              int           `env:"PORT" required:"true"`
	Peers             []string      `env:"PEERS"`
	ConnectionTimeout time.Duration `env:"TIMEOUT" default:"10s"`
}

func main() {
	c := config{}
	if err := env.Set(&c); err != nil {
		log.Fatal(err)
	}

	...
}
```

``` bash
$ ID=1 SECRET=shh PORT=1234 PEERS=localhost:1235,localhost:1236 TIMEOUT=5s go run main.go
```

## Supported field types

- `bool` and `[]bool`
- `string` and `[]string`
- `[]byte`
- `int`, `int8`, `int16`, `int32`, `int64`, `[]int`, `[]int8`, `[]int16`, `[]int32`, and `[]int64`
- `uint`, `uint8`, `uint16`, `uint32`, `uint64`, `[]uint`, `[]uint8`, `[]uint16`, `[]uint32`, and `[]uint64`
- `float32`, `float64`, `[]float32`, and `[]float64`
- `time.Duration` and `[]time.Duration`

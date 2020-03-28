# playground-links
links of golang playgrounds I've used to test something

# testing writing to an out of scope var is thread safe
https://play.golang.org/p/KITUN-ItcsP
```
package main

import (
	"fmt"
	"time"
)

func main() {
	vs := []string{"init"}
	go func() {
		for {
			vs = []string{"first"}
			fmt.Println("first done", vs)
			time.Sleep(500 * time.Microsecond)
		}
	}()
	go func() {
		for {

			vs = []string{"second"}
			fmt.Println("second done", vs)
			time.Sleep(500 * time.Microsecond)
		}
	}()
	for i := 0; i < 5; i++ {
		fmt.Println(i, vs)
		time.Sleep(1 * time.Millisecond)
	}
}
```

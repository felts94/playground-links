# playground-links
links of golang playgrounds I've used to test something

# testing writing to an out of scope var is thread safe
https://play.golang.org/p/m3hfAtTfMhN
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

# pass by copy sanity check
https://play.golang.org/p/2jDcMItVHOJ

```
package main

import "fmt"

type Bar struct {
	Zap string
}

func main() {
	bar := Bar{Zap: "first"}
	foo(bar)
	fmt.Println(bar.Zap)
}

func foo(bar Bar) {
	fmt.Println(bar.Zap)
	bar.Zap = "second"
	fmt.Println(bar.Zap)
}
```

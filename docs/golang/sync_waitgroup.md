# sync.WaitGroup in Go

`sync.WaitGroup` is a synchronization primitive in Go used to **wait for a collection of goroutines to finish executing**.

It is commonly used when:
- launching multiple goroutines
- you need to block until all of them complete
- you do NOT need to return values directly (channels are used for that)

---

## Why WaitGroup is needed

Goroutines run asynchronously. Without synchronization, the main function may exit before goroutines finish.

```
go doWork()
fmt.Println("main done") // may execute before doWork finishes

```
## Basic Usage Pattern
```go
var wg sync.WaitGroup
wg.Add(1)

go func() {
    defer wg.Done()
    // work here
}()

wg.Wait()
```

## Single GoRoutine

```go

package main

import (
    "fmt"
    "sync"
)

func main() {
    var wg sync.WaitGroup

    wg.Add(1)

    go func() {
        defer wg.Done()
        fmt.Println("Hello from goroutine")
    }()

    wg.Wait()
    fmt.Println("All goroutines finished")
}
```
## Multiple Goroutines
```go
var wg sync.WaitGroup

for i := 0; i < 5; i++ {
    wg.Add(1)

    go func(i int) {
        defer wg.Done()
        fmt.Println("Worker", i)
    }(i)
}

wg.Wait()
fmt.Println("All workers done")
```
## Waiting for Http Calls

```go

var wg sync.WaitGroup

urls := []string{
    "https://example.com",
    "https://golang.org",
}

for _, url := range urls {
    wg.Add(1)

    go func(u string) {
        defer wg.Done()
        fmt.Println("Fetching", u)
    }(url)
}

wg.Wait()
```
## WaitGroup with channels

```go

var wg sync.WaitGroup
results := make(chan int, 5)

for i := 0; i < 5; i++ {
    wg.Add(1)

    go func(i int) {
        defer wg.Done()
        results <- i * 2
    }(i)
}

go func() {
    wg.Wait()
    close(results)
}()

for r := range results {
    fmt.Println("Result:", r)
}
```
## Other details

### Do not call Add() inside goroutines

```go
go func() {
  wg.Add(1)  // WRONG
}()

```

### Use defer wg.Done()

Ensures Done() is called even if the function returns early.


## Other Links

[Go Official Docs] (https://pkg.go.dev/sync#WaitGroup)


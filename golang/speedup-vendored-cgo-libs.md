# Speedup Vendored cgo Libaries

`go run` took a long time start my application when vendoring was enabled. Turns out `go run` does not cache builds and I was compiling sqlite3 every time. 

The solution was to use `go install` which does cache data.

```
go install ./vendor/github.com/mattn/go-sqlite3/
```

After this `go run` was fast as always.
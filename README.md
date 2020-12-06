Try Go WebAssembly follow the instructions from [Go WebAssembly](https://github.com/golang/go/wiki/WebAssembly).

## Steps
* Create main.go and add code
* Build wasm file by running ` GOOS=js GOARCH=wasm go build -o main.wasm` in terminal
* Copy wasm_exec.js to local directory `* Copy wasm_exec.js to local directory `
* Copy index.html to local 
```shell
cat <<EOF > index.html                                                                                                                                       
<html>
        <head>
                <meta charset="utf-8"/>
                <script src="wasm_exec.js"></script>
                <script>
                        const go = new Go();
                        WebAssembly.instantiateStreaming(fetch("main.wasm"), go.importObject).then((result) => {
                                go.run(result.instance);
                        });
                </script>
        </head>
        <body></body>                                   
        EOF
```
* Try to run `goexec 'http.ListenAndServe(`:8080`, http.FileServer(http.Dir(`.`)))'` failed
    * install goexec, `go get -u github.com/shurcooL/goexec`
    * install gogoon, ` go get github.com/shurcooL/go-goon`
  
* Run again, works, terminal blocks
* Open chrome, http://localhost:8080/index.html, and can find the output in Debugger Console(fn+F12)


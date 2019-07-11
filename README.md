### VSCode
-   setup extension -> users > settings.json
    -   go-tools
        -   `"go.toolsGopath": "/home/hadn/.go"`
    -   go-lint
        ```bash
        "go.lintFlags": [
        "--disable-all",
        "--enable=golint",
        "--exclude=exported (const|type|method|function) [\\w.]+ should have comment (\\(or a comment on this block\\) )?or be unexported",
        "--exclude=don't use ALL_CAPS in Go names; use CamelCase",
        "--exclude=(func|const|struct field|) \\w+ should be \\w+"
        ]
        ```

### Go lang
-   install
    -   `/usr/local/go/bin/go`
    -   GOROOT=/usr/local/go
-   Create Go folders
    -   `mkdir envoy`
        -   `envoy` - project folder
    -   `cd envoy`
    -   `mkdir -p {src,bin/gen,pkg}`
        -   `src` - source folder
        -   `bin` - store lib from third party
        -   `bin/gen` - store proto files which is compiled from cli `protoc`
-   GOPATH -> `export GOPATH=$(pwd)`
-   GOBIN -> `export GOPATH=$(pwd)/bin`
-   entry point -> `go run src/main.go`

#### CLI
-   go get -u 3-partied-packages

#### Pointer
-   Params are passed by values
-   `&` reference by value of RAM
-   `*` reference by address of RAM
-   require referenced Types by Address -> dont worry about pointers
    -   slices
    -   maps
    -   channels
    -   pointers
    -   functions
-   require referenced Types by Values -> beware about pointers
    -   int
    -   float
    -   string
    -   bool
    -   structs

#### Function
-   Syntax of function for multiple return value:
    ```go
    func (r receiver) f_name(params type_of_params) (return_val_1 type_of_return, return_val_2 type_of_return)
    {
        ....
    }
    ```
-   Syntax of function for single return value:
    ```go
    func (r *receiver) f_name(params type_of_params) return_val_1 type_of_return
    {
        ....
    }
    ```

#### Struct
-   Define a struct
    ```go
        type Person struct {
            // Field appears in JSON as key "first_name"
            FirstName   string  `json:"first_name"`
            // Field appears in JSON as key "last_name"
            // Field appears in xml as key "last_name"
            LastName    string  `json:"last_name" xml:"last_name"`
            // Field is omitted from the object if its value is empty
            Password    string  `json:"password,omitempty"`
            // Field appears in JSON as key "-"
            CreateAt    int     `json:"create_at,-,`
            // Field is ignored by this package
            DeleteAt    int     `json:"delete_at,-"`
        }
    ```
-   Marshal function
    ```go
    type Person struct {
        FirstName   string
        LastName    string
    }

    p := Person{
        "Bob",
        "Pickle"
    }

    // type of []byte -> string
    // _ -> ignore variable
    p1, _ := json.Marshal(p)
    fmt.Println(string(p1))
    ```
-   UnMarshal function
    ```go
    type Person struct {
        FirstName   string
        LastName    string
    }

    b := []byte(`{"FirstName":"Bob","LastName":"Pickle"}`)
    var m Person
    // type of []bytes into Person Object -> Go JSON Object
    _ := json.Unmarshal(b, &m)
    fmt.Println(m)
    fmt.Println(m.FirstName)
    fmt.Println(m.LastName)
    ```
-   reference
    -   https://golang.org/pkg/encoding/json/#Marshal

#### Interface
-   Define an interface
    ```go
    type alochym interface {
        f_name(params type_of_params) (return_val_1 type_of_return) {
            ...
        }
    }
    ```

### gRPC
-   install `protoc` command line
    -   protobuf-compiler-3.6.1-1.el7.x86_64.rpm
    -   protobuf-3.6.1-1.el7.x86_64.rpm
-   CLI
    -   `protoc --proto_path=src --go_out=bin/gen src`
-   references
    -   https://grpc.io/docs/guides/concepts/
    -   https://www.grpc.io/docs/guides/error/
    -   https://cloud.google.com/apis/design/errors
    -   https://godoc.org/google.golang.org/grpc/codes
    -   https://godoc.org/google.golang.org/grpc/status
    -   https://developers.google.com/protocol-buffers/docs/proto3
    -   https://developers.google.com/protocol-buffers/docs/encoding
    -   https://developers.google.com/protocol-buffers/docs/gotutorial
    -   https://godoc.org/github.com/golang/protobuf/proto
    -   https://developers.google.com/protocol-buffers/docs/reference/go-generated
    -   https://developers.google.com/protocol-buffers/docs/reference/google.protobuf
    -   https://developers.google.com/protocol-buffers/docs/reference/proto3-spec
    -   https://github.com/protocolbuffers/protobuf/blob/master/docs/third_party.md
    -   https://awesome-go.com/

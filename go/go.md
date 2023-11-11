
## Go Notes

Notes written while learning to code in go

### Run a go scipt
    
    go run test.go

or create an executable

    └── src
        └── hello
            ├── hello
            └── hello.go

1. Inside the hello directory run:

        go build

2. This will create an executable hello, which runs with:

       ./hello


/* Comments */


### Reserved Keywords

    break	default	func	interface	select
    case	defer	Go	map	Struct
    chan	else	Goto	package	Switch
    const	fallthrough	if	range	Type
    continue	for	import	return	Var

### Variable Declaration

    var variable_list optional_data_type;
    
    var  i, j, k int;
    var  c, ch byte;
    var  f, salary float32;
    d =  42;


### Packages in GO
There are two type of packages:
- executable package -> package main -> defines a package that can be compiled and then executed - must have a func called main as well. only package main can do that
- reusable packages -> package any_name -> defines a package that can be used as a dependency (helper code)


### Type Conversion

TO_TYPE(FROM_TYPE)

e.g. from string to a byte slice ->  []byte("Hello") -> [ 223 33 33 44 22 ]


### Pointers -> memory addresses
- Turn address into value with *address
- Turn value into address with &value


    *person VS *pointerToPerson

*person is a type description - it means we're working with a pointer to a person
*pointerToPerson is an operator - it means we want to manipulate the value the pointer is referencing


### Reference VS Value Types

Slice is a reference type - so it consists of:
- length
- capacity
- pointer to array of elems

so when

    slice := []string{a,b,c}
    
    func updateSlice(slice []string) {
        slice[0] = b
    }

the slice[0] is actually updated because although a new slice is created inside the updateSlice function,
the pointers to the values of the slice remain the same

This is what we call a reference Type. It is a reference to another data structure in memory

### Other Reference Types:
- slices
- maps
- channels
- pointers
- functions

### Value Types:
- int
- float
- string
- bool
- structs


### Interface Type vs Concrete Type

- a concrete type is something that we can create a value of this type
- only if you extend an interface to a concrete type you can create a value of this




### Useful commands

      // Get all dependencies ~~
      go get -d ./...

      // tidy up the dependencies
      go mod tidy
      
      
      // where is this module used?
      go mod why -m github.com/emicklei/go-restful
      
      
      // vendor - have your deps locally - faster build times
      go mod vendor
      
      
      // upgrade dependency and all its dependencies to the latest version
      go get -u example.com/pkg
      
      
      // List all of the modules that are dependencies of your current module, along with the latest version available for each:
      go list -m -u all

More info [here](https://go.dev/doc/modules/managing-dependencies#enable_tracking)






### %+v Printing
fmt.Printf("%+v", aStruct) -> prints out the struct's fieldNames and its values


Questions To Answer:

- fmt.Println VS fmt.Printf


__:=__ Opperator can be used to declare and assign multiple variables.
It can also be used to just asign a new value to existing variables as long as it is declaring one new variable (see code below):
```
package main
import (
 "fmt"
//  "os"
)

func main() {
  fmt.Println("lol")
power := 9000
fmt.Printf("It's over %d\n", power)

//CAN "Redeclare" variable, if you are declaring a 1 new variable, then the rest are considered to just have their values change
x, power := 9000, 9001
fmt.Printf("It's also %d%d", x, power)
}
```

### Short hand for func parameter declaration when parameters are of same type)
```
func simultaneousEq(a,b,c int, x,d int) int {
  return 4
}
```
Functions:
```
func logTests(inputNums int) {
  //retuns nothing
}

func add(a int, b, int) int {
  //returns int
  
  return a + b
}

func kamehamehaStrength(name string) (int, bool) {
  //Returns two values
  
  return 9000, True
}
```
#### Pass by value is defualt
To pass by Reference we need to get the value of the pointer and we need out func paramer to expect a pointer __(of the correct data type)__
```
goku := &Saiyan{"Goku", 9000} // &  used to get pointer value

func Super(s *Saiyan) {   //  *   used to expect a pointer   of data type Saiyan
  s.Power += 10000
}
```
\
Many funcs return multiple values and you may often not want to use all of them at once.
```
func kamehamehaStrength(name string) (int, bool) {
  //Returns two values
  
  return 9000, True
}

_ , canCellKamehameha = kamehamehaStrength("Cell")
```
\
### Defining a Struct (basics e.g. no methods):
```
type Saiyan struct {
  Name string
  Power int
}
```
\
\
Code (languages): Trailing and the opposite? - "Trailing __Commas__ " -> commas after each atribute in a structure Instantiation INCLUDING THE LAST ONE:
```
goku := Saiyan{
  Name: "Goku",
  Power: 9000,
}
```
```
goku := Saiyan{}
```
```
goku := Saiyan{}
goku.Name = "Goku"
goku.Power = 9001
```
```
goku := Saiyan{Name: "Goku"}
goku.Power = 9001
```
```
//Only use with structs that hve FEW attributes, to preserve clarity.
goku := Saiyan{"Goku",9001}
```
#### Add METHODS
```
type Saiyan struct {
  Name string
  Power int
}

func (s *Saiyan) Super () {
  s.Power += 10000
}
```
\
Calling a Struct's method
```
goku := &Saiyan("Goku", 9001}
goku.Super()
```
Use pointer - so the method actully affects __goku__'s attributes. (Pass ByRef)
\
#### Constructors
```
func newSaiyan(name string, power int) *Saiyan {  //Return ByRef
  return &Saiyan{
    Name: name,
    Power: power,
  }
}

//Return ByVal
func newSaiyan(name string, power int) Saiyan {  //Return ByRef
  return Saiyan{
    Name: name,
    Power: power,
  }
}

```
##### instantiating With "New"
__new()__
Using new() creates a ByRefer  (a pointer value) to an empty (default value) instance of the structure.
```
goku := new(Saiyan)
goku := &Saiyan{}
```
```
goku := new(Saiyan)
goku.Name = "Goku"
goku.Power = 9001

goku := &Saiyan {
  Name: "Goku",
  Power: 9001,
}
```
#### Can "overwrite"
It's not technically overwriting. You create a method (func) of the same name associated with the newly composed struct.
```
type Person struct {
  Name string
}
func (p *Person) Introduce() {
  fmt.Printf("Hi im %s.", p.Name)
}

type Saiyan struct {
  *Person
  Power int
}

func (s *Saiyan) Introduce() {
  fmt.Printf("I am %s!\n", s.Name)
}


func main() {
  goku := Saiyan{
    Person: &Person{"Goku"},
    Power: 9001,
  }
  goku.Introduce()
  goku.Person.Introduce()
}

```
### Arrays
```
func main() {
  scores := [5]int{9001,9004,500,3,7000} // Array of ints
  
  for index, value := range scores {
    fmt.Printf("%d and %d\n", index, value)
  }
  
  
  
  text := [5]string{"Hello","World","Little","Lamb","TEST"} // Array of strings
  
  for index, value := range text {
    fmt.Printf("%d and %s\n", index, value)
  }
}
```
#### Slices
Slices  (similar to the slices in python) refer to a segemnt of a hidden array.
__Length__ the length of the slice. len(testArray) -> int
__Capacity__ the length of the hidden array. cap(testslice) -> int
__append__(slice, value) to the end of the __length__ of a slice.
Also, append returns a new value to point to a new array if the previous aray becomes full.
Go uses a 2x aray growth algorith (everytime you need to increase array size, doubole it).
Normal (when the underlying aray doesn't need to be copied into a larger one) append just returns a pointer (or the slice of the arry) for the origonalarray.
```
func main() {
  exampleSlice := make([]int, 0, 10)
  exampleSlice = append(exampleSlice , 5)
  fmt.Println(exampleSlice )


  scoreSlice := make([]int, 1, 10)
  scoreSlice = append(scoreSlice, 5)
  fmt.Println(scoreSlice)


  sliceNArray:= make([]int, 0, 0)
  sliceNArray = append(sliceNArray, 5)
  fmt.Println(sliceNArray)

  sliceNArray3:= make([]int, 0, 0)
  sliceNArray3 = append(sliceNArray3, 5)
  sliceNArray3 = append(sliceNArray3, 6)
  fmt.Println(sliceNArray3)


  sliceNArray2:= make([]int, 0, 3)
  sliceNArray2 = append(sliceNArray2, 5)
  fmt.Println(sliceNArray2)
  sliceNArray2 = append(sliceNArray2, 6)
  fmt.Println(sliceNArray2)


  sliceNArray4:= make([]int, 3, 10)
  fmt.Println(sliceNArray4)
  sliceNArray4 = append(sliceNArray4, 5)
  fmt.Println(sliceNArray4)
  sliceNArray4 = append(sliceNArray4, 6)
  fmt.Println(sliceNArray4)
}
```

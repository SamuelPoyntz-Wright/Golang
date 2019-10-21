Questions To Answer:

- fmt.Println VS fmt.Printf


__:=__ Opperator can be used to declare and assign multiple variables.
It can also be used to just asign a new value to existing variables as long as it is declaring one new variable (see code below):
```go
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
```go
func simultaneousEq(a,b,c int, x,d int) int {
  return 4
}
```
Functions:
```go
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
```go
goku := &Saiyan{"Goku", 9000} // &  used to get pointer value

func Super(s *Saiyan) {   //  *   used to expect a pointer   of data type Saiyan
  s.Power += 10000
}
```
\
Many funcs return multiple values and you may often not want to use all of them at once.
```go
func kamehamehaStrength(name string) (int, bool) {
  //Returns two values
  
  return 9000, True
}

_ , canCellKamehameha = kamehamehaStrength("Cell")
```
\
### Defining a Struct (basics e.g. no methods):
```go
type Saiyan struct {
  Name string
  Power int
}
```
\
\
Code (languages): Trailing and the opposite? - "Trailing __Commas__ " -> commas after each atribute in a structure Instantiation INCLUDING THE LAST ONE:
```go
goku := Saiyan{
  Name: "Goku",
  Power: 9000,
}
```
```go
goku := Saiyan{}
```
```go
goku := Saiyan{}
goku.Name = "Goku"
goku.Power = 9001
```
```go
goku := Saiyan{Name: "Goku"}
goku.Power = 9001
```
```go
//Only use with structs that hve FEW attributes, to preserve clarity.
goku := Saiyan{"Goku",9001}
```
#### Add METHODS
```go
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
```go
goku := &Saiyan("Goku", 9001}
goku.Super()
```
Use pointer - so the method actully affects __goku__'s attributes. (Pass ByRef)
\
#### Composition
Creating new classes which use other classes as attributes.  
The football team class uses 11 instances of the football player class.  
ArsenalPlayer11.Name -> Mike  
ArsenalPlayer11.Position -> Midfeilder  
ArsenalPlayer11.Player.Position -> \[Midfeilder, Defender]  

The position of a plyer is overloaded in the team class as for the team (with this combo of players) they fit best by far as a midfeilder, but their name isn't overloaded as that stays the same.  
A player can play different positions, but when they are in a team a player's positions maybe limmited.
```go
type Person struct {
 Name string
}
func (p *Person) Introduce() {
  fmt.Printf("Hi, I'm %s\n", p.Name)
}

type Saiyan struct {
  *Person
   Power int
}


//Using it
goku := &Saiyan{
  Person: &Person{"Goku"},
  Power: 9001,
}
goku.Introduce()
```

#### Constructors
```go
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
```go
goku := new(Saiyan)
goku := &Saiyan{}
```
```go
goku := new(Saiyan)
goku.Name = "Goku"
goku.Power = 9001

goku := &Saiyan {
  Name: "Goku",
  Power: 9001,
}
```
#### Can "overload"
It's not technically overloading. You create a method (func) of the same name associated with the newly composed struct.
```go
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
```go
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
```go
sliceScores := []int{1,2,3,4}
sliceScores2 := make([]int, 4)
sliceScores3 := make([]int, 2, 4) //length 2 (which is three positions) Capacity of 4 (which means there ae a max of 4 positions)

newSlice := make ([]int, 0, 10)
newSlice = append(newSlice, 9000)
fmt.Println(newSlice)
newSlice = newSlice[0:7]
fmt.Println(newSlice)
for _, value := range sliceScores{
  newSlice = append(newSlice, value)
}
fmt.Println(newSlice)
```
```go
//Appending



func main() {
  exampleSlice := make([]int, 0)
  fmt.Println(exampleSlice )
  exampleSlice = append(exampleSlice , 5)
  fmt.Println(exampleSlice )


  example44Slice := make([]int, 1)
  fmt.Println(example44Slice )
  example44Slice = append(example44Slice , 5)
  fmt.Println(example44Slice )  

  example44Slice = append(example44Slice , 7)
  example44Slice  =example44Slice [0:4]
  fmt.Println(example44Slice )  

  example44Slice = append(example44Slice , 99)
  fmt.Println(example44Slice )

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
\
Defining slices
```go
var names := []string
identifiers := []string{"ford", "jake", "Spain"}
tally := make([]int, 10)
score := make([]int, 6, 10)
```
##### Slices refer to arrays (slices are wrappers)
A slice of a slice -> the new slice referes to the same array as the previous slice.
```go
func main() {
  nums := []int{34,6,89,44,180}
  newSlice := nums[2:4]
  newSlice [0] = 999
  fmt.Println(newSlice)
  fmt.Println(nums)
}
```
Output  
(999, 44)  
(34, 6, 999, 44, 180)
  
##### Copy function (inbuilt)
```go
package main

import (
  "fmt"
  "math/rand"
  "sort"
)

func main() {
  nums := make([]int, 100)
  for i := 0; i < 100; i++ {
    nums[i] = int(rand.Int31n(1000))
  }
  sort.Ints(nums)
  worst := make([]int, 5)
  avg := make([]int, 5)
  best := make([]int, 5)

  copy(worst, nums[:5])
  copy(avg, nums[54:59])
  copy(best, nums[95:])

  fmt.Println(worst)
  fmt.Println(avg)
  fmt.Println(best)
}
```
  
### Strings
```go
//Returns INDEX of first space character after position 5 in string "stringName"
strings.Index(stringName[5:], " ")
```
### Maps
Maps use __make()__ aswell.  
```go
Library := make(map[string]int) //empty map

Library2 := map[string]*int{    //Mapp with key-value pairs to start
  "Bible": 3,
  "Dickens": 2,
  "Famous Five": 1,
}
```
#### Maps in structures
```go
type People struct {
  Address string
}

type Saiyan struct {
  Name string
   Friends map[string]*People
}

//Initialise VERSION 1
goku := &Saiyan {
  Name: "Goku",
  Friends: make(map[string]*People),
}
goku.Friends["Mike"] = "24 Crescent Drive, Apple Guild Lane, Funky Town"
```
```go
//Initialise VERSION 2
package main

import (
  "fmt"
)


func main() {

type People struct {
  Address string
}

type Saiyan struct {
  Name string
  Friends map[string]*People
}



goku := &Saiyan {
  Name: "Goku",
  Friends: map[string]*People{"Mike": &People{"24 Crescent Drive, Apple Guild Lane, Funky Town"}},
}


fmt.Println(goku.Name)
fmt.Println(goku.Friends["Mike"])
fmt.Println(goku.Friends["Mike"].Address)
fmt.Println(goku.Friends)
}
```
__Output:__  
Goku  
&{24 Crescent Drive, Apple Guild Lane, Funky Town}  
24 Crescent Drive, Apple Guild Lane, Funky Town  
map[Mike:0x40c138]  

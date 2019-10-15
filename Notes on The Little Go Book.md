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


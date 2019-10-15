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
\
Many funcs return multiple values and you may often not want to use all of them at once.
```
func kamehamehaStrength(name string) (int, bool) {
  //Returns two values
  
  return 9000, True
}

_ , canCellKamehameha = kamehamehaStrength("Cell")
```

Code (languages): Trailing and the opposite? - "Trailing __Commas__ " -> commas after each atribute in a structure INCLUDING THE LAST ONE:
```
goku := Saiyan{
  Name: "Goku",
  Power: 9000,
}
```



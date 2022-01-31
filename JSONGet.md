Panos's implementation. This queries thw Star Wars API (SWAPI) (GET request). It then successfuly interprets the JSON responce  
(only making the key: value pairs, we're interested in availble).
He used this lin (https://mholt.github.io/json-to-go/) to create the appropriate Go structures for the JSON responce.
```go
package main
import ("fmt"
        //"strings"
        //"io/ioutil"
        "net/http"
        "encoding/json"
        //"log"
)
type SwapiData struct{
    PlanetCount int `json:"count"`
    Result []struct {
        PlanetName string `json:"name"`
        PlanetClimate string `json:"climate"`
    } `json:"results"`
}
func main(){
    var d SwapiData
    response, err :=http.Get("https://swapi.co/api/planets")
    if err != nil{
        fmt.Println("Failed HTTP request %s\n", err)
    }
    defer response.Body.Close()
    
    if err := json.NewDecoder(response.Body).Decode(&d); err !=nil{
        fmt.Println( SwapiData{}, err)
    } else {
        fmt.Println(d)
        fmt.Println(d.Result[0].PlanetName)
        fmt.Println(d.Result[0].PlanetClimate)
    }
}
```


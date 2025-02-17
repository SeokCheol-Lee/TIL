# Go 언어 TIL

Go 언어는 간결하고 효율적인 문법과 높은 성능을 목표로 설계되었습니다. 여기서는 Go의 기본 문법과 주요 특징들을 정리합니다.

---

## 패키지와 Export

- **패키지**: Go의 모든 코드는 패키지 단위로 구성됩니다.
- **Export**:
    - Go에서는 외부에서 접근 가능하도록 하려면 함수, 변수, 구조체, 필드의 이름을 **대문자**로 시작해야 합니다.
    - 소문자로 시작하면 해당 패키지 내에서만 접근할 수 있습니다.

예시:

```go
package mypackage

// ExportedFunction은 외부 패키지에서도 호출할 수 있습니다.
func ExportedFunction() {
    // ...
}

// notExportedFunction은 현재 패키지 내에서만 호출할 수 있습니다.
func notExportedFunction() {
    // ...
}

```

---

## 변수와 상수

### 상수 (Constants)

- `const` 키워드를 사용하며, 값이 변경되지 않습니다.
- 타입은 명시할 수도 있고, 생략할 수도 있습니다.

```go
const language string = "Go"
const version = 1.18 // 타입 추론

```

### 변수 (Variables)

- `var` 키워드를 사용하여 변수를 선언합니다.
- 변수는 선언 후 값을 변경할 수 있습니다.

```go
var name string = "GoLang"
var age int = 10

```

### 단축 변수 선언

- 함수 내부에서는 `:=`를 사용해 간편하게 변수를 선언하고 초기화할 수 있습니다.
- 단, 함수 바깥에서는 사용할 수 없습니다.

```go
func main() {
    greeting := "Hello, Go!"
    fmt.Println(greeting)
}

```

---

## 함수

### 기본 함수 정의

- 인자와 반환 타입을 명시해야 합니다.

```go
func multiply(a int, b int) int {
    return a * b
}

```

### 여러 개의 반환값

- Go는 하나의 함수에서 여러 개의 값을 반환할 수 있습니다.

```go
import (
    "fmt"
    "strings"
)

func lenAndUpper(name string) (int, string) {
    return len(name), strings.ToUpper(name)
}

func main() {
    totalLength, upperName := lenAndUpper("golang")
    fmt.Println(totalLength, upperName)
}

```

- 반환값을 사용하지 않을 때는 `_` (언더스코어)를 사용하여 무시할 수 있습니다.

### Naked Return

- 반환할 변수의 이름을 미리 지정하면, `return`문만으로도 값을 반환할 수 있습니다.

```go
func lenAndUpper(name string) (length int, uppercase string) {
    length = len(name)
    uppercase = strings.ToUpper(name)
    return // naked return
}

```

---

## Defer

- `defer`는 함수가 종료되기 직전에 지정한 함수를 실행합니다.

```go
func main() {
    defer fmt.Println("I'm done")
    fmt.Println("Processing...")
}

```

---

## 루프 (Loops)

### for 루프

- Go에는 유일한 반복문인 `for`가 있습니다.

```go
// 기본 for 루프
for i := 0; i < 5; i++ {
    fmt.Println(i)
}

```

### range를 사용한 순회

- 배열, 슬라이스, 맵, 문자열 등에 대해 반복할 수 있습니다.

```go
numbers := []int{1, 2, 3, 4, 5}
for index, number := range numbers {
    fmt.Println(index, number)
}

```

- 필요에 따라 인덱스나 값을 무시할 수 있습니다:

```go
for _, number := range numbers {
    fmt.Println(number)
}

```

---

## 조건문

### if-else와 초기화 구문

- `if`문 안에서 변수를 선언할 수 있으며, 그 변수는 if 블록 내에서만 유효합니다.

```go
func canIDrink(age int) bool {
    if koreanAge := age + 2; koreanAge < 18 {
        return false
    } else {
        return true
    }
}

```

### switch 문

- Go의 `switch`문도 초기화 구문을 지원합니다.

```go
func canIDrink(age int) bool {
    switch koreanAge := age + 2; koreanAge {
    case 10:
        return false
    case 18:
        return true
    default:
        return false
    }
}

```

---

## 포인터 (Pointers)

- Go는 C/C++처럼 포인터를 지원하여 메모리의 주소를 직접 다룰 수 있습니다.

```go
func main() {
    a := 2
    b := &a // a의 주소를 b에 할당
    fmt.Println(*b) // b가 가리키는 값을 출력 (2)
}

```

---

## 배열과 슬라이스

### 배열 (Arrays)

- 배열은 고정된 길이를 가진 데이터 구조입니다.

```go
names := [5]string{"name", "name2", "name3", "name4", "name5"}
names[3] = "aa"

```

### 슬라이스 (Slices)

- 슬라이스는 동적 배열로, 길이가 가변적입니다.
- 슬라이스는 배열 위에 구축된 자료구조이며, `append` 함수를 사용해 요소를 추가할 수 있습니다.

```go
names := []string{"name", "name2"}
names = append(names, "add")

```

---

## 맵 (Maps)

- 맵은 키-값 쌍으로 이루어진 자료구조로, Python의 딕셔너리와 유사합니다.

```go
n := map[string]string{"name": "n1", "age": "12"}
for key, value := range n {
    fmt.Println(key, value)
}

```

---

## 구조체 (Structs)

- 구조체는 여러 필드를 가진 복합 데이터 타입입니다.
- Go에는 클래스가 없지만, 구조체와 메서드를 통해 객체 지향 프로그래밍과 유사한 기능을 구현할 수 있습니다.

### 구조체 정의

- 외부에서 접근 가능한 필드로 만들고 싶다면 필드 이름을 대문자로 시작해야 합니다.

```go
type Person struct {
    Name    string   // Exported field
    Age     int
    FavFood []string
}

```

### 구조체 인스턴스 생성

- 두 가지 방식이 있습니다.

```go
// 순서대로 필드 값을 지정 (주의: 순서가 중요)
person1 := Person{"Alice", 30, []string{"kimchi", "bulgogi"}}

// 필드 이름을 명시하여 생성 (가독성 좋음)
person2 := Person{
    Name:    "Bob",
    Age:     25,
    FavFood: []string{"bibimbap", "kimbap"},
}

```

- Go에는 클래스나 생성자(constructor)가 없으므로, 초기화 함수를 만들어 사용할 수 있습니다.

```go
func NewPerson(name string, age int, favFood []string) Person {
    return Person{
        Name:    name,
        Age:     age,
        FavFood: favFood,
    }
}

```

---

## 추가 참고 사항

- **패키지 관리**: Go에서는 `go mod`를 통해 의존성 관리를 합니다.
- **문서화**: GoDoc을 통해 패키지와 함수에 대한 문서화를 할 수 있습니다.
- **도구**: `gofmt` 명령어를 사용해 코드를 자동으로 정리할 수 있습니다.

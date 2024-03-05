### golang make和new的区别

### 1. 相同点

- 都是内建函数，都是在堆上分配内存，都需要传递类型参数

### 2. 不同点

- 传递的参数不一样，new函数只接收一个参数，make函数可以接收一个以上的参数

```golang
package main

import "fmt"

func main() {
	// int类型0值的指针，返回的值是以0x开头的16进制整数，参数个数为1
	intZeroValuePoint := new(int)
	fmt.Printf("%v\n", intZeroValuePoint)

	// 为slice分配内存, 创建初始值问 [0 0 0 0 0] 的切片，参数个数为3，第三个参数是可选的
	intHasInitLenSlice := make([]int, 5, 10)
	fmt.Printf("%v\n", intHasInitLenSlice)
}


```

- 返回的参数类型不一样，new函数返回对应输入参数类型的指针类型，make函数返回输入参数类型

```golang
package main

import "fmt"

func main() {
	// int类型0值的指针，返回的值是以0x开头的16进制整数
	intZeroValuePoint := new(int)
	fmt.Printf("%T\n", intZeroValuePoint)		// 输出 *int

	// 为slice分配内存, 创建初始值问 [0 0 0 0 0] 的切片
	intHasInitLenSlice := make([]int, 5, 10)
	fmt.Printf("%T\n", intHasInitLenSlice)		// 输出 []int
}

```

- 使用场景不一样，new函数为类型分配类型对应零值内存并返回指针，make是为特定引用类型slice map chan 分配内存

```golang
package main

import "fmt"

func main() {
	// int类型0值的指针，返回的值是以0x开头的16进制整数
	intZeroValuePoint := new(int)
	fmt.Printf("%T\n", intZeroValuePoint) // 输出 *int

	// 为slice零值分配内存，返回的值是以0x开头的16进制整数
	sliceZeroValuePoint := new([]int)
	fmt.Printf("%T: %v\n", sliceZeroValuePoint, sliceZeroValuePoint) // 输出 *[]int &[]

	// 为slice分配内存, 创建初始值问 [0 0 0 0 0] 的切片
	intHasInitLenSlice := make([]int, 5, 10)
	fmt.Printf("%T\n", intHasInitLenSlice) // 输出 []int

	// 为map分配内存
	mapValue := make(map[string]string, 10)
	fmt.Printf("%T\n", mapValue) // 输出 map[string]string

	// 为chan类型分配内存
	chanValue := make(chan int, 10)
	fmt.Printf("%T\n", chanValue)
}


```






























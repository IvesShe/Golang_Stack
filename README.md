# Golang Stack 數組模擬實作

# 棧 簡介
- 有些程序員也把棧稱為堆棧(但實際上棧與堆是有區別的)。
- 棧(Stack)是一個先入後出的有序列表(FILO-First In Last Out)。
- 棧是限制線性表中元素的插入和刪除只能在線性表的同一端進行的一種特殊線性表，允許插入和刪除的一端，為變化的一端，稱為棧頂(Top)，另一端為固定的一端，稱為棧底(Bottom)。
- 根據堆棧的定義可知，最先放入棧中元素在棧底，最後放入的元素在棧頂，而刪除元素剛好相反，最後放入的元素最先刪除，最先放入的元素最後刪除。

![image](./images/20210131161149.png)

![image](./images/20210131161233.png)


# 棧 的應用場景

1. 子程序的調用
2. 處理遞歸的調用
3. 表達式的轉換與求值
4. 二叉樹的遍歷
5. 圖形的深度優先(depth-first)搜索法

# 執行結果

![image](./images/20210131161929.png)

# 代碼

main.go

```go
package main

import (
	"errors"
	"fmt"
)

// 使用數組來模擬一個棧的使用
type Stack struct {
	MaxTop int    // 表示棧最大可以存放個數
	Top    int    // 表示棧頂，因為棧頂固定，因此直接使用Top
	arr    [5]int // 數組模擬棧
}

// 入棧
func (s *Stack) Push(val int) (err error) {
	// 先判斷棧是否滿了
	if s.Top == s.MaxTop-1 {
		fmt.Println("stack full")
		return errors.New("stack full")
	}
	s.Top++

	// 存放數據
	s.arr[s.Top] = val
	return
}

// 出棧
func (s *Stack) Pop() (val int, err error) {
	// 判斷棧是否為空
	if s.Top == -1 {
		fmt.Println("stack empty")
		return
	}

	// 先取值，再s.Top--
	val = s.arr[s.Top]
	s.Top--
	return val, nil
}

// 遍歷棧，注意需要從棧頂開始遍歷
func (s *Stack) List() {
	// 判斷棧是否為空
	if s.Top == -1 {
		fmt.Println("stack empty")
		return
	}

	fmt.Println("棧的情況如下: ")
	for i := s.Top; i >= 0; i-- {
		fmt.Printf("arr[%d] = %d \n", i, s.arr[i])
	}
}

func main() {

	stack := &Stack{
		MaxTop: 5,  // 表示最多存放5個數到棧中
		Top:    -1, // 當前棧頂為-1，表示棧為空
	}

	// 入棧
	stack.Push(1)
	stack.Push(2)
	stack.Push(3)
	stack.Push(4)
	stack.Push(5)

	// 顯示
	stack.List()

	val, _ := stack.Pop()
	fmt.Println("出棧 val = ", val)

	// 顯示
	stack.List()

	val, _ = stack.Pop()
	fmt.Println("出棧 val = ", val)

	// 顯示
	stack.List()
}
```

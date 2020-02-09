# 包含min函数的栈
 
## 题目描述
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

### 解题思路

定义一个set 保存 进入 stack 的元素， 保证非重复， 当在stack 出栈后，且当前栈不再存在该元素时，
就将对应元素也从 set 中移除。

### 代码

```java
import java.util.*;

public class Solution {
    int temp;
    // 定义一个用于正常出入栈的数据栈
    Stack<Integer> stack = new Stack();
    // 定义一个元素不重复的数据结构
    Set<Integer> set = new HashSet(); // 
    int minV = 0;
    // 顺序不能变 要求以此找到
    public void push(int node) {
       // 入栈 进行判断
        // 首先 保存栈 基本不需要判断 直接入栈 元素 
        stack.push(node);
        // 非重复栈只记录 新元素 并且排序
        set.add(node);
        minV = Collections.min(set);
    }
    
    public void pop() {
    
        if(!stack.isEmpty()){
           temp = stack.pop();
           if(stack.search(temp) == -1 && set.contains(temp))
               set.remove(temp);
         }      
        minV = Collections.min(set);
    }
    
    public int top() {
        if(!stack.isEmpty())
            return stack.peek();
        return -1;
    }
    
    public int min() {
        return minV;
        /*
        if(!set.isEmpty())
            return Collections.min(set);
        return -1;
        */
    }
}// 3 [3] 4 [3] 2 [2] 3 [2]  p3 [2] p2 [3] p3 [3] 0 [0]
```

### 参考其他人的做法
使用双栈 一个栈用来保存所有元素，一个栈用来保存 最优元素，两个栈长度保持一致。

### 代码

```java
链接：https://www.nowcoder.com/questionTerminal/4c776177d2c04c2494f2555c9fcc1e49?answerType=1&f=discussion
来源：牛客网

import java.util.Stack;
 
public class Solution {
    Stack<Integer> stackTotal = new Stack<Integer>();
    Stack<Integer> stackLittle = new Stack<Integer>();
 
    public void push(int node) {
        stackTotal.push(node);
        if(stackLittle.empty()){
            stackLittle.push(node);
        }else{
            if(node <= stackLittle.peek()){
            // 如果比当前 栈顶元素还要小 那就直接 将该元素入栈
                stackLittle.push(node);
            }else{
                // 保留 自身  因为只要自己是最小的 后面的来的没有自己小 当前最小值就还是自己
                // 所以直接用自身替代。
                stackLittle.push(stackLittle.peek()); 
            }
        }
    }
 
    public void pop() {
        stackTotal.pop();
        stackLittle.pop();
    }
 
    public int top() {
        return stackTotal.peek();
    }
 
    public int min() {
        return stackLittle.peek();
    }
}

```

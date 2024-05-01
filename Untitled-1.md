数组栈的Java表示

```java
class Stack{
public final int SIZE = //自己定义
    int[] stack ;
    int top ;

    public Stack(){
        stack = new int[SIZE];
        top = 0;
    }

    public void push(int val){
        //注意越界的问题
        stack[top++] = val;
    } 

    public int pop(){
        //注意是不是为空
        if(top > 0)
        return stack[--top];
    }

    public boolean isEmpty(){
        return top == 0;
    }
}
```

链表栈的Java实现

```java
//需要用到Listnode类，自己创建
class Stack{
    ListNode head, tail;
    public Stack(){

    }

    public void push(int x){
        ListNode list = new ListNode(x);

    }

}
```

最小栈（就是返回的值是栈中的最小值）

```java
建立两个栈，一个是正常的，另一个是最小栈
class MinStack{
    public MinStack(){

    }

    public void push(int x){
        if(x <= MinStack.peek()){
            就压入x
        }
        else{
            压入MinStack.peek()
        }
    }
}
```

栈和队列之间的相互转换

```java
//栈 ----->  队列
class StackDeque{
    Stack<Integer> in = new Stack<>();
    Stack<Integer> out = new Stack<>();

    public void push(int x){
        in.push(x);
    }

    public int pop(){
        if(!out.isEmpty()){
            return out.pop();
        }
        if(in.isEmpty()){
            return -1;
        }    
        while(!in.isEmpty()){
            out.push(in.pop())
        }
        return out.pop();
    }

    public boolean isEmpty(){
        if(in.isEmpty() && out.isEmpty()){
            return true;
        }
        else {
            return false;
        }
    }
}


//队列  ------>   栈
class DequeStack{
    Deque<Integer> d1 = new ArrayDeque();
    Deque<Integer> d2 = new ArrayDeque();
    public void push(int x){
        d1.push(x);
        while(!d2.isEmpty()){
            d1.push(d2.pop());
        }
        Deque temp = d1;
        d1 = d2;
        d2 = temp;
    }

    public int pop(){
        return d2.pop();
    }


}
```

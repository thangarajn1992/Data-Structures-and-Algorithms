# Implement Queue using Stack

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/queue-using-stack/1#)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Solution

#### Using Single Stack and functional call stack - Dequeue heavy

```cpp
class Queue {
    stack<int> s;
public:
    void enqueue(int x) {
        s.push(x);
    }
    
    int dequeue() {
        if(s.empty())
            return -1; // error
            
        int x = s.top();
        s.pop();
        
        if(s.empty())
            return x;
        
        int item = dequeue();
        
        s.push(x);
        return item;
    }
};
```

#### Two Stacks - Dequeue Heavy

```cpp
class Queue {
    stack<int> input, output;
public:
    void enqueue(int x) {
        input.push(x);
    }

    int dequeue() {
        if(input.empty() && output.empty())
            return -1;
        if(output.empty())
        {
            while(!input.empty())
            {
                output.push(input.top()); 
                input.pop();
            }
        }
        int tmp = output.top();
        output.pop();
        return tmp;
    }
};
```

#### Two Stacks - Enqueue Heavy

```cpp
class Queue {
    stack<int> input, output;
public:    
    void enqueue(int x) {
       while(!input.empty())
       {
           output.push(input.top());
           input.pop();
       }
       input.push(x);
       while(!output.empty())
       {
           input.push(output.top());
           output.pop();
       }
    }    
    int dequeue() {
        int x = input.top();
        input.pop();
        return x;
    }
};
```


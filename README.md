# sandboxprof

Testing : 

1. Stack 
#include <iostream>
#include <stack>

int main() {
    std::stack<int> s;

    // Push elements
    s.push(10);
    s.push(20);
    s.push(30);

    // Access top element
    std::cout << "Top element: " << s.top() << std::endl; // Output: 30

    // Remove top element
    s.pop();

    std::cout << "New top element: " << s.top() << std::endl; // Output: 20

    return 0;
}

Stacks are essential because they provide a simple way to track state.

Undo/Redo: Every time you type in a document, your actions are "pushed" onto a stack. When you hit Ctrl+Z, the editor "pops" the most recent action to reverse it.

Function Calls: Your computer uses a "Call Stack" to manage functions. When you call a function, the computer pushes the current execution state onto the stack. When the function returns, it pops that state off to resume where it left off.

Syntax Checking: Compilers use stacks to ensure parentheses in your code are balanced—every ( must have a corresponding ).

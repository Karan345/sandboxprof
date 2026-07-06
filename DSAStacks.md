DSA : Stacks : 

#include #include
int main() { std::stack s;

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

#Methds : 
class StackLinkedList:
    """Template for Stack using Linked List"""
    
    def __init__(self):
        """Initialize empty stack"""
        self.top = None
    
    def push(self, value):
        """Push element onto stack"""
        new_node = Node(value)
        new_node.next = self.top
        self.top = new_node
    
    def pop(self):
        """Pop element from stack"""
        if self.is_empty():
            print("Stack Underflow: Cannot pop from empty stack")
            return None
        value = self.top.value
        self.top = self.top.next
        return value
    
    def peek(self):
        """View top element without removing"""
        if self.is_empty():
            print("Stack is empty")
            return None
        return self.top.value
    
    def is_empty(self):
        """Check if stack is empty"""
        return self.top is None
    
    def size(self):
        """Get current size of stack"""
        count = 0
        current = self.top
        while current:
            count += 1
            current = current.next
        return count
    
    def display(self):
        """Display all elements in stack"""
        if self.is_empty():
            print("Stack is empty")
            return
        print("Stack elements (top to bottom):", end=" ")
        current = self.top
        while current:
            print(current.value, end=" ")
            current = current.next
        print()


class BalancedParentheses:
    """Application: Check balanced parentheses"""
    
    def is_balanced(self, expression):
        """Check if parentheses are balanced"""
        stack = StackArray()
        matching = {'(': ')', '[': ']', '{': '}'}
        
        for char in expression:
            if char in matching:
                stack.push(char)
            elif char in matching.values():
                if stack.is_empty():
                    return False
                opening = stack.pop()
                if matching[opening] != char:
                    return False
        
        return stack.is_empty()


class InfixToPostfix:
    """Application: Convert infix to postfix notation"""
    
    def convert(self, infix_expr):
        """Convert infix expression to postfix"""
        precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
        stack = StackArray()
        postfix = []
        
        for char in infix_expr:
            if char.isalnum():
                postfix.append(char)
            elif char == '(':
                stack.push(char)
            elif char == ')':
                while not stack.is_empty() and stack.peek() != '(':
                    postfix.append(stack.pop())
                if not stack.is_empty():
                    stack.pop()
            elif char in precedence:
                while (not stack.is_empty() and stack.peek() != '(' and
                       stack.peek() in precedence and
                       precedence[stack.peek()] >= precedence[char]):
                    postfix.append(stack.pop())
                stack.push(char)
        
        while not stack.is_empty():
            postfix.append(stack.pop())
        
        return ''.join(postfix)


class PostfixEvaluation:
    """Application: Evaluate postfix expression"""
    
    def evaluate(self, postfix_expr):
        """Evaluate postfix expression"""
        stack = StackArray()
        
        for char in postfix_expr:
            if char.isdigit():
                stack.push(int(char))
            elif char in ['+', '-', '*', '/', '^']:
                if stack.size() < 2:
                    print("Invalid expression")
                    return None
                operand2 = stack.pop()
                operand1 = stack.pop()
                
                if char == '+':
                    result = operand1 + operand2
                elif char == '-':
                    result = operand1 - operand2
                elif char == '*':
                    result = operand1 * operand2
                elif char == '/':
                    if operand2 == 0:
                        print("Division by zero")
                        return None
                    result = operand1 // operand2
                elif char == '^':
                    result = operand1 ** operand2
                
                stack.push(result)
        
        if stack.size() != 1:
            print("Invalid expression")
            return None
        
        return stack.pop()

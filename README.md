# Ex.No: 1.2  Infix to Postfix Conversion using Stack  
### DATE: 10.04.2025                                                                          
### REGISTER NUMBER: 212222220054  

### AIM:  
To write a Python program to convert a given Infix expression to Postfix expression by following the precedence and associativity rules using dictionary and set in Python.

### Algorithm:  
1. Start the program.  
2. Initialize a dictionary to define operator precedence.  
   - `^` has higher precedence than `*`.  
   - `^` is **right associative**, `*` is **left associative**.  
3. Initialize a set to store supported operators (`^` and `*`).  
4. Initialize an empty stack and output list.  
5. Scan the input infix expression from left to right.  
6. If the token is an operand, append it to output.  
7. If the token is an operator:  
   - Pop from stack to output based on precedence and associativity.  
   - Then push the current operator onto the stack.  
8. If the token is `(`, push to stack.  
9. If the token is `)`, pop from stack to output until `(` is found.  
10. After the scan, pop all remaining operators from stack to output.  
11. Display the postfix expression.  

### Program:
```python
def infix_to_postfix(expression):
    # Precedence dictionary: higher value = higher precedence
    precedence = {'^': 3, '*': 2}
    # Operators set
    operators = {'^', '*'}

    stack = []
    output = []

    for token in expression:
        if token.isalnum():  # Operand
            output.append(token)
        elif token == '(':
            stack.append(token)
        elif token == ')':
            while stack and stack[-1] != '(':
                output.append(stack.pop())
            stack.pop()  # Remove '('
        elif token in operators:
            while (stack and stack[-1] in operators and
                   ((precedence[token] < precedence[stack[-1]]) or
                    (precedence[token] == precedence[stack[-1]] and token != '^'))):
                output.append(stack.pop())
            stack.append(token)

    while stack:
        output.append(stack.pop())

    return ''.join(output)

# Driver Code
infix_expr = input("Enter infix expression using only ^ and *: ")
postfix_expr = infix_to_postfix(infix_expr)

print("Infix notation: ", infix_expr)
print("Postfix notation: ", postfix_expr)
```
# Output:

![image](https://github.com/user-attachments/assets/49fefa5d-2444-462e-a855-b9016dda42e1)





### Result:
Thus, the conversion of infix to postfix expression using stack with operator precedence and associativity was implemented successfully.

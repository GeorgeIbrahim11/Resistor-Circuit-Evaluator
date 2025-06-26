
# Resistor Circuit Evaluator

A C++ program that calculates total resistance in mixed series and parallel resistor circuits, based on a structured text input format.

## Features
- Supports nested `S` (series) and `P` (parallel) combinations
- Handles invalid inputs and edge cases
- Uses recursive parsing to evaluate the circuit

eaxmples
Input : S 1 2 3 23 3.4 e 
Output: The total resistance = 32.4 

Input : P 1 2 S 1 1 e e
Output: The total resistance = 0.5 

Input : S 1 P 1 1 e 2 e
Output: The total resistance = 3.5 

Input : P 1 2 w 1 1 e e  
Output: Wrong Description 

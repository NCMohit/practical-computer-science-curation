# Basic Programming

## Interface with command-line

### Output
```python
print("Output")
```

### Input
```python
input_var = input("Enter input: ")
```

## Interface with memory

### Data types
```python
int_var     = 5
float_var   = 0.5
string_var  = "string"
boolean_var = True

# Data type methods
print(type(int_var)) # <class 'int'>
print(abs(-10))      # 10
print(ord("a"))      # 97
print(chr(97))       # 'a'
```

### Type conversion
```python
float_to_int_var    = int(0.5)     # 0
float_to_string_var = str(0.5)     # '0.5'
int_to_string_var   = str(5)       # '5'
int_to_float_var    = float(5)     # 5.0
string_to_int_var   = int("5")     # 5
string_to_float_var = float("5.1") # 5.1
```

### Derived Data Types
```python
int_list   = [1,2,3,4,5] # Mutable, has index
tuple_list = (1,2,3,4,5) # Immutable, has index
set_list   = {1,2,3,4,5} # Immutable, dosen't have index
dictionary = {
    "numbers": [1,2,3,4,5],
    "characters": ["a","b","c"]
}

### Assign value to index of list
int_list[0] = 6     # Indexes start with 0   
print(int_list)     # [6,2,3,4,5]

### Derived data type methods
print(len(int_list))   # 5
print(max(tuple_list)) # 5
print(min(set_list))   # 1
print(sum(int_list))   # 20 

### Dictionary methods
print(len(dictionary))     # 2
print(dictionary.keys())   # ["numbers","characters"]
print(dictionary.values()) # [[1,2,3,4,5],["a","b","c"]]
print(dictionary.items())  # [("numbers",[1,2,3,4,5]), ("characters",["a","b","c"])]
```

### Memory address
```python
var1 = 5
var2 = var1

print(var1) # 5
print(var2) # 5

var1 = 7
print(var1) # 7
print(var2) # 5

### var1 and var2 memories directly have the value inside them

var1 = [1,2,3]
var2 = var1

var1[0] = 4
print(var1) # [4,2,3]
print(var2) # [4,2,3]

print(id(var1)) # 2151836418496
print(id(var2)) # 2151836418496

### var2 stores the address of var1 in its memory

### Instead to create a new memory allocation use copy()
var1 = [1,2,3]
var2 = var1.copy()

var1[0] = 4
print(var1) # [4,2,3]
print(var2) # [1,2,3]

print(id(var1)) # 2151836418496
print(id(var2)) # 2151836333696
```

## Interface with disk

### Read
```python
file = open("/path/to/file.txt","r").read()
```

### Write
```python
text = "Text to be written to file"

### Overwrite entire file
file = open("/path/to/file.txt","w")

### Append to file
file = open("/path/to/file.txt","a")

file.write(text)
```

## Logic ( Interface with CPU )

### Operators
```python
var_True  = True
var_False = False
var_high  = 99
var_low   = 1

or_opeartor            = var_True | var_False  # True
and_operator           = var_True & var_False  # False
less_than_operator     = var_low < var_high    # True
greater_than_operator  = var_low > var_high    # False
equals_to_operator     = var_low == var_high   # False
not_equals_to_operator = var_low != var_high   # True

### Numeric Operators

addition_operator       = 5 + 10  # 15
subtration_operator     = 5 - 10  # -5
multiplication_operator = 5 * 10  # 50
division_operator       = 5 / 10  # 0.5
quotient_operator       = 5 // 10 # 0
remainder_operator      = 5 % 10  # 5

operator_shortcut = 5
operator_shortcut += 10
```

### Controls

#### If-Else
```python
var_1 = 5
var_2 = 6

if(var1 == var2):
    print("Numbers equal")
else:
    print("Numbers not equal")
```

#### While
```python
counter = 0
while(counter < 5):
    print(counter)
    counter += 1        # 0 1 2 3 4
```

#### Functions
```python
def left_is_greater(a, b):
    if(a > b):
        return True
    else:
        return False

print(left_is_greater(4,5))     # False
```

### Object Oriented Programming ( Classes )
```python
class Car:
    def __init__(self, speed, size):
        self.speed = speed
        self.size  = size
    def get_speed(self):
        print("Speed of this car is: ",self.speed)
    def set_speed(self, new_speed):
        self.speed = new_speed

car1 = Car(speed=5, size=10)
car2 = Car(speed=7, size=11)

car1.get_speed()    # Speed of this car is: 5
car2.get_speed()    # Speed of this car is: 7

car1.set_speed(10)
car1.get_speed()    # Speed of this car is: 10
```

## Interface with Network

### HTTP protocol
```python
import requests

response = requests.get("http://info.cern.ch")
print(response.content)
```

### Socket Programming

#### Server
```python
import socket

def run_server(host,port):
    server_socket = socket.socket() 
    server_socket.bind((host, port))
    print("Waiting for client connection . . . ")
    server_socket.listen(2)
    conn, address = server_socket.accept()
    print("Client connected!")
    while True:
        data = input("Enter server message: ")
		conn.send(data.encode())
		client_data = conn.recv(1024).decode()
        print("Message from client: ",client_data)

run_server("localhost",8080)
```

#### Client
```python
import socket

def run_client(host,port):
	client_socket = socket.socket()
	client_socket.connect((host, port))
    while True:
        data = client_socket.recv(1024).decode()
        print("Message from server: ",data)
        send_data = input("Enter client message: ")
        client_socket.send(send_data.encode())

run_client("localhost",8080)
```
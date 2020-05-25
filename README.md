# Ten Holy Grail Blocks

1. CPU, Abstractions
2. variables
3. operators
4. statements
5. scopes
6. loops
7. functions
8. collections
9. classes

# 1. CPU

accepts `instructions numbers` as a binary

```
0001 1100 0010 1010
0011 0100 1010 1010
0011 0100 1010 1010
```

human readable aliases

```
ADD = 0001 1100
PUT = 0011 0100
```

so instead of binary, you write an assembler language

```
ADD 0xb1
PUT 0xf0
...
```

Languge Abstraction

| Language    | What's new?     |
| ----------- | --------------- |
| Assembler   | ADD 0xb1        |
| c           | int a = 5 + 1;  |
| c ++        | classes         |
| Java        | virtual machine |
| Python      | a = 5           |
| AppleScript | set a to five   |

How to convert Binary to a Decimal?

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   | Result |
| --- | --- | --- | --- | --- | --- | --- | --- | ------ |
| 0   | 0   | 0   | 1   | 0   | 0   | 1   | 0   | = 18   |

Ho to convert Decimal to the Binary?

`Say we have a Decimal 22. We substract the biggest "Binary" Number. Here will it be 16, so 22-16=6. Next biggest Binary will be 4, so 6-4=2. Next Binary 2. We have no reminder left. Our Binary is 16,4,2 = 0001 0110`

What is a Byte? For an 8-bit CPU...

`1` byte = `0000 0000` bit

8 bit boolean

```
0000 0001 = true
0000 0000 = false
```

8 bit unsigned integer

```
0000 0000 = 0
0000 0001 = 1
0000 0011 = 3
1111 1111 = 255
```

8 bit signed integer

```
1000 0000 = -0
1 111 1111 = -128
0 111 1111 = 128
```

8 bit char

```
0100 0001 = 65 = 'A'
char test = 65
char test = 0b0100001
char test = 'A'
```

2 byte = 16 bit integer uint16_t / long unsigned int

```
0000 0000 0000 0000
```

# 2. Variables

#### Primitive Types

```
bool a = true;
byte a = 255;
unsigned int a = 65536;
signed int a = -32768;
float a = 4.234;
char a = 'B';
```

Problem of Floats

```
float a = 100;
a += 1
a == 101 is not true because 101.0000000000001 != 100
```

Solution

```
float range = 0.01;
if (a < 100 - range && 100 + range < a) ...
```

#### Complex Types

lists

```
int a [10];
a[9] = 435; // set value 435 to the position 9th position
a = {100, ..., 435}
a.push(10) // adds an element to the end
a.pop() // removes an element from the end
a.slice(4, 3) // removes 3 elements starting from the 4th position
```

list of chars is a string

```
char word [11] = {'H', 'e', 'l', ...};
String word = "Hello World";
```

structs to bundle different typed variables and functions in one tupple

```
struct Human {
	byte age = 18;
	int hasMoneyInThePocket = 892734;
	String name = "Vasja";
	...
}
```

miscellaneous types

```
functions ...
classes ...
```

# 3. Operators

Bitwise Operators to shift Bits

| Operator | Meaning                       |
| -------- | ----------------------------- |
| &        | and                           |
| \|       | or                            |
| << n     | shift to the left by n steps  |
| >> n     | shift to the right by n steps |

Example for 'or'

```
0000 0001 |
0000 1001 =
0000 1001
```

Example for 'and'

```
0000 0001 &
0000 1001 =
0000 0001
```

Boolean operators

| Operator | Meaning               |
| -------- | --------------------- |
| ==       | equal comparison      |
| <        | smaller than          |
| >        | bigger than           |
| <=       | smaller or equal      |
| >=       | bigger or equal       |
| &&       | and                   |
| \|\|     | or                    |
| !        | flip the boolean sign |
| !=       | is not equal          |
| ()       | boolean group         |

Examples

```
false == true = false
false != true = true
!false == true = true
false == !true = true
false || true = true
true || false = true
false || false = false
false && true = false
true && true = true
```

Parentheses (remember && is more dominant than ||)

```
int a = 6
bool b = false
!(5 < a) == true && b // will result true
(!(5 < a) == true) && b // will result false
```

Mathematical operators

| Operator | Meaning                   |
| -------- | ------------------------- |
| =        | asign value to a variable |
| +        | addition                  |
| -        | substraction              |
| \*       | multiplication            |
| /        | devision                  |
| %        | modulo                    |

Shorthands

| Operator | Meaning              |
| -------- | -------------------- |
| +=       | add number to itself |
| ++       | add 1 to itself      |

Examples for any Number

```
i = i + 5
i += 5
i *= 5
i /= 5
```

Addition with 1

```
i = i + 1
i += 1
i ++
```

Substraction with 1

```
i = i - 1
i -= 1
i --
```

# 4. statements

```
int a;
if (conditionA) {
	a = 5;
} else if (conditionB) {
	a = -1;
} else {
	a = 92;
}
```

if else shorthand

```
int a = conditionA? 5: 92;
int a = conditionA? 5: conditionB? -1: 92;
```

# 5. scopes

```
int a = 5;
int b = 8;

if (a < b) {
	int c = 10;
	int b = c + 20; // global b will be ignored
	exec(c + a, b);
} else {
	c // will be undefined
	exec(a + c);
}

int d = c + a; // will be undefined
```

Additional Example

```
int a = 5;
int b = 8;

if (a < b) {
	if (a < 5) {
		int f = 10;
		...
	} else {
		...
	}
	f // will be undefined
} else {
	...
}
```

# 7. Loops

classic loop

```
for (int i = 0; i < 10; i = i + 1) {
	// each time the body updates, you have another i
}
```

logic in the body of the loop

```
for (int i = 0; i < 10; i++) {
	if (a[i] == 100) func(890)
	if (a[i] + 10 == 38) func(234)
	if (a[i] == a[4]) break;
}
```

advance example of loops

```
int SIZE = 10;
int a [SIZE] = {5,4,3,7,8,2,1,0,10,4};

for (int i = 0; i < SIZE/2; i ++) {
	int b = a[i * 2 + 0]; // 0, 2, 4
	int c = a[i * 2 + 1]; // 1, 3, 5
}
```

while

```
int a = 0;
bool b = true;

while (b) {
	a ++;
	if (a == 100) b = false;
}
```

# 6. functions

they give you

1. less writing
2. less changes
3. incapsulation
4. meaningful abstraction

define

```
function moveCursorTo(x, y) {
	let cursor = window.getCursor()
	cursor.x = x
	cursor.y = y
	cursor.move()
	window.update()
}
```

use

```
moveCursorTo(20, 13)
```

void function just does, and returns nothing

```
void doSomething() {
	moveCursorTo(50, 100)
	copy()
	moveCursorTo(20, 1)
	paste()
	refresh()
}
```

return function returns a result

```
bool decide (a, b) {
	if (a + b < 10) {
		return true
	} else {
		return false
	}
}

bool a = decide(4, 1)
```

recursion is a low lever for and while :)

```
let recFunc = (parameter) => {
	parameter += 10
	if (parameter < 100)
		recFunc(parameter)
	return parameter
}

let b = recFunc(2)
```

# 7. collections

array

```
int a [10] = {0, 4, 10};
a[2] // 10
```

object

```
let person = {
	name : 'vasja',
	age: 25,
	eyes: 'brown'
}
person.age // 25
person['age'] // 25

for (let key in person) {
	if (key == 'age' && person[key] == 10)
		person[key] = 46
	if (key == 'eyes')
		person[key] = 'blue'
}
```

# 8. classes

object

```
let door = {
	color : 'red',
	size : [3, 1],
	state : 'closed',
	open () {
		this.state = 'opened'
	},
	close () {
		this.state = 'closed'
	},
	authorizeFor(person) {
		if (person == 'Lena') this.open()
		if (person == 'vasja') this.close()
	}
}

```

class aka object factory

```
class Door {
	String color = 'red';
	int size [2] = [0, 0];
	bool isOpened = false;

	Door (String _color, int _size, bool _initialState) {
		color = _color;
		size = _size;
		if (size[1] < 10)
			initialState = false;
		else {
			initialState = _initialState;
		}
	}

	void open () {
		isOpened = true;
	}

	void close () {
		isOpened = false;
	}

	bool authorizeFor(String person) {
		if (person == 'Sergej') this.open();
		if (person == 'Lena') this.open();
		if (person == 'vasja') this.close();
		return isOpened;
	}
};
```

use class to create object

```
Door Home('Green', [1,3], false);

Home.close()
Home.open()

if (Home.authorizeFor('Sergej')) {
	Serial.println('hey its authorized')
}
```

list of objects

```
Door doors[100] = {
	new Door('red', ...),
	new Door('red', ...),
	new Door('red', ...),
	new Door('red', ...),
	new Door('red', ...),
};
```

class inheritance to reuse code

```
class Animal {
	walk () {}
}

class Dog extends Animal {
	bark () {}
	// walk will be available too!
}

class Cat extends Animal {
	miau () {}

	// extends walk of the super class
	walk () {
		miau()
		super.walk()
	}
}

```

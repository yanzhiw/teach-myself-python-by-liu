## EX 3
### 代码
```
print("数一下我的小鸡：")

print("母鸡", 25 + 30 / 6)
print("公鸡", 100 - 25 * 3 % 4)

print("现在我来数一下鸡蛋：")
print(3 + 2 + 1 - 5 + 4 % 2 - 1 // 4 + 6)

print("3 + 2 < 5 - 7，这是对的吗？")
print(3 + 2 < 5 - 7)

print("What is 3 + 2?", 3 + 2)
print("What is 5 - 7?", 5 - 7)

print("Oh, that's why it's Flase.")

print("How about some more.")
print("Is it greater?", 5 > -2)
print("Is it greater or equal?", 5 >= -2)
print("Is it less or equal?", 5 <= -2)
```

### 运行结果

数一下我的小鸡：
母鸡 30.0
公鸡 97
现在我来数一下鸡蛋：
7
3 + 2 < 5 - 7，这是对的吗？
False
What is 3 + 2? 5
What is 5 - 7? -2
Oh, that's why it's Flase.
How about some more.
Is it greater? True
Is it greater or equal? True
Is it less or equal? False

### 主要区别点

|    区别    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print语法    | pirnt "" |   print()     |
| 整除        |   3/2 输出 1  |   3/2输出 1.5   |
| 是否支持原生中文       |    不支持   |  支持  |

### 注意事项
python3整除需要使用//而不是/。在python3如果使用/作为整除不会报错，需要引起注意，从头脑中把python2的相关概念剔除。
另外尝试了支持原生中文的功能。

## EX 4
### 代码
```
cars = 100
space_in_a_car = 4.0
drivers = 30
passengers = 90
cars_not_driven = cars - drivers
cars_driven = drivers
carpool_capacity = cars_driven * space_in_a_car
average_passengers_per_car = passengers / cars_driven


print("There are", cars, "car available.")
print("There are only", drivers, "drivers available.")
print("There will be", cars_not_driven, "empty cars today.")
print("We can transport", carpool_capacity, "people today.")
print("We have", passengers, "to carpool today.")
print("We need to put about", int(average_passengers_per_car), "in each car.")
```

### 运行结果
There are 100 car available.
There are only 30 drivers available.
There will be 70 empty cars today.
We can transport 120.0 people today.
We have 90 to carpool today.
We need to put about 3 in each car.

### 主要区别点
|    区别    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print语法    | pirnt "" |   print()     |

### 注意事项
我在这里注意到了，```average_passengers_per_car = passengers / cars_driven```在python中输出的是一个整数```3```，而在python3中输出了一个浮点数```3.0```,为了让输出结果保持一致，我用了int语句转了一下格式。

## EX29
### 代码
```
people = 20
cats = 30
dogs = 15

if people < cats:
	print("Too many cats! The world is doomed!")
	
if people > cats:
	print("Not many cats! The world is saved!")

if people < dogs:
	print("The world is doorled on!")

if people > dogs:
	print("The world is dry!")
	
dogs += 5

if people >= dogs:
	print("People are greater than or equal to dogs.")
	
if people <= dogs:
	print("People are less than or equal to dogs.")
	
if people == dogs:
	print("People are dogs.")
```
### 运行结果
Too many cats! The world is doomed!
The world is dry!
People are greater than or equal to dogs.
People are less than or equal to dogs.
People are dogs.
### 主要区别点
|    区别    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print语法    | pirnt "" |   print()     |
### 注意事项
这一段改写是比较轻松的，基本上来说只要注意一下==和=的区别就可以了。事实上我们的自然语言中=并没有赋值的含义，因此在编程中很容易就把自然语言的思维带进来了，在这段代表攥写过程中我也犯了这个错误，阅读后改进了。

## EX33
### 代码
```
i = 0
numbers =[]

while i < 6:
	print("At the top i is %d" % i)
	numbers.append(i)
	
	i += 1
	print("Numbers now: ", numbers)
	print("At the bottom i is %d" % i)
	

print("The numbers:")

for num in numbers:
	print(num)
```
### 运行结果
At the top i is 0
Numbers now:  [0]
At the bottom i is 1
At the top i is 1
Numbers now:  [0, 1]
At the bottom i is 2
At the top i is 2
Numbers now:  [0, 1, 2]
At the bottom i is 3
At the top i is 3
Numbers now:  [0, 1, 2, 3]
At the bottom i is 4
At the top i is 4
Numbers now:  [0, 1, 2, 3, 4]
At the bottom i is 5
At the top i is 5
Numbers now:  [0, 1, 2, 3, 4, 5]
At the bottom i is 6
The numbers:
0
1
2
3
4
5
### 主要区别点
|    区别    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print语法    | pirnt "" |   print()     |
### 注意事项
这个练习的主要注意点是while函数很容易无限循环，要确保整个while语句最后的布尔表达式最后一定会变成false。如果可能的话，尽量用for来运行。

## EX35
### 代码
```
from sys import exit

def gold_room():
	print("This room is full of gold. How much do you take?")
	
	next = input(">")
	if "0" in next or "1" in next:
		how_much = int(next)
	else:
		dead("Man, learn to type a number.")
		
	if how_much < 50:
		print("Nice, you're not greedy,you win!")
	else:
		dead("You greedy bastard!")

def bear_room():
	print("There is a bear here.")
	print("The bear has bunch of honey.")
	print("The fat bear is in front of antoher door.")
	print("How are you going to move the bear.")
	bear_moved = False 
	
	while True:
			next = input(">")
			
			if next == "take honey":
					dead("The bear looks at you then slaps your face off.")
			elif next == "taunt bear" and not bear_moved:
				print("The bear have move from the door. You can go through it now")
				bear_moved = True
			elif next == "taunt bear" and bear_moved:
				dead("The bear gets pissed off and chews your leg off.")
			elif next == "open door" and bear_moved:
				gold_room()
			else:
				print("I got no idea what that means.")
				
def cthulhu_room():
	print("Here you see the great evil Cthulhu.")
	print("He, it, whatever stares at you and you go insane.")
	print("Do you flee for your life or eat you head?")
	
	next = input("> ")
	
	if "flee" in next:
		start()
	elif "head" in next:
		dead("Well that was tasty!")
	else:
		cthulhu_room()
		
def dead(why):
		print(why, "Good job!")
		exit(0)

def start():
	print("You are in a dark room.")
	print("There is a door to you right or left.")
	print("While one do you thke?")
	
	next = input("> ")

	if next == "left":
		bear_room()
	elif next == "right":
		cthulhu_room()
	else:
		dead("You stumble around the room until you starve.")
		
start()
```

### 运行结果
这是一个文字游戏，我完了一次之后结果如下
You are in a dark room.
There is a door to you right or left.
While one do you thke?
There is a bear here.
The bear has bunch of honey.
The fat bear is in front of antoher door.
How are you going to move the bear.
I got no idea what that means.
I got no idea what that means.
The bear looks at you then slaps your face off. Good job!

### 主要区别
### 主要区别点
|    区别    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print语法    | pirnt "" |   print()     |
| 输入   | raw_input |  input   |

### 注意事项
测试的时候发现在bear_room由于没有任何提示，很难想到要输入```take honey```或者```open door```等很抽象的用法，而且阅读代码发现需要绝对等于才有效，也就是说如果我用其他词汇表达相同意思，可能就永远无法解开这个谜题了。我也是阅读代码之后才知道的。
在python2中 raw_input被input替代了，而且恒定认为输出的是字符串。
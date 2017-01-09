## EX 3
### ����
```
print("��һ���ҵ�С����")

print("ĸ��", 25 + 30 / 6)
print("����", 100 - 25 * 3 % 4)

print("����������һ�¼�����")
print(3 + 2 + 1 - 5 + 4 % 2 - 1 // 4 + 6)

print("3 + 2 < 5 - 7�����ǶԵ���")
print(3 + 2 < 5 - 7)

print("What is 3 + 2?", 3 + 2)
print("What is 5 - 7?", 5 - 7)

print("Oh, that's why it's Flase.")

print("How about some more.")
print("Is it greater?", 5 > -2)
print("Is it greater or equal?", 5 >= -2)
print("Is it less or equal?", 5 <= -2)
```

### ���н��

��һ���ҵ�С����
ĸ�� 30.0
���� 97
����������һ�¼�����
7
3 + 2 < 5 - 7�����ǶԵ���
False
What is 3 + 2? 5
What is 5 - 7? -2
Oh, that's why it's Flase.
How about some more.
Is it greater? True
Is it greater or equal? True
Is it less or equal? False

### ��Ҫ�����

|    ����    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print�﷨    | pirnt "" |   print()     |
| ����        |   3/2 ��� 1  |   3/2��� 1.5   |
| �Ƿ�֧��ԭ������       |    ��֧��   |  ֧��  |

### ע������
python3������Ҫʹ��//������/����python3���ʹ��/��Ϊ�������ᱨ����Ҫ����ע�⣬��ͷ���а�python2����ظ����޳���
���Ⳣ����֧��ԭ�����ĵĹ��ܡ�

## EX 4
### ����
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

### ���н��
There are 100 car available.
There are only 30 drivers available.
There will be 70 empty cars today.
We can transport 120.0 people today.
We have 90 to carpool today.
We need to put about 3 in each car.

### ��Ҫ�����
|    ����    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print�﷨    | pirnt "" |   print()     |

### ע������
��������ע�⵽�ˣ�```average_passengers_per_car = passengers / cars_driven```��python���������һ������```3```������python3�������һ��������```3.0```,Ϊ��������������һ�£�������int���ת��һ�¸�ʽ��

## EX29
### ����
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
### ���н��
Too many cats! The world is doomed!
The world is dry!
People are greater than or equal to dogs.
People are less than or equal to dogs.
People are dogs.
### ��Ҫ�����
|    ����    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print�﷨    | pirnt "" |   print()     |
### ע������
��һ�θ�д�ǱȽ����ɵģ���������˵ֻҪע��һ��==��=������Ϳ����ˡ���ʵ�����ǵ���Ȼ������=��û�и�ֵ�ĺ��壬����ڱ���к����׾Ͱ���Ȼ���Ե�˼ά�������ˣ�����δ���߬д��������Ҳ������������Ķ���Ľ��ˡ�

## EX33
### ����
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
### ���н��
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
### ��Ҫ�����
|    ����    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print�﷨    | pirnt "" |   print()     |
### ע������
�����ϰ����Ҫע�����while��������������ѭ����Ҫȷ������while������Ĳ������ʽ���һ������false��������ܵĻ���������for�����С�

## EX35
### ����
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

### ���н��
����һ��������Ϸ��������һ��֮��������
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

### ��Ҫ����
### ��Ҫ�����
|    ����    | python2   |  python3  |
| --------   | -----:  | :----:  |
| print�﷨    | pirnt "" |   print()     |
| ����   | raw_input |  input   |

### ע������
���Ե�ʱ������bear_room����û���κ���ʾ�������뵽Ҫ����```take honey```����```open door```�Ⱥܳ�����÷��������Ķ����뷢����Ҫ���Ե��ڲ���Ч��Ҳ����˵������������ʻ�����ͬ��˼�����ܾ���Զ�޷��⿪��������ˡ���Ҳ���Ķ�����֮���֪���ġ�
��python2�� raw_input��input����ˣ����Һ㶨��Ϊ��������ַ�����
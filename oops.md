## OOPS(object oriented programming) ## 
**needs** 
- If you write a programs in general way without any classes and object the code reusibility and data security will be lose
- By this oops concpets we can organise relatable data and functions in a structured way.
- consider an exampple :
If you are building an company employees data if you write program witout classes and objects whole managers  teamleads and fresher will clumsy
- if you create separate classes for fresher  manger the operations will be easy 

**Class** = Blueprint or design to create an functionality
**Objects** = instances of classes or entity of class 

## class defining : ##
- Class Computer :

## Objects defining : ##
- obj1 = Classname()
- obj2 = Classname() 

### def __init__ method ###
- If you declare any methods in classes we need to call with object name 
- But for this __init__ special method we dont  need to call them separatly
- whenever you create a object it will automatically called as a self parameter 

**Syntax**

- def __init__(self,cpu,ram): #constuctor
    self.cpu = cpu
    self.ram = ram #Assigns to objects here self means object 

**Types of variables**

- **class variable -** These are common for all objects we declare this inside the class

- **instance variable -** These are defined with object name.

**Types of Methods**

-  **Instance method**- These methods can work with instances or classes variables. here we self parameter in method

- **Class methods** - These methods can work with claass variables in this we use (cls) keyword in method.
 - Before class methods we need to declare decoraters above the method **@classmethod .**

- **static method** - If you are not concerned about class variables or instance variables in that case we use static methods. 

- we use this to perform operations with other classes methods.

- we have to use ***@staticmethod** before the static method definition.


## Inner class ##
- IF you want to crete a class but having some related data from another instead of doing that separatly we can crete a inner class init.

```
  class Car:
    def __init__(self,brand,model):
        self.brand = brand
        self.model = model

    def show(self):
        print(self.brand,self.model)

    class Car_function:
        def __init__(self,car,color):
            self.car = car
            self.color = color
        def show(self):
            print(self.car.brand,self.color,self.car.model)

c1 = Car("bmd","mt")
c1.show()
f1 = Car.Car_function(c1,"Blue")
f1.show()

```
- This is how inner class works !

- **NOTE** We need create a variable with outer class name like this "f1 = Car.Car_function(c1)"

## Inheritance ## 
- Inheritance means basically acceppting properties like attributes and methods from parent class 
 - This can be done in different types :

 1. Single inheritance 
 2. Multiple inheritance 
 3. Mutilevel inheritance 
 4. hierarichal inheritance
 5. Hybrid iinheritance

**Example of multiple inheritance**
```
class A:
    def feature1(self):
        print("F1 woring")
    def feature2(self):
        print("F2 woring")
class B:
    def feature3(self):
        print("F3 woring")
    def feature4(self):
        print("F4 woring")
class C(B,A):
    pass
c = C()
c.feature1()
c.feature3()


```
## Constructer in Inheritance ## 
- what if both have constructor (__init__)method in both classes what will happen.

- without super() keyword it calls the same function 

- with **super().__init__()** By using this we can call the parents constructor first and then childs constructor.

```
class A:
    def __init__(self):
        print("A working")

class B(A):
    def __init__(self):
        super().__init__()
        print("B working")
b = B()

```
## Method resolution order ## 
- This means when you are in mutiple iniheritance if you want to call __init__ method the question will raise weather i fetch left class's constructor or right class's constructor.

- Here (MRO) comes into picture it always executes or prefers from left to right.

```
class A:
    def __init__(self):
        print("A working")

class B:
    def __init__(self):
        print("B working")

class C(A,B):
    def __init__(self):
        super().__init__()
        print("C working")
c = C()

```
**What if mutlilevel inheritances** 
- In that case you have to follow MRO order to specify the class names:

```
class A:
    def __init__(self):
        print("A working")

class B(A):
    def __init__(self):
        super().__init__()
        print("B working")

class C(B, A):
    def __init__(self):
        super().__init__()
        print("C working")

c = C()
print(C.__mro__)

```
## Polymorphism(Many ways) ##
- In python we can achieve this in 4 types :
1. Duck typing
2. operator Overloading
3. Method overloading
4. Method overriding 

**Ducktyping**

- Simply we can understand this in different classes we use same method (That means same method with different functionalities.) 

**Operator overloading**

- Basically in python there is some functionalities is prebuild for operators like + ,   * 
- when we click on it in background the __add__ function will runs for some specific data types 
like addition subtraction etc 

- what if we pass two objects predifined functions doesn't know what to do so that in that cases we can define our own methods 

```
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
print(p1 + p2)    # (4, 6)

``` 
## Method overloading ##
- In this we can method overloading by set a value = 0 (default) 
- If you pass value then it overrides or else it does nothing.

```
class Calc:
    def add(self, a, b, c=0):
        return a + b + c

c = Calc()
print(c.add(1, 2))      # 3
print(c.add(1, 2, 3))   # 6

```
## Method Overriding ## 
- If a super class (Parent class) has one method and if child class also use same method name with different functionality That scenario is known as method overrding.
- If you call that method with object its generally runs child's method first 
- If you define super() keyword in the method it will first call the parents and then child.

```
class Vehicle:
    def sound(self):
        print("Some sound")

class Car(Vehicle):
    def sound(self):
        super().sound()           # run the parent's version first
        print("Vroom")

Car().sound()
# Some sound
# Vroom

```
## Abstraction ## 
- Abtraction means hidding the unwnted details like backgroud alogorithms of in built methods in a library 
- By default python doesn't supports abstraction 
- But we can import abs module to achieve abstraction
 ```
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

    def describe(self):                      # normal method, inherited by all
        print(f"Area: {self.area()}, Perimeter: {self.perimeter()}")


class Rectangle(Shape):
    def __init__(self, w, h):
        self.w = w
        self.h = h

    def area(self):
        return self.w * self.h

    def perimeter(self):
        return 2 * (self.w + self.h)


class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return round(3.14159 * self.r ** 2, 2)

    def perimeter(self):
        return round(2 * 3.14159 * self.r, 2)


shapes = [Rectangle(4, 5), Circle(3)]

for s in shapes:
    s.describe()


 ```

## encapsulation ## 

- Encapsulation means bundling data and methods that works on one class from outside classes.
- In python there is no keyords to mention private , protect and public instead of that we use some conventions.

- a = 10 (public) 
- _a = 10 (protect) (we can acccesss form child classes)
- __ = 10 (private)(we cannot modify from outer side even from your child classes)

``` 
class Demo:
    def __init__(self):
        self.a = 1       # public
        self._b = 2      # protected
        self.__c = 3     # private

d = Demo()
print(d.a)     # 1
print(d._b)    # 2
print(d.__c)   # AttributeError

```

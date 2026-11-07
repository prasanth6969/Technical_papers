## SOLID PRINCIPLES ## 
- Solid principles are the design principles that enable us manage most of the software design problems.

- Solid is an acronym of five principles.
- S - single responsibility principle
- O - open closed priciple
- Liskov substitution principle
- Interface segregation principle 
- Dependency Inversion principle 

**SRP** - Every class/function/componenet should do exactly one thing.
- It will be difficult to add or maintain the code which a file has more than 150 lines. 

**OCP(Open Closed principle)** -  The main theme about this principle is if you want to add new features try to extend from already existed like inheritance .

- You should be able to add new behavior without editing existing, tested code.
```
class Square:
    def __init__(self, size):
        self.size = size
    def area(self):
        return self.size * self.size


class Circle:
    def __init__(self, radius):
        self.radius = radius
    def area(self):
        return 3.14 * self.radius * self.radius


def print_area(shape):
    print(shape.area())      # never needs to change

print_area(Square(4))
print_area(Circle(2))


```

**Liskov substitution principle**
- If a recipe says “use any fruit,” then an apple or a banana works. A rock doesn’t, even though someone could call it a “fruit” by mistake.
- This means even if it is a bird or belongs to something but properties have different so that you can write a code according to its abilities and properties.
 ```
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        print("Flying")

class Penguin(Bird):
    def swim(self):
        print("Swimming")

def send_to_sky(bird: FlyingBird):
    bird.fly()
 
 ```

 **Intertface segregation**
 - Dont force classes to have methods they ddon't need.
 ```
class Workable:
    def work(self): ...

class Eatable:
    def eat(self): ...

class Human(Workable, Eatable):
    def work(self):
        print("Working")
    def eat(self):
        print("Eating")

class Robot(Workable):          # only what it needs
    def work(self):
        print("Working")

 ```

## Dependency Inversion ##
- Depend on genral idea rather than a specific thing like when you are in hungry just eat rice and dont care about from where it comes 
```
class Phone:
    def alert(self):
        print("Ring ring")

class Watch:
    def alert(self):
        print("Buzz buzz")

class Person:
    def __init__(self, device):      # any device with alert() works
        self.device = device

    def get_alert(self):
        self.device.alert()

Person(Phone()).get_alert()   # Ring ring
Person(Watch()).get_alert()   # Buzz buzz```

```
| Principle | One-line version | Question to ask yourself |
|---|---|---|
| **S**ingle Responsibility | One class, one job | "Does this class do more than one thing?" |
| **O**pen/Closed | Add new, don't edit old | "Do I have to edit old code to add a feature?" |
| **L**iskov Substitution | Children can replace parents | "Does any child break when used as the parent?" |
| **I**nterface Segregation | Small, focused blueprints | "Am I forcing a class to have methods it can't use?" |
| **D**ependency Inversion | Pass things in, don't hard-code | "Is this class locked to one specific thing?" |
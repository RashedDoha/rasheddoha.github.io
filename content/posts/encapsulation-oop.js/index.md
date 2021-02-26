---
title: "Why some things are best kept private: Encapsulation in OOP"
linktitle: Encapsulation in OOP
publishdate: 2017-07-05
---

![Encapsulation](images/encapsulation-oop.jpeg)

Whenever we come across an introductory or somewhat intermediate text on object oriented programming there’s always someone there to remind us of the importance of encapsulating an object’s member variables. In layman’s terms, that means to make sure that you don’t allow direct access to an object’s members but instead make use of getters and setters. This is of course important, in fact it is one of the four principles of OOP which are-

1. Encapsulation
2. Inheritence
3. Abstraction
4. Polymorphism

The importance and practical usefulness of the last three are usually intuitive and easier to grasp. However, the purpose of the first principle is often abstracted by vague advice such as

> "It’s safer to make everything private."
 
> “It’s best practice. Everyone does it.”

> “Accessing member variables directly can cause major security issues”

While these do sound like the kind of factors you’d want to account for when developing software, as a beginner who’s just getting started. This can feel like something that is “sometimes” or “most of the times” important, but not always. There’s a simple answer to this question of Why should I make my variables private?


Because it allows you to prevent users from setting your object’s properties to invalid values. For example, suppose you have a rectangle object. And it has two properties- height and width.

```java
public class Rectangle {
    public int height;
    public int width;
    public void drawOnCanvas(Canvas c) {
        c.draw(this); 
    }    
}
```

Now if someone was to create a Rectangle object and had the freedom of assigning any heights and widths they wish by using the dot operator, that could mistakenly set a negative value for a positive length and that would prevent your object from drawing or creating a valid rectangle.

This could be solved by making both the length and width private and allowing modifications through a setter method.

```java
public setLength(int length) {
    if(length > 0) this.length = length;
    else this.length = 0; // or some error handling code
}
public getLength() {
    return this.length;
}
```

Now we are saving our code from breaking but this brings us to wonder that perhaps it’s only important when there are a fixed range of valid values for properties. Such as only positive integers for the example above. What if my object doesn’t have any restriction like that. What if I simply have a variable that is valid for whatever value a user might assign by a direct dot operation? 

Here’s a short story that should clear up why it’s the use of encapsulation is not selectively important, but imperative in general.

---

You just joined a new firm which is known for creating wonderful cloud solutions for its customers. Employees of the firm are allowed their own cloud storage for free. But this process is still just getting started. As a simple task, your boss asked you to write a client side program that will allow employees of the organization to write their own code that can access cloud storage space allocated for that employee.

Your boss wants to keep things simple for you, so he says that the backend will reject all invalid size allocations such as negative sizes. So you figure that this is simply a case of writing a storage class with a size property that users are free to access, since the backend will deal with negative sizes, you don’t have to worry about encapsulating them either.

> Boss: “Okay I think I forgot to mention one small thing. Storage space isn’t limitless. I can only afford to provide up to a terabyte of storage for each employee.”

> You: “Wait but you said the server handles invalid values for sizes”

> Boss: “Well yes, but this isn’t really invalid. This is just heavy on the budget. The server doesn’t know that. You have to fix this.”

Oh boy, now you’re in trouble. So what happened was that some employees started allocating excessively large sizes for their cloud storage. While some stayed within the limits. But the problem is, if you fix the code by simply marking the size as private and allowing access through a setter method that checks for sizes exceeding the maximum amount, you break everyone’s code, including the ones that didn’t allocate a wrong size. Since everyone was using the dot operator for access, once you change the code, everyone’s code that had the dot operator access in it, will break. So everyone will have to change their code as well. That might be embarrassing.

This is poor **maintainability**. And the very purpose of **OOP** and **design patterns** in general is to make sure your work is future proof. Meaning, no matter what spec changes come at you in the future, you’ll be safe.

If you started with the size as private and only allowed access via a simple setter method that checked for nothing, all you’d have to do for the second version would be to add the condition in the method and the users who were not assigning invalid sizes wouldn’t have any trouble. Their code would work as if nothing had changes.

Truth is, even the simplest of applications will probably turn into something entirely different down the road. But if you’re careful, then whatever happens, Encapsulation has you covered. So remember, it’s always safe to cover up. _In both life and in code_.
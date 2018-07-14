# Array Methods

![Drawing](http://i.imgur.com/C7v4Nuy.jpg?1)

> We delight in the beauty of the butterfly, but rarely admit the changes it has gone through to achieve that beauty. -[Maya Angelou](https://en.wikipedia.org/wiki/Maya_Angelou)

## Overview

We'll cover various methods that you can use to add, insert, remove, and change elements in an array. 

## Learning Objectives 
- Add element to the end of the array using `append()`
- Insert an element at the specified index using `insert(_:at:)`
- Remove an element at the specified index using `remove(at:)`
- Use _Subscript Syntax_ to change elements at a specified index and access the element at a specified index to store in a variable

# Methods

Take a look at the following:

```swift
let greeting = "Hello"
let loudGreeting = greeting.uppercased()

print(loudGreeting)
// prints "HELLO"
```

This is an example of a 'method', which can be thought of as a pre-written function that helps you accomplish common tasks.

You also saw `.append` in the last lesson, which is another method. Whilst there are some common methods, many are contextual and only work on particular types. For example, a method like `.append` that works on an array will not work for a String, and `.uppercased()` will not work on an array.

The `.append()` method adds a value to the end of an array. You could achieve this in several ways which would involve far more code and calculation, I think you'll agree that `.append()` is far more convenient. There are many other methods for arrays, and in this lesson you'll look at some others.

## Enumeration

Before going any further, there's one other array concept to introduce.

Say you have an array of string literals that represent a list of instructions to create great tea. If you want to print these instructions, you would need to do the following:

```swift
var toMakeTea = [
    "Boil Water",
    "Add tea bag to cup",
    "Wait ten minutes",
    "Add Milk",
    "Drink"
]

print("1\. \(toMakeTea[0])")
print("2\. \(toMakeTea[1])")
// and so on

// prints "1\. Boil Water"
// prints "2\. Add tea bag to cup"
// etc
```

This way of accomplishing the task is incredibly tedious. Knowing how a `for-in` loop works, you can iterate over each value in the array of strings. You also need the index of the value in the array because you want to display numbered instructions.

If steps need to be added, removed, or changed at a particular index in the array, then you also need to know what the index of the value is. When you have a simple list of unchanging values, then maybe this is simple, but with a larger list processed in a loop, there is another way, the `.enumerated` method that you call on an array variable.

```swift

for (index, step) in toMakeTea.enumerated() {
    print("\(index + 1). \(step)")
}

// 1\. Boil Water
// 2\. Add tea bag to cup
// 3\. Wait ten minutes
// 4\. Add Milk
// 5\. Drink
```

In this example you first create an array of the steps to make tea (and yes, there are intentional mistakes!) and add a couple of extra things to the `for in` loop. First, inside the brackets you add variables to hold the index and value variables, the names of these are up to you. Using `index` is of course a useful name, but you can call it whatever you want. At the end of the array variable you want to iterate through, add the `.enumerate()` method. Now inside the loop you have access to the value in the current iteration as well as its index in the array. Above, you add '1' to the index value as unlike computers, humans don't count from 0!

## Check an array has values

Before undertaking any further actions, it's a good idea to check if the array you would like to work with actually has any values in it. Of course there's a method to help, `.isEmpty`.

```swift
if toMakeTea.isEmpty {
   print("No tea yet :(")
} else {
   print("Ready to make tea! :)")
}

// prints "No tea yet :("
```

This method checks to see if the array contains any values, but the array still needs to actually exist (i.e. if you have initiated it) in the first place.

![Array not Initialized](http://i.imgur.com/x82qniD.png)

It might be a good idea to add this check to your array before any other functionality we look at in the rest of the lesson, wrapping it in `if else` statements.

You can reverse a logical check with the `!` symbol:

```swift
if !toMakeTea.isEmpty {
    print("Ready to make tea! :)")
} else {
    print("No tea yet :(")
}
```

This may seem like confusing syntax, but it may feel more natural to start with a preferred or default status and then handle the alternative or fallback status.

## Array Size

There are some methods that help you access certain properties of an array, one is to find the size of an array, or the number of values it contains.

```swift
print(toMakeTea.count)
// 5
```

Just to confuse matters, `.count` returns the number of items in an array starting from 1, not 0\. This makes sense, but might confuse you the first few times you use the method.

As you try some of the other methods mentioned in the rest of this tutorial, try printing `count` throughout your code to see the affect on the array size.

## Add Items to an Array

You saw this method in the last lesson, but let's quickly look at it again. You missed an important step in the list above, telling people to enjoy their tea, so add it to the end of the array:

```swift
toMakeTea.append("Enjoy!")
print(toMakeTea)
// ["Boil Water", "Add tea bag to cup", "Wait ten minutes", "Add Milk", "Drink", "Enjoy!"]
```

The `.append()` method adds a new value (which has to also be the same type as every other value) to the end of the array.

You have also forgotten an important step at the beginning of the list, adding water to the kettle, so let's add it:

```swift
toMakeTea.insert("Add water to kettle", at: 0)

print(toMakeTea)
// ["Add water to kettle", "Boil Water", "Add tea bag to cup", "Wait ten minutes", "Add Milk", "Drink", "Enjoy!"]
```

Note that this doesn't replace the item at index `0`, but **inserts** it, shifting all the elements to the right of it one place in the index.

## Changing items in an array

Uh oh, unless you like strong tea, waiting ten minutes is way too long, so let's change that value:

```swift
toMakeTea[3] = "Wait 3-5 minutes"

print(toMakeTea)
// ["Add water to kettle", "Boil Water", "Add tea bag to cup", "Wait 3-5 minutes", "Add Milk", "Drink", "Enjoy!"]
```

In this example, you use similar syntax to assign the string of text on the right hand side of the `=` to the index in the array on the left hand side, in this case, position `3`.

## Removing items from an array

Drinking tea is a serious business, so you've decided to remove the 'Enjoy!' step. Setting that index in the array's value to be empty, i.e. "", is not enough to remove it, but there's a method that helps.

```swift
toMakeTea.remove(at:6)

print(toMakeTea)
// ["Add water to kettle", "Boil Water", "Add tea bag to cup", "Wait 3-5 minutes", "Add Milk", "Drink"]
```

The `removeAtIndex()` method removes the value in the array at position 6 and then shuffles all the items to the right of the value to the left, which in this case, is no items.

Note that if you try to access or change the value of an index in the array that doesn't exist, you will receive an error. Try these commands in a Playground and see:

```swift
toMakeTea.remove(at:6)
print(toMakeTea[6])
// Error
toMakeTea.remove(at:6)
// Error
```

To prevent this error, you could combine the code above with some `if else` statements and the `count` method you saw earlier in the lesson. For example:

```swift
if toMakeTea.count > 6 {
    toMakeTea.remove(at: 6)
} else {
    print("There is no value at index 6")
}
```

This checks to see if the size of the array is greater than 6, and if so, removes the value at index 6.

---
published: false
title: Introduction to Hashing
categories: [Computer Science, Data Science, Hashing, Machine Learning]
---

![image](/assets/images/hashing.png?raw=true){: .center-image }

## Introduction
Unless your background is in Computer Science, **hashing** is likely one of those ubiquitous terms that you've heard but maybe don't quite understand. If that's the case, then this post is for you.

Imagine you run a company with 20,000 employees. Also imagine you have an up-to-date table called *Employees* that contains key personal information like first name, last name, address, salary, and so on. If you were to run a query to find out if the last name *Ziganto* is in your table, how long would it take? 

Turns out it depends on how you stored the table. If you stored it as a list of lists where your master list is the table and the sublists include key information about each individual employee, then your lookup time can be very long. But how long? You have to consider the worst case scenario. Here, there are 20,000 employees. Let's assume the table is sorted alphabetically by last name. Therefore, *Ziganto* is somewhere at the end, maybe even the last entry. The best we can do with this type of table is a *linear search*, meaning we check to see if the first last name is *Ziganto*. If it is, great, we can stop. If not, move on to the next and check. You keep doing this until you find the last name *Ziganto* or you exhaust your list. The worst case scenario if a full search of the table. If you're familiar with Big O notation, then you know the time complexity is O(n). 

Given modern computing systems, this process of searching 20,000 last names is not a big deal. But imagine you had millions or billions of items to search through employees. The time to search grows linearly with the number of items, hence the term *linear search*. Clearly, this is not optimal. In fact, it's extraordinarily bad. 

The good news is that there's a MUCH better way to do this and it's called **hashing**.

First, a bit of terminology.

## Terminology
You should walk away from this post knowing what the following terms mean and how they work:
* hashing
* key
* hash key 
* hash function 
* collision 
* linear probing 
* chaining

#### Definitions
**Hashing:** to convert a key to a numeric value with the goal of saving or returning a specific record in an array, table, database, etc.

**Key:** any unique, immutable value (e.g. string, integer, tuple).

**Hash Key:** the numeric value returned from a hash function.

**Hash Function:** the process of converting a key to a hash key (used whenever access to an array, table, or database is needed).

> Note: collision, linear probing, and chaining will be covered later.

## Disclaimer
This is only an introduction to hashing. It's a jumping off point really. There are so many cool things you can do with it but for now just get the general idea.

## Our Very Own Hash Function
The best way to learn about hash functions is to build our own. Let's create a little function called *hasher*. I'll explain what it does in a second.

```
import numpy as np

def hasher(key, num_slots):
    '''Simple hashing function that returns hash key.
    Input:
        key: (int or str) thing to hash
        num_slots: (int) number of memory slots to allocate
    Output:
        (int) hash key
    '''
    
    assert type(key) == int or type(key) == str, "key must be an integer or string!"
    assert type(num_slots) == int, "num_slots must be an integer!"
    
    if type(key) == int:
        return key % num_slots
    elif type(key) == str:
        # sum the ASCII values to convert string to integer
        str2int = [ord(char) for char in list(key)]
        return np.sum(str2int) % num_slots
```

The first bit in triple quotes is just a lengthy docstring. It tells us what *key* and *num_slots* are and the expected data types. It also tells us the output of this function, which is an integer representing the hash key.

The assert statements are a quick and dirty way to ensure inputs are of the right type. Specifically, the key must be an integer or string while num_slots must be an integer. Otherwise an assertion error is thrown alerting the user.

Great, now on to the main logic. 

We start with a simple logical check to see if the key is an integer or string. If it's an integer, simply return $key \mod num_slots$. If it's a string, we need to process the text to convert it into numbers. One way to do that is by simply parsing the string into individual characters, returning the ASCII integer for each character, summing all ASCII integers, and applying the mod function. That's precisely what happened in our hasher function with `str2int = [ord(char) for char in list(key)]` and then `np.sum(str2int) % num_slots`. That's all there is to it.

## Examples
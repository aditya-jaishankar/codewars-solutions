# codewars-solutions
My solutions to codewars problems

The problems are arranged in order of increasing difficulty. All problems can be viewed at www.codewars.com

## 1. Find the odd int

Given an array, find the int that appears an odd number of times. There will always be only one integer that appears an odd number of times.

```python

import collections
def find_it(seq):
    d = collections.defaultdict(int)
    for key in seq:
        d[key] += 1
    ints = [key for key in d if d[key]%2 != 0]
    return ints[0]
```

## 2. Stop gninnipS My sdroW!

Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

```python
def spin_words(sentence):
    words = sentence.split()
    new_words = [''.join(reversed(word)) if len(word) > 4 else word for word in words]
    new_sentence = ' '.join(new_words)
    return new_sentence
```

## 3. Categorize new member

The Western Suburbs Croquet Club has two categories of membership, Senior and Open. They would like your help with an application form that will tell prospective members which category they will be placed. To be a senior, a member must be at least 55 years old and have a handicap greater than 7. In this croquet club, handicaps range from -2 to +26; the better the player the lower the handicap.

Input
Input will consist of a list of lists containing two items each. Each list contains information for a single potential member. Information consists of an integer for the person's age and an integer for the person's handicap.

#### Example Input

`[[18, 20],[45, 2],[61, 12],[37, 6],[21, 21],[78, 9]]`

#### Output

Output will consist of a list of string values stating whether the respective member is to be placed in the senior or open category.

```python
def openOrSenior(data):
    l = ['Senior' if pair[0] >= 55 and pair[1] > 7 else 'Open' for pair in data]
    return l
```

## 4. Tribonacci sequence

As the name may already reveal, it works basically like a Fibonacci, but summing the last 3 (instead of 2) numbers of the sequence to generate the next. So, if we are to start our Tribonacci sequence with `[1, 1, 1]` as a starting input (AKA signature), we have this sequence: `[1, 1 ,1, 3, 5, 9, 17, 31, ...]`

But what if we started with `[0, 0, 1]` as a signature? As starting with `[0, 1]` instead of `[1, 1]` basically shifts the common Fibonacci sequence by once place, you may be tempted to think that we would get the same sequence shifted by 2 places, but that is not the case and we would get: `[0, 0, 1, 1, 2, 4, 7, 13, 24, ...]`

Well, you may have guessed it by now, but to be clear: you need to create a fibonacci function that given a signature array/list, returns the first n elements - signature included of the so seeded sequence.

Signature will always contain 3 numbers; n will always be a non-negative number; if `n == 0`, then return an empty array and be ready for anything else which is not clearly specified ;)

```python
def tribonacci(signature, n):
    if n in [0,1,2]:
        return signature[:n]
    else:
        i = 1
        for i in range(1,n-2):
            signature.append(sum(signature[-3:]))
    return signature
```

## 5. Format a string of names like Bart, Lisa & Maggi

Given: an array containing hashes of names

Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.

#### Examples:

```python
namelist([ {'name': 'Bart'}, {'name': 'Lisa'}, {'name': 'Maggie'} ])
# returns 'Bart, Lisa & Maggie'

namelist([ {'name': 'Bart'}, {'name': 'Lisa'} ])
# returns 'Bart & Lisa'

namelist([ {'name': 'Bart'} ])
# returns 'Bart'

namelist([])
# returns ''
```
#### Solution

```python
def namelist(names):
    if len(names) == 1:
        return names[0].get('name')
    elif len(names) == 0:
        return ''
    else:
        listOfNames = [names[i].get('name') for i in range(len(names))]
        pre = str(', '.join(listOfNames[:-1]))
        last = str(listOfNames[-1])
        out = ' & '.join([pre,last])
        return out
```
## 6. Replace with alphabet position

In this kata you are required to, given a string, replace every letter with its position in the alphabet. If anything in the text isn't a letter, ignore it and don't return it. a being 1, b being 2, etc.

As an example: `alphabet_position("The sunset sets at twelve o' clock.")` should return `"20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11"` as a string.

```python
import string
def alphabet_position(s):
    alphabets = string.ascii_lowercase
    d = {alphabet: n+1 for n, alphabet in enumerate(alphabets)}
    sentence = [char.lower() for char in s if char.lower() in alphabets]
    lst = [str(d.get(key)) for key in ''.join(sentence)]
    return ' '.join(lst)
````

## 7. Build tower

Build Tower

Build Tower by the following given argument:
number of floors (integer and always greater than 0).

Tower block is represented as *

for example, a tower of 3 floors looks like below
```python
[
  '  *  ', 
  ' *** ', 
  '*****'
]
```
#### Solution
```python

def tower_builder(total_floors):
    def stars(level): # generates just the stars for arbitrary level
        return ''.join(['*' for i in range(2*level-1)])
    def padded_stars(level, total_floors): # pads the stars with spaces appropriate for that level
        side_padding = ''.join([' ' for j in range(total_floors - level)])
        print(side_padding)
        lst = [side_padding, stars(level), side_padding]
        return ''.join(lst)
    return [padded_stars(level,total_floors) for level in range(1,total_floors+1)]
    # generates the list of padded stars
    
```

## 8. Persistent bugger

Write a function, `persistence`, that takes in a positive parameter `num` and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.

```python
# Not the most elegant solution. Functional programming constructs like reduce might be more elegant.
def persistence(num):
    counter = 0
    while len(str(num)) > 1:
        stnum = str(num)
        lstnum = [int(i) for i in stnum]
        prod = 1
        for j in range(len(str(num))):
            prod *= lstnum[j]
        num = prod
        counter += 1
    return counter
```
## 9. Valid parentheses

Write a function that takes a string of parentheses, and determines if the order of the parentheses is valid. The function should return true if the string is valid, and false if it's invalid.
```python
def valid_parentheses(s):
    flag = 0
    for char in s:
        if char == '(':
            flag += 1
        elif char == ')':
            flag -= 1
            if flag < 0:
                return False
    return flag == 0
```

## 10. Moving zeroes to the end

Write an algorithm that takes an array and moves all of the zeros to the end, preserving the order of the other elements.

```python
def move_zeros(items):
    selected = [item for item in items if item != 0 or item is False]
    # Subtle point about compaing Boolean's here. If I had used ... or item == False, 
    # it evaluates False to 0 and hence treats it as a 0 in the rest of the code. 
    # When comparing Booleans, there are some cases where using 'is' is more valuable. 
    no_of_zeros = len(items) - len(selected)
    zeros = [0] * no_of_zeros
    return selected + zeros
```

## 11. Array difference

Your goal in this kata is to implement a difference function, which subtracts one list from another and returns the result.
It should remove all values from list a, which are present in list. Example: `array_diff([1,2,2,2,3],[2]) == [1,3]`.

```python

def array_diff(a, b):
    return [x for x in a if x not in b] # There are ugly and non-puthonic ways to write this
```

## 12. Simple pig latin

Move the first letter of each word to the end of it, then add "ay" to the end of the word. Leave punctuation marks untouched.

#### Examples
```python
pig_it('Pig latin is cool') # igPay atinlay siay oolcay
pig_it('Hello world !')     # elloHay orldWay !
```

#### Solution

Note: A cleverer solution exists in terms of list comprehensions. 
```python
import string
def pig_it(text):
    words = text.split()
    last_character = words[-1][-1]
    if last_character not in string.ascii_letters:
        del[words[-1]] # Assumes that last character will always be after a space
    new_words = [''.join([word[1:], word[0], 'ay']) for word in words]
    if last_character not in string.ascii_letters:
        new_words.append(last_character)
    return print(' '.join(new_words))
```

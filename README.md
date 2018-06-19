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

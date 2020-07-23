# Vim

- Typing is not the bottleneck !!"Michael"Hill"(GeePawHill) "http://anarchycreek.com/2009/05/26/how-tdd-and-pairing-increase-production/
- Thinking is the bottleneck
- Vim gives me a language to express the changes that I want to make in the most 
  concise, efficient and easy to iterface way that I have ever found.
- I dont speak vim's language, vim speaks my language.
-
- language for defining changes
- optimized for editing texts
- language to express the changes that you want to make concisely, repeatably
    and undoably.


## Syntax of language 

- Verbs (operaitons) + Noun (text on which operation is performed)

```
d for delete
w for word
combine to be "delete word"
```

## Commands are Repeatable and Undoable

```
dot (.) - repeat change
U - undo
```

## Verbs in Vim

```
d => Delete
c => Change (delete and enter insert mode)
> => Indent
v => Visually select
y => Yank (copy)
```

Example:

```
> j : Indent current line and line below
```

## Nouns in Vim -- Motions

```
w => word (forward by a "word")
b => back (back by a "word")  
2j => down 2 lines 
```


## Nouns in Vim -- Text Objects

```
iw => "inner word" (works from anywhere in a word)
it => "inner tag" (the contents of an HTML tag)  
i" => "inner quotes"
ip => "inner paragraph"
as => "a sentence"
```
Example:
```python
result = calculate(['test one', 'test_two'], True)
```

Repeatability
```
Cursor on result
ciw hello
cursor on calculate => dot(.)
```

<div class="users">
  <p>Users List</p
  <ul>
    <li>Hello</li>
    <li>Ben</li>
    <li>Joe</li>
  </ul>
</div>

```
Cursor on Users list => cit
Cursor on closed li tag => dot(.)
Works even if cursor on closed tag and not in middle, works
``` 

## Nouns in Vim -- Parametrized Text Objects

```
f, F => "find" the next character
t, T => "find" the next character (goes upto but does not include )
/ => search
```

Example:
```
ctL
cf'
/ or ?
```

Repeatable eg

## The "dot" command

- Use the more general text object (iw rather than w even if at beginning of the word)
- Prefer text objects to motions when possible
- Repeat.vim for plugin repeating

## Relative number
c6j

## Visual mode is smell

- Breaks repeatability

Example: 
viw c Hello then . (not repeatable)
ciw Hello then . (Repeatable)

## Custom Operators

### Surround
- ds" - delete "surrounding"
- cs"' - change surrounding
- ysiw" - add surrounding

Example: 
- cst```<h2>``` - change surrounding tag 
- if *x>3{ &nbsp; &nbsp; ysW( &nbsp; &nbsp; if ( x>3 ) {
- ysWf print<cr(Enter)> : "hello" -> print("hello")
- In Visual mode, S) -> add surrounding 

### Commentary

### ReplaceWithRegister
griw - replace the inner word

### Titlecase
gti'
gtip

### Sort-motion
gsip

### Indent
cmii - comment inner indent
cmai - comment an indent


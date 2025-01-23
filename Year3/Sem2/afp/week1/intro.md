# Introduction to Agda

You can create a <span style="color:#00bfff">hole</span> with a `?`

When you load Agda it type checks the program

Types are actually called Sets in base Agda
- you can change this. by writing `Type = Set` before the code

### Declaring Types
How to create a <span style="color:#00bfff">Bool</span>
```Agda
data Bool : Type where
 true false : Bool
```

Types are 'first class citizens'

You can have a function that given a Natural number `n`  gives the lists of types with length `n`

`Either` can be seen as a disjoint union
- We have 2 copies of each type

#### Lists
Lists are declared recursively like
```Agda
data List (A : Type) : Type where
 []   : List A
 _::_ : A -> List A -> List A
```

List is a function of Type -> Type

#### Binary Tree
```
data BinTree (A: Type) : Type where
 empty: BinTree A
 fork: A -> BinTree A -> BinTree A -> BinTree A
```

Given a root and 2 BinTrees, it creates a BinTree

### Comments
Comments are done using `--`

### Numbers
Numbers are done using church numerals

`0: zero`
`1: suc(zero)`
`2: suc(suc(zero))`
etc

### Precedence
You can add precedence to operations using <span style="color:#00bfff">infixr</span>

The higher the number the more precedence it has

```
infixr 20 _+_
infixr 30 _*_
```

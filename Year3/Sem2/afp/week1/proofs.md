# Proofs
To prove two functions are equal we can use the triple equal sign

To prove rev is the same as reverse we would do
```Agda
rev-correct : {A: Type} (xs : List A) \r- rev xs \== reverse xs
```

### Proof that $\forall x. x \equiv x$
```Agda
reflexivity : (x : \bN) \r- x \== x
reflexivity zero = *
reflexivity (suc x) = reflexivity x
```

Instead of writing proofs we will be writing programs


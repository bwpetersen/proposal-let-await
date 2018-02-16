# Let Await
Currently, when if a user naively tried to await multiple promises, it will be done so in sequence.
```javascript
let owner = await user.findById(id),
  pets = await pet.findAllByUserId(id)
```
They can await them in parallel if they user `Pormise.all`
```javascript
let [ 
  owner,
  pets
] = await Promise.all([
  user.findById(id),
  pet.findAllByUserId(id)
])
```
The problem with this is that there is a disconnect between the variables and the values they are being assigned.
Let await solves this problem by simply having a `let await` syntax which is equivalent.
```javascript
let await owner = user.findById(id),
  pets = pet.findAllByUserId(id)
```
In general it would convert the following:
```javascript
let await lvalue1 = rvalue1,
  lvalue2 = rvalue2,
  ...,
  lvalueN = rvalueN
```
into the following:
```javascript
let [lvalue1, lvalue2, ..., lvalueN] = Promise.all([rvalue1, rvalue2, ..., rvalueN])
```

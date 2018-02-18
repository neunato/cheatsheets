# Spread

Expands iterables in function calls or array literals.

__Array literals__

```javascript
//const numbers = [1,2,3]
[...numbers]                    // [1,2,3]
[0, ...numbers, 4, 5]           // [0,1,2,3,4,5]
```

__Function arguments__

```javascript
//const numbers = [1,2,3]
Math.max( ...numbers )          // Math.max(1,2,3)
Math.max( 0, ...numbers, 4, 5 ) // Math.max(0,1,2,3,4,5)
```


# Rest

Collects the remaining function arguments or elements of destructuring assignment into an array. Has to be the last element.



__Array destructuring__

```javascript
const [first, second, ...rest] = [1, 2, 3, 4]  // rest is [3, 4]
```

__Function parameter__

```javascript
function f( ...args ){}                // Instead of `args = arguments`.          
function f( first, second, ...rest ){} // Instead of `rest = Array.prototype.slice.call(arguments, 2)`.
```
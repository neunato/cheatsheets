# node.js assert
	
#### ```assert( value[, message] )```

#### ```assert.ok( value[, message] )```

Test if `value` is truthy.  
&nbsp;


#### ```assert.equal( value1, value2[, message] )```

Test for equality between `value1` and `value2` by using `==`.  
&nbsp;


#### ```assert.notEqual( value1, value2[, message] )```

Test for inequality between `value1` and `value2` by using `!=`.  
&nbsp;


#### ```assert.strictEqual( value1, value2[, message] )```

Test for equality between `value1` and `value2` by using `===`.  
&nbsp;


#### ```assert.notStrictEqual( value1, value2[, message] )```

Test for inequality between `value1` and `value2` by using `!==`.  
&nbsp;


#### ```assert.deepEqual( value1, value2[, message] )```

Test for deep equality between `value1` and `value2` by comparing primitive values with `==` and only considering enumerable own properties.  
&nbsp;


#### ```assert.notDeepEqual( value1, value2[, message] )```

Opposite of `deepEqual`.  
&nbsp;


#### ```assert.deepStrictEqual( value1, value2[, message] )```

Test for deep equality between `value1` and `value2` by comparing primitive values with `===` and only considering enumerable own properties. Also, `[[prototype]]`s and type tags (`.toString()`) have to match.  
&nbsp;


#### ```assert.notDeepStrictEqual( value1, value2[, message] )```

Opposite of `deepStrictEqual`.  
&nbsp;


#### ```assert.throws( block[, error][, message] )```

Test if `block` throws an error. `error` can be a constructor (type the thrown error has to match), a `RegExp` (tested against thrown error message), or a validation function (has to return true). If fails, `message` is appended to `AssertionError.message`.  
&nbsp;


#### ```assert.doesNotThrow( block[, error][, message] )```

Test if `block` doesn't throw an error. If it does, and `error` evaluates to  false, the thrown error is propagated to the caller. If evaluates to true, an `AssertionError` is thrown, with `message` appended to `.message`.  
&nbsp;


#### ```assert.fail( message )```

Throw an `AssertionError` with `message` property.  
&nbsp;


#### ```assert.ifError( value )```

Throw `value` if it is truthy.

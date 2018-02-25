# Typed arrays
	
`ArrayBuffer`s represent fixed-length raw binary data; a byte array in physical memory. To read or write its contents, a _view_ is needed. Depending on the data, a view can be a typed array or a `DataView`.

### Typed arrays

When the binary data is aligned in memory in fixed length units of same type, an appropriate typed array should be used:

- `Int8Array`
- `Uint8Array`
- `Uint8ClampedArray` - values clamped to integers in 0-255 range.
- `Int16Array`
- `Uint16Array`
- `Int32Array`
- `Uint32Array`
- `Float32Array`
- `Float64Array`.

A typed array can be constructed from a length, an `ArrayBuffer`, another typed array or an iterable.

```javascript
// From a length.
const view = new Int32Array(10)
view[0] = 37                        // Used like a normal array.

// From an ArrayBuffer.
new Int32Array(view.buffer, 4, 1)   // Int32Array(buffer, byteOffset, length).

// From a typed array.
new Int32Array(view)

// From an iterable.
new Int32Array([23, 37])
```

The following properties are assigned at construction time:

- `.buffer`
- `.byteOffset`
- `.byteLength`
- `.length`

Typed array views use the platform's native byte-order.

### DataView

When a flexible `ArrayBuffer` is needed for data of variable types and widths, or starting from non aligned positions, `DataView` should be used.

```javascript
DataView(buffer, byteOffset, byteLength)
```

```javascript
const buffer = new ArrayBuffer(10)
const view = new DataView(buffer, 3, 4)
view.setUint32(0, 2337, true)
```

Data is manipulated by the following functions of `DataView.prototype`, which give control over the byte-order (defaulting to big endian):

- `.getInt8(offset)` 
- `.getUint8(offset)` 
- `.getInt16(offset, le)` 
- `.getUint16(offset, le)` 
- `.getInt32(offset, le)` 
- `.getUint32(offset, le)` 
- `.getFloat32(offset, le)` 
- `.getFloat64(offset, le)` 
- `.setInt8(offset, value)`
- `.setUint8(offset, value)`
- `.setInt16(offset, value, le)`
- `.setUint16(offset, value, le)`
- `.setInt32(offset, value, le)`
- `.setUint32(offset, value, le)`
- `.setFloat32(offset, value, le)`
- `.setFloat64(offset, value, le)`


The following properties are assigned at construction time:

- `.buffer`
- `.byteOffset`
- `.byteLength`


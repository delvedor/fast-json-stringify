# fast-json-stringify&nbsp;&nbsp;[![Build Status](https://travis-ci.org/mcollina/fast-json-stringify.svg)](https://travis-ci.org/mcollina/fast-json-stringify)

__fast-json-stringify__ is x1-5 times faster than `JSON.stringify()`.
It is particularly suited if you are sending small JSON payloads, the
advantages reduces on large payloads.

Benchmarks:

```
JSON.stringify array x 3,500 ops/sec ±0.91% (85 runs sampled)
fast-json-stringify array x 4,456 ops/sec ±1.68% (87 runs sampled)
JSON.stringify long string x 13,395 ops/sec ±0.88% (91 runs sampled)
fast-json-stringify long string x 95,488 ops/sec ±1.04% (90 runs sampled)
JSON.stringify short string x 5,059,316 ops/sec ±0.86% (92 runs sampled)
fast-json-stringify short string x 12,219,967 ops/sec ±1.16% (91 runs sampled)
JSON.stringify obj x 1,763,980 ops/sec ±1.30% (88 runs sampled)
fast-json-stringify obj x 5,085,148 ops/sec ±1.56% (89 runs sampled)
```

## Example

```js
const fastJson = require('fast-json-stringify')
const stringify = fastJson({
  title: 'Example Schema',
  type: 'object',
  properties: {
    firstName: {
      type: 'string'
    },
    lastName: {
      type: 'string'
    },
    age: {
      description: 'Age in years',
      type: 'integer'
    },
    reg: {
      type: 'string'
    }
  }
})

console.log(stringify({
  firstName: 'Matteo',
  lastName: 'Collina',
  age: 32,
  reg: /"([^"]|\\")*"/
}))
```

## API

### fastJsonStringify(schema)

Build a `stringify()` function based on
[jsonschema](http://json-schema.org/).

Supported types:

 * `'integer'`
 * `'number'`
 * `'array'`
 * `'object'`
 * `'boolean'`
 * `'null'`

And nested ones, too.  

*Specific use cases:*

| Instance   | Serialized as                               |
| -----------|---------------------------------------------|
| `Date`     | `string` <small>via `toISOString()`</small> |
| `RegExp`   | `string`                                    |


## Acknowledgements

This project was kindly sponsored by [nearForm](http://nearform.com).

## License

MIT

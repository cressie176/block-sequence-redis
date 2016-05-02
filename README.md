# block-sequence-redis
A redis implementation of [block-sequence](https://www.npmjs.com/package/block-sequence).

## Usage
```js
var BlockArray = require('block-sequence').BlockArray
var init = require('block-sequence-redis')

// Initialise the redis Block Sequence Driver
init({ host: '127.0.0.1' }, function(err, driver) {
    if (err) throw err

    // Ensure the sequence exists
    driver.ensure({ name: 'my-sequence' }, function(err, sequence) {
        if (err) throw err

        // Create a block array containing 1000 ids per block (defaults to 2 blocks)
        var idGenerator = new BlockArray({ block: { sequence: sequence, driver: driver, size: 1000 } })

        // Grab the next id
        idGenerator.next(function(err, id) {
            if (err) throw err
            console.log(id)
        })
    })
})
```
See https://github.com/NodeRedis/node_redis for all connection parameters



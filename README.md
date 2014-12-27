# poisson-process.js<sup>v0.1.0</sup>

A JavaScript library to generate events in realistically varying time intervals to _improve realism in your games or animations_. For example it can be used to simulate aliens walking by a window or cars trying to drive over your character on a busy road. It can also be used to simulate the frequency of chat messages, page loads or arriving emails as well as queues, traffic and earthquakes.



## Usage

It is simple; you specify an _average call interval_ in milliseconds, a _function to be called_ and then _start_ the process.

    var p = PoissonProcess.create(500, function message() {
      console.log('A message arrived.')
    })
    p.start()

Now the `message` function will be called each 500 milliseconds _in average_. The delay from previous call can vary from near 0 milliseconds to a delay that is significantly longer than the given average, even though the both ends are very unlikely.

The process is paused by:

    p.stop()



## Installation

### Browsers

    <script src="scripts/poisson-process.js"></script>

### CommonJS & Node.js

    $ npm install poisson-process
    ---
    > var PoissonProcess = require('poisson-process');

### AMD & Require.js

    define(['scripts/poisson-process'], function (PoissonProcess) { ... });



## API

### PoissonProcess.create(averageIntervalMs, triggerFunction)

The constructor takes in two parameters. `averageIntervalMs` is an integer and the average interval in milliseconds to call the `triggerFunction`. `triggerFunction` takes no parameters and does not have to return anything.

    var p = PoissonProcess.create(500, function message() {
      console.log('A message arrived.')
    })

### p.start()

Start the process; begin to call the `triggerFunction`.

### p.stop()

Stop the process; do not anymore call the `triggerFunction`.



## Theory

The generator is based on the mathematical concept of Poisson process. It is a process usually perceived in the frequency of earthquakes, arriving mail and, in general, other events where a single event, like an arriving letter, does not much depend on the others.

It is well known that inter-arrival times of the events in a Poisson process follow an exponential distribution with a rate parameter *r*. It is also known that the multiplicative inverse of *r*, *1/r* is the average of the inter-arrival times. Therefore to generate an event each *m* milliseconds in average, we sample the exponential distribution of the rate of *1/m*.

More detailed and enjoyable introduction to the theory is given by [Jeff Preshing](http://preshing.com/) at [How to Generate Random Timings for a Poisson Process](http://preshing.com/20111007/how-to-generate-random-timings-for-a-poisson-process/).



## Versioning

[Semantic Versioning 2.0.0](http://semver.org/)



## License

[MIT License](../blob/master/LICENSE)

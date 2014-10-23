mpw-js
======

mpw-js is a JavaScript + Web Crypto implementation of the Master Password App ([Lyndir/MasterPassword](https://github.com/Lyndir/MasterPassword)) algorithm (<http://masterpasswordapp.com/algorithm.html>).

mpw-js relies on `window.crypto.subtle` when it is avaliable on [modern browser](http://caniuse.com/#feat=cryptography) but will fallback to using [crypto-js](https://code.google.com/p/crypto-js/). It is written in ES6 JS but is transpiled to ES5 JS for browsers that do not yet support ES6 JS. It is purely intended as a proof-of-concept.

The `MPW` constructor `constructor(name, password)` accepts two mandatory arguments; `.name` is set to the argument `name` and both `name` and `password` are subsequently passed to `calculateKey`, `.key` being set to the result.

The `MPW` class implements `static calculateKey(name, password)` which is an implementation of step 1 of the algorithm, *Calculate the __master key__ from a user's name and master password*, it accepts two mandatory arguments, the users full name and the users master password; `calculateKey` is invoked automatically by the constructor.

`MPW` also implements `calculateSeed(site, counter = 0)`, an implementation of step 2 of the algorithm, *Calculate the __template seed__ from the site's name and counter*, it accepts two arguments, the name of the site -- potentially it's FQDN -- and a counter -- *This is an integer that can be incremented when the user needs a new password for the site*; `calculateSeed` is invoked automatically by `generate`.

`MPW` implements `generate(site, counter = 0, template = "long")` which is an implementation of step 3 of the algorithm, *Encode a __site password__ using the site's type template*, it accepts three arguments, the name of the site -- potentially it's FQDN -- and a counter -- *This is an integer that can be incremented when the user needs a new password for the site.* -- which are passed to `calculateSeed`, and `template` which refers to any of the 'Password Type Templates' supported by the algorithm -- maximum, long, medium, short, basic or pin.

`MPW` finally implements `invalidate()` which sets `.key` to a `Promise.reject`, preventing further access to the non-exportable key.

Dependencies
------------

	npm install -g traceur

License
-------

This work is licensed under the Creative Commons Attribution 4.0 International License. To view a copy of this license, visit <http://creativecommons.org/licenses/by/4.0/> or see [LICENSE](https://github.com/tmthrgd/mpw-js/blob/master/LICENSE).
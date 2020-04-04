## ImmutableJS flow types

I've updated the flow types for immutable.js v4

With these updates you should be able to use Immutable.Record
as a class base with strict typing, as:

```js
import * as Immutable from 'immutable';

const Color = |
  'red' |
  'green' |
  'blue' |
  'orange' |
  'yellow' |
  'black' |
  'brown' |
  'pink' |
  'purple';

class User extends Immutable.Record({
  id: null,
  registrationDate: new Date(),
  name: '',
  email: '',
  favoriteColors: Immutable.Set(),
}) {
  id: ?number;
  registrationDate: Date;
  name: string;
  email: string;
  favoriteColors: Immutable.Set<Color>;

  get isValid(): boolean { return this.id !== null; }
}

let user = new User({
  id: 1,
  name: 'Keith Gabryelski',
  email: 'keith@gabryelski.com',
});

console.log('email', user.email); // keith@gabryelski.com

user = user.set('registrationDate', new Date()); // works

user = user.set('registrationDate', null); // Error

user = user.update('favoriteColors', fc => fc.set('blue')); // works
user = user.update('favoriteColors', fc => fc.set('chartreuse')); // fails

```


## Use

replace any immutablejs flow types files (in your flow-typed folder) with
this repository's `immutablejs-flow.js`.

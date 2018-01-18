# Reference vs Copy

Exercises to practice the difference between referencing and copying in JavaScript. Part of Wes Bos'
[JavaScript 30](https://javascript30.com/) course.

## Notes

### Strings, Numbers, and Booleans

When dealing with strings, numbers and Boolean, if you assign them to a variable, set another variable to equal it, and then change the original, the second variable will not be updated.

```js
let age = 100;
let age2 = age;
console.log(age, age2); // 100 100
age = 200;
console.log(age, age2); // 200 100
```

You have made a copy, independent of the original.

### Arrays

Arrays work differently. If you create an array, then set a second array to equal it, then chage the second array, the original array will be updated.

This is because the second array is an array is an array reference, not an array copy. They both point to the same array.

```js
const players = ["Wes", "Sarah", "Ryan", "Poppy"];
const team = players;
console.log(players, team);
// ["Wes", "Sarah", "Ryan", "Poppy"]
// ["Wes", "Sarah", "Ryan", "Poppy"]
team[3] = "Lux";
console.log(players, team);
// ["Wes", "Sarah", "Ryan", "Lux"]
// ["Wes", "Sarah", "Ryan", "Lux"]
```

If you update an array, it will always reference back.

You need to make a copy, not a reference.

You can take the original array and call `.slice()` against it without any paramaters. This will return a copy of the original array.

`const team2 = players.slice();`

Another option is to take an empty array and concatenate in the existing array.

`const team3 = [].concat(players);`

You can also use ES6 spread. Spread takes every item out of your iterable and puts it into the containing array.

`const team4 = [...players];`

Finally, you can use `Array.from()` which also leaves the original array untouched.

`const team5 = Array.from(players);`

### Objects

Objects behave similarly to arrays.

If you create an object, set a second object equal to it, and then change the second object, you will change the original object.

```js
const person = {
  name: "Ger Hynes",
  age: 29
};

const captain = person;
captain.number = 99;
// person {name: "Ger Hynes", age: 29, number: 99}
```

You will have made a reference, not a copy.

To make a copy, use `Object.assign()`.

Start with a blank object. Pass it the object you wish to copy the properties from. Then add in the new properties you want to overwrite. Finally, put it into its own variable.

```js
const cap2 = Object.assign({}, person, { number: 99, age: 12 });
console.log(cap2); // {name: "Ger Hynes", age: 12, number: 99}
```

Object spread should be added soon.
`cap3 = {...person};`

So far, these are very shallow copies. They only go one level deep.

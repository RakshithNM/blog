---
title: Exploring the array reduce method
date: 2021-04-04
published: true
tags: ['js','array method','reduce']
description: "Going through the array reduce function"
---

Reduce is a method on the javascript Array object's prototype. Let us see how it actually works.

The array reduce method executes a callback function on each element of the array and gives a single output value.

```js
const myArray = [1, 2, 3, 4];
const summer = (accumulator, current, currentIndex, sourceArray) => accumulator + current;
console.log(myArray.reduce(summer, 0)); // 10
```
In the above example the `summer` function is called the reducer. On each iteration of the reducer function we iterate over the current value and add it to the accumulator value returned in the last iteration.

The reducer function takes in 4 parameters:
    * the accumulator value - which is the result of the operation in the body of the reducer from the last iteration or
                              the initial value in the first iteration
    * the current value - the current item over which we are iterating
    * the current index - the current index of the item we are iterating over
    * the source array - the array we are iterating over

Let us now look at the custom implementation of the array reduce function

```js
1. function reduce(reducer, initialValue, array) {
2.    let accumulator = initialValue;
3.    for(const item of array) {
4.        accumulator = reducer(accumulator, item);
5.    }
6.    return accumulator;
7. }
```
 Explanation: In line 2 we assign the value of initial value to accumulator. We iterate over the array in line number 3 and in line 4 we call the reducer function passed in on the accumulator value and the current element we are iterating over. The accumulator value in line 4 on the RHS is the initial value in the first iteration and in subsequent iterations it is the output value of calling the reducer on the previous value of the accumulator and the previous iterating item. Once we have completed with the iteration over the array we return the value of the accumulator in line 6.

Some use cases of the array reduce method is listed below:

```js
/*
 * Problem two
 * Turn an array of numbers into a long string of all those numbers
 */

const myArray2 = [1, 2, 3];
const stringifiedArray = myArray2.reduce((a, b) => a + b, '');

console.log(stringifiedArray); // 123
```

```js
/*
 * Problem three
 * Turn an array of voter objects into a count of how many people voted
 */

const voters = [
    {name:'Bob' , age: 30, voted: true},
    {name:'Jake' , age: 32, voted: true},
    {name:'Kate' , age: 25, voted: false},
    {name:'Sam' , age: 20, voted: false},
    {name:'Phil' , age: 21, voted: true},
    {name:'Ed' , age:55, voted:true},
    {name:'Tami' , age: 54, voted:true},
    {name: 'Mary', age: 31, voted: false},
    {name: 'Becky', age: 43, voted: false},
    {name: 'Joey', age: 41, voted: true},
    {name: 'Jeff', age: 30, voted: true},
    {name: 'Zack', age: 19, voted: false}
];

const totalVotes = (inVoters) => {
  const votedUsersArray = inVoters.reduce((a, b) => a + (b.voted ? 1 : 0), 0);
  return votedUsersArray;
};

console.log(totalVotes(voters)); // 7
```

```js
/*
 * Problem four
 * Given an array of all your wishlist items, figure out how much it would cost to just buy everything at once
 */

const wishlist = [
  { title: "Tesla Model S", price: 90000 },
  { title: "4 carat diamond ring", price: 45000 },
  { title: "Fancy hacky Sack", price: 5 },
  { title: "Gold fidgit spinner", price: 2000 },
  { title: "A second Tesla Model S", price: 90000 }
];

const shoppingSpree = (inWishlist) => {
  const totalCost = inWishlist.reduce((a, b) => {
    return a + b.price
  }, 0);
  return totalCost;
}

console.log(shoppingSpree(wishlist)); // 227005
```

```js
/*
 * Problem five
 * Given an array of arrays, flatten them into a single array
 */

var arrays = [
  ["1", "2", "3"],
  [true],
  [4, 5, 6]
];

const flatten = (inArrays) => inArrays.reduce((a, b) => a.concat(b), []);

console.log(flatten(arrays)); // ['1', '2', '3', true, 4, 5, 6]
```

```js
/*
 * Problem six
 * Given an array of potential voters, return an object representing the results of the vote
 * Include how many of the potential voters were in the ages 18-25, how many from 26-35, how many from 36-55, and how many of each of those age ranges actually voted. The resulting object containing this data * should have 6 properties. See the example output at the bottom.
 */

const voters2 = [
  {name:'Bob' , age: 30, voted: true},
  {name:'Jake' , age: 32, voted: true},
  {name:'Kate' , age: 25, voted: false},
  {name:'Sam' , age: 20, voted: false},
  {name:'Phil' , age: 21, voted: true},
  {name:'Ed' , age:55, voted:true},
  {name:'Tami' , age: 54, voted:true},
  {name: 'Mary', age: 31, voted: false},
  {name: 'Becky', age: 43, voted: false},
  {name: 'Joey', age: 41, voted: true},
  {name: 'Jeff', age: 30, voted: true},
  {name: 'Zack', age: 19, voted: false}
];

const voterResults = (inVoters) => {
  const reducedObject = inVoters.reduce((a, b) => {
    if(b.age >= 18 && b.age <= 25 && b.voted) {
      a.numYoungVotes++;
    }
    if(b.age >= 18 && b.age <= 25) {
      a.numYoungPeople++;
    }
    if(b.age >= 26 && b.age <= 35 && b.voted) {
      a.numMidVotesPeople++;
    }
    if(b.age >= 26 && b.age <= 35) {
      a.numMidsPeople++;
    }
    if(b.age >= 36 && b.age <= 55 && b.voted) {
      a.numOldVotesPeople++;
    }
    if(b.age >= 36 && b.age <= 55) {
      a.numOldsPeople++;
    }
    return {...a};
  }, {
    numYoungVotes: 0,
    numYoungPeople: 0,
    numMidVotesPeople: 0,
    numMidsPeople: 0,
    numOldVotesPeople: 0,
    numOldsPeople: 0
  });
  return reducedObject;
};

console.log(voterResults(voters2)); // Returned value shown below:
/*
{ numYoungVotes: 1,
  numYoungPeople: 4,
  numMidVotesPeople: 3,
  numMidsPeople: 4,
  numOldVotesPeople: 3,
  numOldsPeople: 4
}
*/
```

```js
/*
 * Problem seven
 * Return an object where each property is the name of the an ice cream flavor and each value is an integer that is the total count of that flavor.
 * Store the returned data in a new iceCreamTotals variable.
 */

const data = [
  { name: 'Superman', favoriteIceCreams: ['Strawberry', 'Vanilla', 'Chocolate', 'Cookies & Cream'] },
  { name: 'Batman', favoriteIceCreams: ['Cookies & Cream', 'Mint Chocolate Chip', 'Chocolate', 'Vanilla'] },
  { name: 'Flash', favoriteIceCreams: ['Chocolate', 'Rocky Road', 'Pistachio', 'Banana'] },
  { name: 'Aquaman', favoriteIceCreams: ['Vanilla', 'Chocolate', 'Mint Chocolate Chip'] },
  { name: 'Green Lantern', favoriteIceCreams: ['Vanilla', 'French Vanilla', 'Vanilla Bean', 'Strawberry'] },
  { name: 'Robin', favoriteIceCreams: ['Strawberry', 'Chocolate', 'Mint Chocolate Chip'] }
];

const iceCreamTotals = data.reduce((acc, item) => {
  item.favoriteIceCreams.forEach((e) => {
    acc[e] = (acc[e] || 0) + 1;
  });
  return acc;
}, {});

console.log(iceCreamTotals);
/*{
  Strawberry: 3,
  Vanilla: 4,
  Chocolate: 5,
  'Cookies & Cream': 2,
  'Mint Chocolate Chip': 3,
  'Rocky Road': 1,
  Pistachio: 1,
  Banana: 1,
  'French Vanilla': 1,
  'Vanilla Bean': 1
}*/
```

```js
/*
 * Problem eight
 * Given an array, use reduce to calculate the average of sub arrays and print out the averages.
 */

const nums = [
  [1,6,9,2,5,4],
  [50,67,3,80,24,17],
  [100,77,50,35,12,56]
];

const averageSubArray = (inNums) => {
  const average = inNums.map((a) => {
    const averagesub = a.reduce((c, d) => c + d);
    return averagesub / a.length;
  }, [])
  return average;
}

console.log(averageSubArray(nums)); //[ 4.5, 40.166666666666664, 55 ]
```

```js
/*
 * Problem nine
 * Return the number of `true` in the array
 */

const trueArray = [true, false, false, true, true, false];

const countTrue = (inArray) => {
  const count = inArray.reduce((a, b) => a + (b === true ? 1 : 0), 0)
  return count;
};

console.log(countTrue(trueArray)); // 3
```

# Reduce exercises
Simple examples for using reduce function.

## Sum of numbers

Input
```javascript
[1, 2, 3, 4]
```

Output
```javascript
10
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((sum, num) => sum + num);
```
</details>


## Count occurences

Input
```javascript
['a', 'b', 'b']
```

Output
```javascript
{
  a: 1,
  b: 2
}
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((obj, item) => {
  obj[item] = obj[item] ? obj[item] + 1 : 1;

  return obj;
}, {});
```
</details>


## Group items

Input
```javascript
[
  { type: 'a', value: 3 },
  { type: 'b', value: 1 },
  { type: 'b', value: 2 },
]
```

Output
```javascript
{
  a: [
    { type: 'a', value: 3 }
  ],
  b: [
    { type: 'b', value: 1 },
    { type: 'b', value: 2 }
  ]
}
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((obj, item) => {
  if (obj[item.type]){
    obj[item.type].push(item);
  } else {    
    obj[item.type] = [item];
  }

  return obj;
}, {});
```
</details>

## Filter reimplementation

Input
```javascript
const arr = [1, 2, 3, 4];
const callbackFn = (val) => val % 2 === 0;
```

Output
```javascript
[2, 4]
```

<details>
  <summary>Solution</summary>

```javascript
arr.reduce((acc, key) => callbackFn(key) ? [...acc, key] : acc, []);
```
</details>

## Map reimplementation

Input
```javascript
const arr = ['a', 'aa', 'aaa', 'aaaa'];
const callbackFn = (val) => val.length;
```

Output
```javascript
[1, 2, 3, 4]
```

<details>
  <summary>Solution</summary>

```javascript
arr.reduce((acc, key) => [...acc, callbackFn(key)], []);
```
</details>

## Single level flatten

Input
```javascript
[
  1,
  [2, 3],
  4,
  [5, 6]
]
```

Output
```javascript
[1, 2, 3, 4, 5, 6]
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((arr, item) => arr.concat(item), []);
```
</details>


## Item with largest value

Input
```javascript
[
  { id: 1, value: 3 },
  { id: 2, value: 1 },
  { id: 3, value: 2 }
]
```

Output
```javascript
{ id: 1, value: 3 }
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((top, item) => top.value > item.value ? top: item);
```
</details>

## Invert object keys with values

Input
```javascript
{
  a: 1,
  b: 2
}
```

Output
```javascript
{
  '1': 'a',
  '2': 'b'
}
```

<details>
  <summary>Solution</summary>

```javascript
Object.entries(INPUT).reduce((obj, [key, value]) => {
  obj[value] = key;

  return obj;
}, {})
```
</details>

<details>
  <summary>Reduce free solution</summary>

```javascript
Object.fromEntries(Object.entries(INPUT).map(([key, value]) => [value, key]));
```
</details>

## Sum values

Input
```javascript
[
  { day: 'Monday', type: 'Food', value: 10 },
  { day: 'Friday', type: 'Drink', value: 10 },
  { day: 'Friday', type: 'Drink', value: 15 },
  { day: 'Sunday', type: 'Drink', value: 20 },
]
```

Output
```javascript
{
  Drink: {
    Friday: 25,
    Sunday: 20
  },
  Food: {
    Monday: 10
  },
}
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((dict, { day, type, value }) => {
  const typeDict = dict[type] || (dict[type] = {});
  const dayDict = typeDict[day] || (typeDict[day] = 0);

  typeDict[day] += value;

  return dict;
}, {});
```
</details>


## Words from sentences

Input
```javascript
[
  'Lorem ipsum',
  'Hello there',
  'General Kenobi'
]
```

Output
```javascript
['Lorem', 'ipsum', 'Hello', 'there', 'General', 'Kenobi']
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((arr, sentence) => [...arr, sentence.split(' ')], []);
```
</details>

<details>
  <summary>Reduce free solution</summary>

```javascript
INPUT.flatMap((sentence) => sentence.split(' '));
```
</details>


## Promise sequence

Input
```javascript
const starting = 0;
const promises = [
  (val) => Promise.resolve(val + 1),
  (val) => Promise.resolve(val + 2),
  (val) => Promise.resolve(val + 3),
]
```

Output
```javascript
6
```

<details>
  <summary>Solution</summary>

```javascript
promises.reduce((prev, current) => prev.then(current), Promise.resolve(starting));
```
</details>

## Resolve object properties

Input
```javascript
const obj = { a: { b: { c: 3 } } };
const path = ['a', 'b', 'c'];
```

Output
```javascript
3
```

<details>
  <summary>Solution</summary>

```javascript
path.reduce((acc, key) => acc[key], obj);
```
</details>

## Unique items

Input
```javascript
['a', 'b', 'b']
```

Output
```javascript
['a', 'b']
```

<details>
  <summary>Solution</summary>

```javascript
INPUT.reduce((arr, key) => arr.includes(key) ? arr : [...arr, key], input);
```
</details>

<details>
  <summary>Reduce free solution 1</summary>

```javascript
['a', 'b', 'b'].filter(function(item)  {return this[item] ? false : (this[item] = true)}, {})
```
</details>

<details>
  <summary>Reduce free solution 2</summary>

```javascript
[...new Set(['a', 'b', 'b'])]
```
</details>

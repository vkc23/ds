# DS Exercises

# pollyfill for bind
// note: Accepting any number of arguments passed to myBind
Function.prototype.myBind = function (obj, ...args) {
  let func = this;
  // Accepting arguments passed to newFunc
  return function (...newArgs) {
    func.apply(obj, [...args, ...newArgs]);
  };
};

# pollyfill for forEach
var logicAlbums = [
  "Bobby Tarantino",
  "The Incredible True Story",
  "Supermarket",
  "Under Pressure"
];

Array.prototype.myForEach = function (callback) {
  let self = this;
  for (var i = 0; i < self.length; i++) {
    callback(self[i], i, self); // current, index, array
  }
};

logicAlbums.myForEach(function (el) {
  console.log(el);
});


# pollyfill for Map
Array.prototype.myMap = function (callback) {
  let arr = [];
  for (let i = 0; i < this.length; i++) {
    arr.push(callback(this[i], i, this)); //currentEle, index, array
  }
  return arr;
};

const result = logicAlbums.myMap(function (el) {
  return el;
});

# pollyfill for Filter
Array.prototype.myFilter = function (callback, context) {
  let arr = [];
  for (let i = 0; i < this.length; i++) {
    if (callback.call(context, this[i], i, this)) {
      arr.push(this[i]);
    } //currentEle, index, array
  }
  return arr;
};

# pollyfill for Reduce
Array.prototype.myReduce = function (callback, initialValue) {
  var accumulator = initialValue === undefined ? undefined : initialValue;

  for (var i = 0; i < this.length; i++) {
    if (accumulator !== undefined) {
      accumulator = callback.call(undefined, accumulator, this[i], i, this);
    } else {
      accumulator = this[i];
    }
  }
  return accumulator;
};

# find the missing no ?
const arr = [1, 2, 4, 6, 3, 7, 8];
 const findMissingNo = (arr) => {
  let n = arr.length;
  let total = ((n + 1) * (n + 2)) / 2;
  console.log(`total is ${total}`);
  for (let i = 0; i < n; i++)
    total -= arr[i];
  return total;
};
console.log("missing value", findMissingNo(arr));


# Rotate an array by d = 2 element?
 const arr = [1, 2, 3, 4, 5, 6, 7, 8];
const createArr = (arr, start, end) => {
  let temp = [];
  for (let i = start; i < end; i++) {
    temp.push(arr[i]);
  }
  return temp;
};
const firstArr = createArr(arr, 0, d);
const secondArr = createArr(arr, d, arr.length);
console.log(secondArr.concat(firstArr));

# second Method
const rotateLeft = (arr, d) => {
  for (let i = 0; i < d; i++) {
    rotateLeftOne(arr);
  }
};

const rotateLeftOne = (arr) => {
  let temp = arr[0];
  const len = arr.length - 1;
  for (let i = 0; i < len; i++) {
    arr[i] = arr[i + 1];
  }
  arr[len] = temp;
};

rotateLeft(arr, d);
console.log('rotated', arr);


<Note:> Given an array, only rotation operation is allowed on array. We can rotate the array as many times as we want. Return the maximum possible summation of i*arr[i]. </Note>

# Find array sum and i*arr[i] with no rotation
function maxSum(arr, n){
    let arrSum = 0; // Stores sum of arr[i]
    let currVal = 0; // Stores sum of i*arr[i]
    for (let i=0; i<n; i++){
        arrSum = arrSum + arr[i];
        currVal = currVal+(i*arr[i]);
    }
 console.log(arrSum, currVal)
    // Initialize result as 0 rotation sum
    let maxVal = currVal;
 
    // Try all rotations one by one and find
    // the maximum rotation sum.
    for (let j=1; j<n; j++){
        currVal = currVal + arrSum-n*arr[n-j];
        if (currVal > maxVal)
            maxVal = currVal;
    }
    return maxVal;
  }
 let arr = [10, 1, 2, 3, 4, 5, 6, 7, 8, 9];
 let n = arr.length;
console.log("Max", maxSum(arr,n));

# Maximum sum of i*arr[i] among all rotations of a given array
function maxSum(arr, n) {
  var res = Number.MIN_VALUE;
  console.log("res", res);
  for (i = 0; i < n; i++) {
    var curr_sum = 0;
    for (j = 0; j < n; j++) {
      var index = (i + j) % n;
      curr_sum += j * arr[index];
    }
    res = Math.max(res, curr_sum);
  }
  return res;
}
var arr = [3, 2, 1];
var n = arr.length;
console.log(maxSum(arr, n));

# Search an element in a sorted and rotated array
# Note : Instead of two or more pass of binary search the result can be  found in one pass of binary search. The binary search needs to be modified to perform the search. 
The idea is to create a recursive function that takes l and r as range in input and the key. 
# Linear Search - Time Complexity: O(n).
const searchEle = (arr, key) => {
  for (let i = 0; i < arr.length-1; i++) {
    if (arr[i] === key) return i;
  }
};

let ind = searchEle([5, 6, 7, 9, 10, 1, 2, 3], 10);
if (ind != -1) console.log("Index: " + ind);
else console.log("Key not found");

# Second Mathod : Binary search - Time Complexity: O(log n).

const searchEle = (arr, key, low, high) => {
  if (low > high) return -1;
  let mid = Math.floor((low + high) / 2);
  if (key === arr[mid]) return mid;
  else if (arr[low] <= arr[mid]) {
    if (key >= arr[low] && key <= arr[mid])
      return searchEle(arr, key, low, mid - 1);
    else return searchEle(arr, key, mid + 1, high);
  } else {
    if (key >= arr[mid + 1] && key <= arr[high])
      return searchEle(arr, key, mid + 1, high);
    else return searchEle(arr, key, low, mid - 1);
  }
};

// Driver program
let arr = [5, 6, 7, 9, 10, 1, 2, 3];
let n = arr.length;
let key = 3;
let ind = searchEle(arr, key, 0, n - 1);
if (ind != -1) console.log("Index: " + ind);
else console.log("Key not found");

# move all zero in the last
let arr = [1, 2, 0, 0, 0, 3, 6];

const moveZeroToEnd = (arr, n) => {
let count = 0;
for (let i = 0; i < arr.length; i++) {
  if (arr[i] !== 0) {
let temp = arr[count];
    arr[count] = arr[i]
    arr[i] = temp;
    count++
    debugger
  }
 }
return arr;
}
console.log(moveZeroToEnd(arr, arr.length));


# Find the element that appears once in an array where every other element appears twice

// Input: let arr = [7, 3, 5, 4, 5, 3, 4]
// Output: 7

const findElement = arr => {
  return arr.reduce((res, currrentEle) => {
    res = res ^ currrentEle;
    return res;
  }, 0);
};
console.log(findElement([7, 3, 5, 4, 5, 3, 4]));


# Find the two non-repeating elements in an array of repeating elements/ Unique Numbers 2

const findElement = arr => {
  let sum = arr.reduce((res, currrentEle) => {
    res = res ^ currrentEle;
    return res;
  }, 0);
  // Bitwise & the sum with it's 2's Complement Bitwise & will give us the sum containing
  //  only the rightmost set bit
  sum = sum & -sum;
  // console.log(sum & sum);

  let sum1 = 0;
  let sum2 = 0;
  for (let i = 0; i < arr.length; i++) {
    // Bitwise & the arr[i] with the sum Two possibilities either result == 0  or result 0

    if ((arr[i] & sum) > 0) {
      // If result > 0 then arr[i] xored with the sum1
      sum1 = sum1 ^ arr[i];
    } else {
      // If result == 0 then arr[i]
      // xored with sum2
      sum2 = sum2 ^ arr[i];
    }
  }
  console.log(sum1, sum2);
};

let inputArr = [2, 4, 7, 9, 2, 4];
findElement(inputArr);


# Unique element in an array where all elements occur k times except one

const findUnique = (arr, n, k) => {
  let int_bit_size = 4;
  let max_bit_size = int_bit_size * 8;
  let count = Array.from({ length: max_bit_size }, (_, i) => 0);

  for (let i = 0; i < max_bit_size; i++)
    // AND(bitwise) each element of the array with each set digit (one at a time) to get the count of set bits at each position
    for (let j = 0; j < n; j++) if ((arr[j] & (1 << i)) !== 0) count[i] += 1;
  // Now consider all bits whose count is not multiple of k to form the required number.
  let res = 0;
  for (let j = 0; j < n; j++) res += (count[j] % k) * (1 << j);
  return res;
};

let a = [6, 2, 6, 5, 2, 2, 6, 2, 6];
let n = a.length;
let k = 4;
console.log(findUnique(a, n, k));

# -----------------------------------------------------------------------------------------------------
# find prime and none prime no in givin array
inputArr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];

const isPrime = arr => {
  const size = arr.length;
  let primeArr = Array.from({ length: size }, (_, i) => true);
  primeArr[0] = false;
  primeArr[1] = false;
  for (let i = 2; i * i <= size; i++)
    for (let j = 2 * i; j <= size; ) {
      primeArr[j] = false;
      j += i;
    }
  return primeArr;
};

console.log(isPrime(inputArr));

# -------------- Greatest comman division ------------------------------------------
const checkGSD = (a, b) => (a % b === 0 ? b : checkGSD(b, a % b));
console.log(checkGSD(45, 60));


# PPT - DSA Assignment 1

## Answer 1:
```js
const mergeIntervals = (intervals) => {
    intervals.sort((a, b) => a[0] - b[0]);

    for (let i = 1; i < intervals.length; i++) {
        let [x, y] = intervals[i];
        let [prevX, prevY] = intervals[i - 1];

        if (x <= prevY) {
            intervals[i - 1][1] = Math.max(y, prevY);
            intervals.splice(i, 1);
            i--;
        }
    }
    return intervals;
};
```

<br/>

## Answer 2:
```js
const sortColors = (nums) => {
    let zero = 0;
    let one = 0;
    let two = 0;

    for (let n of nums) {
        n === 0 ? zero++ : n === 1 ? one++ : two++;
    }

    for (let i = 0; i < nums.length; i++) {
        i < zero ? (nums[i] = 0) : i < zero + one ? (nums[i] = 1) : (nums[i] = 2);
    }
    return nums;
};
```

<br/>

## Answer 3:
```js
var solution = function (isBadVersion) {
    return function (n) {
        let nBad = n;
        let nGood = 0;
        while (nBad - nGood > 1) {
            let nCurr = Math.round((nBad + nGood) / 2); // center
            if (isBadVersion(nCurr)) {                // only one API call
                nBad = nCurr;
            } else {
                nGood = nCurr;
            }
        }
        return nBad;
    };
};
```

<br/>

## Answer 4:
```js
const maximumGap = (nums) => {
    const n = nums.length;

    if (n < 2) {
        return 0;
    }

    if (n < 3) {
        return Math.abs(nums[0] - nums[1])
    }

    let maxNum = -Infinity;
    let minNum = +Infinity;

    for (let i = 0; i < n; i++) {
        maxNum = Math.max(maxNum, nums[i]);
        minNum = Math.min(minNum, nums[i]);
    }

    if (maxNum === minNum) {
        return 0;
    }

    const k = n - 1;
    const averageGap = (maxNum - minNum) / k;

    const minBuckets = new Array(k);
    const maxBuckets = new Array(k);

    minBuckets[0] = minNum;
    maxBuckets[0] = minNum;

    minBuckets[k - 1] = maxNum;
    maxBuckets[k - 1] = maxNum;

    for (let i = 0; i < n; i++) {
        if (minNum === nums[i] || nums[i] === maxNum) {
            continue;
        }

        const j = Math.floor((nums[i] - minNum) / averageGap);

        minBuckets[j] = minBuckets[j] ? Math.min(minBuckets[j], nums[i]) : nums[i];
        maxBuckets[j] = maxBuckets[j] ? Math.max(maxBuckets[j], nums[i]) : nums[i];
    }

    let largestGap = 0;
    let prevMaxIndex = 0;

    for (let i = 1; i < n - 1; i++) {
        if (minBuckets[i]) {
            largestGap = Math.max(largestGap, minBuckets[i] - maxBuckets[prevMaxIndex]);
        }

        if (maxBuckets[i]) {
            prevMaxIndex = i;
        }
    }

    return largestGap;
}
```

<br/>

## Answer 5:
```js
const containsDuplicate = (nums) => {
    const s = new Set(nums);
    return s.size !== nums.length;
};
```

<br/>

## Answer 6:
```js
const findMinArrowShots = (points) => {
    // Sort the array based on diameter's end location
    let sorted = points.sort((a, b) => a[1] - b[1]);
    let result = 0;

    // Init with very small since the diameter could start from -2^31, alternative solution to init with sorted[0][1] but in this case the result should be initialized with 1 and not 0
    var currEnd = -Infinity;

    for (let [s, e] of sorted) {
        // In case start exceeded the current end ->

        if (s > currEnd) {

            // Update the current end and increase the result -> because arrow hitted all possible overlapped balloons in the current range
            currEnd = e;
            result++;
        }
    }

    // Return result
    return result;
};
```

<br/>

## Answer 7:
```js
const lengthOfLIS = nums => {

    let sequence = Array(nums.length).fill(1);

    for (let i = 0; i <= nums.length; i++) {
        for (let j = i - 1; j >= 0; j--) {

            if (nums[j] < nums[i])
                sequence[i] = Math.max(sequence[i], sequence[j] + 1);
        }
    }
    return Math.max(...sequence);
};
```

<br/>

## Answer 8:
```js
const find132pattern = nums => {
    let m = -Infinity;
    // Initialise a empty stack...
    const stack = [];

    // Run a Loop from last to first index...
    for (let i = nums.length - 1; i >= 0; i--) {
        // If nums[i] is greater than the top element of stack, then pop the element...
        while (nums[i] > stack[stack.length - 1]) {
            m = stack.pop();
        }
        // If m is greater than nums[i], return true...
        if (nums[i] < m) {
            return true;
        }
        // Otherwise, push nums[i] into stack...
        stack.push(nums[i]);
    }
    // If the condition is not satisfied, return false.
    return false;
};
```
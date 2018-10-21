---
title: Closest-pair problem
id: 5951a53863c8a34f02bf1bdc
challengeType: 5
---

## Description
<section id='description'>
Task:
<p>Provide a function to find the closest two points among a set of given points in two dimensions,  i.e. to solve the  <a href="https://en.wikipedia.org/wiki/Closest pair of points problem" title="wp: Closest pair of points problem">Closest pair of points problem</a>  in the  planar  case.</p><p>The straightforward solution is a  O(n<sup>2</sup>)  algorithm  (which we can call brute-force algorithm);  the pseudo-code (using indexes) could be simply:</p>
<pre>
bruteForceClosestPair of P(1), P(2), ... P(N)
if N &lt; 2 then
  return ∞
else
  minDistance ← |P(1) - P(2)|
  minPoints ← { P(1), P(2) }
  foreach i ∈ [1, N-1]
    foreach j ∈ [i+1, N]
      if |P(i) - P(j)| < minDistance then
        minDistance ← |P(i) - P(j)|
        minPoints ← { P(i), P(j) }
      endif
    endfor
  endfor
  return minDistance, minPoints
endif
</pre>
<p>A better algorithm is based on the recursive divide&amp;conquer approach, as explained also at  <a href="https://en.wikipedia.org/wiki/Closest pair of points problem#Planar_case" title="wp: Closest pair of points problem#Planar_case">Wikipedia's Closest pair of points problem</a>,  which is  O(n log n);  a pseudo-code could be:</p>
<pre>
closestPair of (xP, yP)
  where xP is P(1) .. P(N) sorted by x coordinate, and
  yP is P(1) .. P(N) sorted by y coordinate (ascending order)
if N ≤ 3 then
  return closest points of xP using brute-force algorithm
else
  xL ← points of xP from 1 to ⌈N/2⌉
  xR ← points of xP from ⌈N/2⌉+1 to N
  xm ← xP(⌈N/2⌉)<sub>x</sub>
  yL ← { p ∈ yP : p<sub>x</sub> ≤ xm }
  yR ← { p ∈ yP : p<sub>x</sub> &gt; xm }
  (dL, pairL) ← closestPair of (xL, yL)
  (dR, pairR) ← closestPair of (xR, yR)
  (dmin, pairMin) ← (dR, pairR)
  if dL &lt; dR then
    (dmin, pairMin) ← (dL, pairL)
  endif
  yS ← { p ∈ yP : |xm - p<sub>x</sub>| &lt; dmin }
  nS ← number of points in yS
  (closest, closestPair) ← (dmin, pairMin)
  for i from 1 to nS - 1
    k ← i + 1
    while k ≤ nS and yS(k)<sub>y</sub> - yS(i)<sub>y</sub> &lt; dmin
      if |yS(k) - yS(i)| &lt; closest then
        (closest, closestPair) ← (|yS(k) - yS(i)|, {yS(k), yS(i)})
      endif
      k ← k + 1
    endwhile
  endfor
  return closest, closestPair
endif
</pre>
References and further readings:
 <a href="https://en.wikipedia.org/wiki/Closest pair of points problem" title="wp: Closest pair of points problem">Closest pair of points problem</a>
 <a href="http://www.cs.mcgill.ca/~cs251/ClosestPair/ClosestPairDQ.html" title="link: http://www.cs.mcgill.ca/~cs251/ClosestPair/ClosestPairDQ.html">Closest Pair (McGill)</a>
 <a href="http://www.cs.ucsb.edu/~suri/cs235/ClosestPair.pdf" title="link: http://www.cs.ucsb.edu/~suri/cs235/ClosestPair.pdf">Closest Pair (UCSB)</a>
 <a href="http://classes.cec.wustl.edu/~cse241/handouts/closestpair.pdf" title="link: http://classes.cec.wustl.edu/~cse241/handouts/closestpair.pdf">Closest pair (WUStL)</a>
 <a href="http://www.cs.iupui.edu/~xkzou/teaching/CS580/Divide-and-conquer-closestPair.ppt" title="link: http://www.cs.iupui.edu/~xkzou/teaching/CS580/Divide-and-conquer-closestPair.ppt">Closest pair (IUPUI)</a>
<p>For the input, expect the argument to be an array of objects (points) with <code>x</code> and <code>y</code> members set to numbers. For the output, return an object containing the key:value pairs for  <code>distance</code> and <code>pair</code> (i.e., the pair of two closest points).</p>
</section>

## Instructions
<section id='instructions'>

</section>

## Tests
<section id='tests'>

```yml
tests:
  - text: <code>getClosestPair</code> is a function.
    testString: assert(typeof getClosestPair === 'function', '<code>getClosestPair</code> is a function.');
  - text: Distance should be the following.
    testString: assert.equal(getClosestPair(points1).distance, answer1.distance, 'Distance should be the following.');
  - text: Points should be the following.
    testString: assert.deepEqual(JSON.parse(JSON.stringify(getClosestPair(points1))).pair, answer1.pair, 'Points should be the following.');
  - text: Distance should be the following.
    testString: assert.equal(getClosestPair(points2).distance, answer2.distance, 'Distance should be the following.');
  - text: Points should be the following.
    testString: assert.deepEqual(JSON.parse(JSON.stringify(getClosestPair(points2))).pair, answer2.pair, 'Points should be the following.');

```

</section>

## Challenge Seed
<section id='challengeSeed'>

<div id='js-seed'>

```js
const Point = function (x, y) {
  this.x = x;
  this.y = y;
};
Point.prototype.getX = function () {
  return this.x;
};
Point.prototype.getY = function () {
  return this.y;
};

function getClosestPair (pointsArr) {
  // Good luck!
  return true;
}
```

</div>


### After Test
<div id='js-teardown'>

```js
const points1 = [
	new Point(0.748501, 4.09624),
	new Point(3.00302, 5.26164),
	new Point(3.61878,  9.52232),
	new Point(7.46911,  4.71611),
	new Point(5.7819,   2.69367),
	new Point(2.34709,  8.74782),
	new Point(2.87169,  5.97774),
	new Point(6.33101,  0.463131),
	new Point(7.46489,  4.6268),
	new Point(1.45428,  0.087596)
];

const points2 = [
  new Point(37100, 13118),
  new Point(37134, 1963),
  new Point(37181, 2008),
  new Point(37276, 21611),
  new Point(37307, 9320)
];

const answer1 = {
  distance: 0.0894096443343775,
  pair: [
    {
      x: 7.46489,
      y: 4.6268
    },
    {
      x: 7.46911,
      y: 4.71611
    }
  ]
};

const answer2 = {
  distance: 65.06919393998976,
  pair: [
    {
      x: 37134,
      y: 1963
    },
    {
      x: 37181,
      y: 2008
    }
  ]
};

const benchmarkPoints = [
  new Point(16909, 54699),
  new Point(14773, 61107),
  new Point(95547, 45344),
  new Point(95951, 17573),
  new Point(5824, 41072),
  new Point(8769, 52562),
  new Point(21182, 41881),
  new Point(53226, 45749),
  new Point(68180, 887),
  new Point(29322, 44017),
  new Point(46817, 64975),
  new Point(10501, 483),
  new Point(57094, 60703),
  new Point(23318, 35472),
  new Point(72452, 88070),
  new Point(67775, 28659),
  new Point(19450, 20518),
  new Point(17314, 26927),
  new Point(98088, 11164),
  new Point(25050, 56835),
  new Point(8364, 6892),
  new Point(37868, 18382),
  new Point(23723, 7701),
  new Point(55767, 11569),
  new Point(70721, 66707),
  new Point(31863, 9837),
  new Point(49358, 30795),
  new Point(13041, 39745),
  new Point(59635, 26523),
  new Point(25859, 1292),
  new Point(1551, 53890),
  new Point(70316, 94479),
  new Point(48549, 86338),
  new Point(46413, 92747),
  new Point(27186, 50426),
  new Point(27591, 22655),
  new Point(10905, 46153),
  new Point(40408, 84202),
  new Point(52821, 73520),
  new Point(84865, 77388),
  new Point(99819, 32527),
  new Point(34404, 75657),
  new Point(78457, 96615),
  new Point(42140, 5564),
  new Point(62175, 92342),
  new Point(54958, 67112),
  new Point(4092, 19709),
  new Point(99415, 60298),
  new Point(51090, 52158),
  new Point(48953, 58567)
];
```

</div>

</section>

## Solution
<section id='solution'>


```js
const Point = function (x, y) {
  this.x = x;
  this.y = y;
};
Point.prototype.getX = function () {
  return this.x;
};
Point.prototype.getY = function () {
  return this.y;
};

const mergeSort = function mergeSort(points, comp) {
	if(points.length < 2) return points;

	var n = points.length,
		i = 0,
		j = 0,
		leftN = Math.floor(n / 2),
		rightN = leftN;

	var leftPart = mergeSort( points.slice(0, leftN), comp),
		rightPart = mergeSort( points.slice(rightN), comp );

	var sortedPart = [];

	while((i < leftPart.length) && (j < rightPart.length)) {
		if(comp(leftPart[i], rightPart[j]) < 0) {
			sortedPart.push(leftPart[i]);
			i += 1;
		}
		else {
			sortedPart.push(rightPart[j]);
			j += 1;
		}
	}
	while(i < leftPart.length) {
		sortedPart.push(leftPart[i]);
		i += 1;
	}
	while(j < rightPart.length) {
		sortedPart.push(rightPart[j]);
		j += 1;
	}
	return sortedPart;
};

const closestPair = function _closestPair(Px, Py) {
	if(Px.length < 2) return { distance: Infinity, pair: [ new Point(0, 0), new Point(0, 0) ] };
	if(Px.length < 3) {
		//find euclid distance
		var d = Math.sqrt( Math.pow(Math.abs(Px[1].x - Px[0].x), 2) + Math.pow(Math.abs(Px[1].y - Px[0].y), 2) );
		return {
			distance: d,
			pair: [ Px[0], Px[1] ]
		};
	}

	var	n = Px.length,
		leftN = Math.floor(n / 2),
		rightN = leftN;

	var Xl = Px.slice(0, leftN),
		Xr = Px.slice(rightN),
		Xm = Xl[leftN - 1],
		Yl = [],
		Yr = [];
	//separate Py
	for(var i = 0; i < Py.length; i += 1) {
		if(Py[i].x <= Xm.x)
			Yl.push(Py[i]);
		else
			Yr.push(Py[i]);
	}

	var dLeft = _closestPair(Xl, Yl),
		dRight = _closestPair(Xr, Yr);

	var minDelta = dLeft.distance,
		closestPair = dLeft.pair;
	if(dLeft.distance > dRight.distance) {
		minDelta = dRight.distance;
		closestPair = dRight.pair;
	}

	//filter points around Xm within delta (minDelta)
	var closeY = [];
	for(i = 0; i < Py.length; i += 1) {
		if(Math.abs(Py[i].x - Xm.x) < minDelta) closeY.push(Py[i]);
	}
	//find min within delta. 8 steps max
	for(i = 0; i < closeY.length; i += 1) {
		for(var j = i + 1; j < Math.min( (i + 8), closeY.length ); j += 1) {
			var d = Math.sqrt( Math.pow(Math.abs(closeY[j].x - closeY[i].x), 2) + Math.pow(Math.abs(closeY[j].y - closeY[i].y), 2) );
			if(d < minDelta) {
				minDelta = d;
				closestPair = [ closeY[i], closeY[j] ]
			}
		}
	}

	return {
		distance: minDelta,
		pair: closestPair
	};
};

function getClosestPair (points) {
  const sortX = function (a, b) { return (a.x < b.x) ? -1 : ((a.x > b.x) ? 1 : 0); }
  const sortY = function (a, b) { return (a.y < b.y) ? -1 : ((a.y > b.y) ? 1 : 0); }

  const Px = mergeSort(points, sortX);
  const Py = mergeSort(points, sortY);

  return closestPair(Px, Py);
}

```

</section>
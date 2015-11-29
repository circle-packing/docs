# An acceptable worsening of a solution for the circle packing problem, a best-fit algorithm.

Note: everything written here is currently very informal and just as a reminder to myself. Most concepts are better defined in my head. There's also some speculation about possible problems and solutions that have not been tested yet.

# Algorithm

The best-fit algorithm is a constructive solution for the circle packing problem. It does not try to make denser packings than previously found, but tries to find a solution blazingly fast. Thus, we try to find an acceptably worse solution in much less time.

## Initialization

We initialize the solution by placing the first circle at `(0,0)`, the second at `(r1+r2,0)` with `r1` and `r2` the radius of the first and second circle respectively. Lastly we place the third circle tangent to the first two. For these first three circles we choose the biggest ones.

We also initialize a first hole between the first three circles, and three mount-points: `(c1,c2)`, `(c2,c3)`, `(c3, c1)`.

## Holes

A hole is some space between three touching circles. It can be 'filled' by placing a fourth circle in it. This creates 3 new holes: `(c1, c2, c4)`, `(c2, c3, c4)`, `(c3, c1, c4)`. These can then again be filled with smaller circles.

Find the side and middle of a hole the Complex Decartes' Theorem can be used.

## Mount-Points

A mount-point is a point on the outside of the already packed circles. It is defined by two circles, on which a third can be placed.

A simple circle-intersection algorithm can be used to find this point for a given third circle. Of course the circle-intersection will give two solution, however since we defined the mount-point to be on the 'outside' of the packed circles only one of those points will be used.

Speculation:
It's possible that when trying to place a circle in a mount-point an overlap with already packed circled occurs. To solve this it suffices to only look at the 'next' mount-points, to see if the placed circle doesn't overlap with any of the mount-point's circles. The 'next' mount-point are the mount-points that have a circle in common with the current one. If a collision happens there are (as I currently see it) two solution:

* Try to place a smaller circle so no collision occurs anymore. This however doesn't solve the problem in the long-run.
* Place the circle a little further from the center so no more collision occurs. This however creates an n-hole, a hole with more than 3 circles as boundaries and not all of them touching.

A way to solve mount-points: instead of having them, remember a 'shell' (list of circles) on the outside on the packing (keep them clock-wise). When placing a circle on the outside just use any two circles in this shell as the mount-point, then insert the new circle in between those two in the shell. Check for collisions only with the next and previous circle on the shell. If there is a collision with either use that one and the opposite of the original circles as the mount-point. This however will create holes of more than 3 circles (N-Hole).

## N-Holes

These are just speculative at the moment. Not sure how to work with these yet.

Possible solution: Place the new circle tangent to two of the hole-circles, and see if it overlaps any of the others.

## Improvement step

Lastly we can improve the solution by using an off-the-shelf non-linear optimizer with the found solution as the starting state.

#

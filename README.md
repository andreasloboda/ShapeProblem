# ShapeProblem
Very Simple code that checks if a given coordinate is within bounds of a shape; Made for practice.



  Is this point within bounds of a convex polygon?

  Well, first of all, we need to see if the shape is a convex polygon. In order to manage this, the code doesn't care about the order of the points.
Entering points in this order [[1,1], [1,2], [2,2], [2,1]] and in this order [[1,1], [2,2], [1,2], [2,1]] results in the same shape. For a shape to
be considered a polygon, it needs to contain at least three points. If user enters only one or two points, the shape will be rejected immediately.
However, the code doesn't check if any of the entered points share coordinates, or if all of them are in a single line. If enough points have been
entered, it is time to check if the shape is convex. For this, the code divides imaginary plane into four quadrants, with the current point being
their zero-point. Then, the code goes through all the other points and assigns them to the quadrants by their position relative to the current zero-
point. If any of the points has points in all four quadrants, the shape is considered not convex and is rejected. If one of the points happens to be
right between two quadrants, it is assigned to both of them. This logic leads to the shape being considered not convex if two points are entered with
same coordinates or if there's more than two points on an x- or y-axis. The case of multiple points being on a single straight line is not fully solved.

  Once the shape is considered convex, the code memorizes it for further usage. When a new shape is entered, the code first checks if it is convex and
only after that replaces the old one with it. In other words:

  1. Program has only started. Shape is undefined and every attempt to check if point is within it returns false.
  2. We enter a non-convex shape. The program rejects it. Shape is still undefined.
  3. We enter a convex shape A. The program accepts it and correctly determines if points are within it or not.
  4. We enter a non-convex shape. The program rejects it and continues to use shape A.
  5. We enter a convex shape B. The program checks if it's convex. It removes shape A from memory and replaces it with shape B. The program now correctly
  determines if points are within shape B or not.

  Next part is checking if a point P is within the polygon or not. If the point is on the very edge, it is considered to be within the bounds*. In order to
check this, the program has a couple of steps.

  First of all, it defines the four borders - even if we're working with a triangle! The borders are marked n (North), e (East), s (South) and w (west).
For the process of defining borders, we once again use the four quadrants - this time searching for the empty ones. A single point can belong to as many
as three borders simultaneously. Once the borders are defined, we compare the coordinates of point P with the borders, to find the closest points on each
side. For n- and s-borther, we compare the x-axis, and for e- and w-border, we compare the y-axis. Once we find these points, we use the equation
a1/b1=a2/b2 to find the points on the border that share coordinates with the point P. At this point, we check if point P is on the correct side of each
border.

* Due to the nature of computer mathematics, sometimes points that are on the border or very near them might give false positives or negatives. One of the
examples of such behavior is: 1-(0.4*0.5)/0.5 SHOULD be 0.6, but the code calculates it to be 0,600000001 and this leads to point being considered out of
the borders of the polygon even if it's actually on its border. To fix this, I would have to extend the calculating logic.

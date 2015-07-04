SketchSolve can be used to solve solve geometric constraints problems found in CAD software. This project is one of the first geometric constraints solver intended to be used in open source CAD software. Another similar project here on Google code is psketcher. In these problems profiles can be created from primitive objects like points, lines, circles, and arcs. These primitives are subjected to geometric constraints like equal length, concentric arcs and so forth. The solver then solves for a set of primitive parameters that satisfy the sketch constraints.

Currently only 2d sketch problems are supported. However I hope to soon also have a set of 3D part Assembly constraints working. This would make SketchSolve be able to solve complex Assemblies. However, I only plan to write that section of the code if people actually use the 2d solver.

The solution method used is actually a optimization method. The sum of the constraint violations are the objective of the optimization problem. The optimization routine used is a BFGS update Newtons method. An Optimization routine was selected because there are often more or fewer constraint equations than unknowns.

The constraints that are currently supported are the following:

  1. pointOnPoint
  1. pointToLine
  1. pointOnCurve
  1. horizontal
  1. vertical
  1. radiusValue
  1. tangentToArc
  1. tangentToCircle
  1. arcRules
  1. Point to point Distance
  1. Point to point vertical Distance
  1. Point to point horizontal Distance
  1. Point to line Distance
  1. Point to line vertical Distance
  1. Point to line horizontal Distance
  1. lineLength
  1. equalLegnth
  1. arcRadius
  1. equalRadiusArcs
  1. equalRadiusCircles
  1. equalRadiusCircArc
  1. concentricArcs
  1. concentricCircles
  1. concentricCircArc
  1. circleRadius
  1. angle ( between two lines )
  1. parallel
  1. Perpendicular
  1. Colinear Lines
  1. Point On Circle
  1. Point On Arc
  1. Point On midpoint of a line
  1. Point on midpoint of an arc
  1. Point on a quadrant point of a circle
    * +x (parameter = 0)
    * +y (parameter = 1)
    * -x (parameter = 2)
    * -y (parameter = 3)
  1. Points Symmetric about a line
  1. lines Symmetric about a line
  1. Circles Symmetric about a line
  1. Arcs Symmetric about a line


The constraints that will be implemented soon are the following:

  1. others I can't think of right now

Let me know if there are constraints that you use that are not on these lists !!!!

Thanks!
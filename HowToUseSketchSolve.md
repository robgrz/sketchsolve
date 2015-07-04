# Introduction #

Sketch solve is really just intended to be a constraints solving library. I hope that some of you CAD loving people will use the solver in your gui CAD applications. The interface between your applications and sketchsolve will hopefully painless. With only slight modification of sketchsolve from it's current state it will also be able solve assembly constraints for 3d assemblies.

## Primatives ##

In the case of a 2d sketch think of a 2d primitives (points, lines, arcs, and circles) as the skeleton of your model. Well I suppose that for a 2d drawing it is the skeleton and the drawing it's self. Points are made of parameters, in this case doubles precision floating point values. Lines are made up of two points. Arcs are made with three points, START point, END point, CENTER point. Circles are made of the CENTER point and the RADIUS parameter. However, in the end all the parameters that make up the points and the Radius of a circle completely define the skeleton. We want to create an array of these parameters that we will manipulate to satisfy the sketch constraints.

## Define the constraints ##

We also want a way to quickly and easily define the constraint for the solver. For this we will use a structure that is define in the following way:

```
struct constraint
{
        int type;
        point point1;
        point point2;
        line line1;
        line line2;
        circle circle1;
        circle circle2;
        arc arc1;
        arc arc2;
        double *parameter; //radius, length, angle etc...
};
```

Suppose we want to create a constraint to constrain a line to be horizontal. Here is some example code:

```
double parameters[100],constants[100];

point points[100];
line lines[100];

constraint cons[100];

parameters[0]=0;// First point X coordinate
parameters[1]=0;// First point Y coordinate
parameters[2]=10;// Second point X coordinate
parameters[3]=2;// Second point Y coordinate

//Define the first point
points[0].x = &parameters[0]; //Pointer to the X coordinate;
points[0].y = &parameters[1]; //Pointer to the Y coordinate;

//Define the second point
points[1].x = &parameters[2]; //Pointer to the X coordinate;
points[1].y = &parameters[3]; //Pointer to the Y coordinate;

//Define the line
lines[0].point1 = points[0];
lines[0].point2 = points[1];

//Define the constraint
cons[0].type = horizontal; //Make it a horizontal constraint
cons[0].line1 = lines[0]; 

```

For any constraint we simply define the appropriate parameters for that constraint. Note that only pointers to parameters are used.

**NOTE:** Every instance of an arc must have a _arcRules_ constraint added to make sure than resulting arcs are valid. Without this constraint added for every arc in the sketch there is no guarantee that the arc center point will be at the center of the arc, DISASTROUS!!!!!

## Solve the constraints ##

To solve the sketch simply call the solve function with the appropriate parameters. The solve function takes five parameters as shown below:
```
results = solve(parameters, numberOfParameters , constraints , numberOfConstraints)  
```

The parameters argument is a pointer to the parameter array. The numberOfParameters argument is simply the length of the parameters array. The constraints argument is a pointer to the constraint array. The numberOfConstraints argument is simply the length of the constraint array.
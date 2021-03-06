# path_extrude

It extrudes a 2D shape along a path. This module is suitable for a path created by a continuous function.

It depends on the `rotate_p` function and the `polysections` module. Remember to include "rotate_p.scad" and "polysections.scad".

When using this module, you should use points to represent the 2D shape. If your 2D shape is not solid, indexes of triangles are required. See [polysections](https://openhome.cc/eGossip/OpenSCAD/lib-polysections.html) for details.

## Parameters

- `shape_pts` : A list of points represent a shape. See the example below.
- `path_pts` : A list of points represent the path.
- `triangles` : `"SOLID"` (default), `"HOLLOW"` or user-defined indexes. See example below.
- `twist` : The number of degrees of through which the shape is extruded.
- `scale` : Scales the 2D shape by this value over the length of the extrusion. Scale can be a scalar or a vector.
- `closed` : If the first point and the last point of `path_pts` has the same coordinate, setting `closed` to `true` will connect them automatically.

## Examples

	include <rotate_p.scad>;
	include <polysections.scad>;
	include <path_extrude.scad>;
	include <bezier_curve.scad>;

	t_step = 0.05;
	width = 2;

	p0 = [0, 0, 0];
	p1 = [40, 60, 35];
	p2 = [-50, 70, 0];
	p3 = [20, 150, -35];
	p4 = [30, 50, -3];

	shape_pts = [   
		[5, -5],
		[3, 4],
		[0, 5],
		[-5, -5] 
	];

	path_pts = bezier_curve(t_step, 
		[p0, p1, p2, p3, p4]
	);

	path_extrude(shape_pts, path_pts);

![path_extrude](images/lib-path_extrude-1.JPG)

	include <rotate_p.scad>;
	include <polysections.scad>;
	include <path_extrude.scad>;
	include <bezier_curve.scad>;

	t_step = 0.05;
	width = 2;

	p0 = [0, 0, 0];
	p1 = [40, 60, 35];
	p2 = [-50, 70, 0];
	p3 = [20, 150, -35];
	p4 = [30, 50, -3];

	shape_pts = [
		// outer
		[20, 0],
		[18, 9],
		[15, 10],    
		[10, 0],
		// inner
		[18, 2],
		[17, 7],
		[15, 7],
		[12, 2]
	];

	path_pts = bezier_curve(t_step, 
		[p0, p1, p2, p3, p4]
	);

	path_extrude(shape_pts, path_pts, triangles = "HOLLOW");

![path_extrude](images/lib-path_extrude-2.JPG)

	include <rotate_p.scad>;
	include <polysections.scad>;
	include <path_extrude.scad>;
	include <bezier_curve.scad>;
	
	t_step = 0.05;
	width = 2;
	
	p0 = [0, 0, 0];
	p1 = [40, 60, 35];
	p2 = [-50, 70, 0];
	p3 = [20, 150, -5];
	p4 = [50, 50, -3];
	
	shape_pts = [
	    // outer
        [30, 0],
        [15, 10],
	    [10, 0],
	    // inner
        [26, 1],
        [15, 8],
	    [12, 1]
	];
	
	path_pts = bezier_curve(t_step, 
	    [p0, p1, p2, p3, p4]
	);
	
	path_extrude(
	    shape_pts, 
	    path_pts, 	   
	    triangles = [
            [0, 4, 3],
            [0, 1, 4],
            [1, 5, 4],
            [1, 2, 5],
            [2, 3, 5],
            [2, 0, 3]
        ]
	);

![path_extrude](images/lib-path_extrude-3.JPG)





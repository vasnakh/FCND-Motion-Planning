## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`
The intial code was different from backyard flyer with more functionalities defined in `planning_utils.py` and after the quad's armed, the quad takes off and switchs to the PLANNING state, and the planner performs path planning in the function plan_path() with following steps:
These scripts contain a basic planning implementation that includes the following:
1. Load the 2.5D map in the colliders.csv file describing the environment.
2. Discretize the environment into a grid representation.
3. Define the start and goal locations.
4. Perform a search using A* search algorithm.
5. Use a collinearity test to prune the path.
6. Converts the planned path into waypoints, and send the waypoints to simulator.

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
Here I have read the first line and splitted the contents of the line to extract lat0 and lon0 and casted it to floating point values and used the `self.set_home_position()` method to set global home.


And here is a lovely picture of our downtown San Francisco environment from above!
![Map of SF](./misc/map.png)

#### 2. Set your current local position
I retreived the drone's current position in geodetic coordinates from `self.global_position`, and the global home position set from last step from `self.global_home`, then used the utility function `global_to_local()` to convert the current global position to local position.


#### 3. Set grid start position from local position
Instead of setting it to center code is changed to start from the current local position.

#### 4. Set grid goal position from geodetic coords
Changed the code be able to choose any (lat, lon) within the map and have it rendered to a goal location on the grid.

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
I updated the A* implementation to include diagnoal motions on the grid with a cost of sqrt(2). Code is implemented in [lines 58 to 61](planning_utils.py#L58-L61), [89 to 96](planning_utils.py#L89-L96) of `planning_utils.py`.

#### 6. Cull waypoints 
Used colinearity test to prune the path. Code is implemented in [lines 166 to 193](planning_utils.py#L166-L193).





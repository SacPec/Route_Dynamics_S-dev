# Route Dynamics [![Build Status](https://travis-ci.com/metromojo/Route_Dynamics.svg?branch=master)](https://travis-ci.com/metromojo/Route_Dynamics)

![alt text][logo]

[logo]: https://github.com/metromojo/Route_Dynamics/blob/master/Documentation/logo.JPG

`route_dynamics` is a python package created to estimate the energy demand of King County Metro bus routes.
The package implements a simple dynamical model for the bus moving along realistic elevation profiles gathered from LIDAR data. The modular nature of the package facilitates experimentation with different estimations of:

* bus speed and acceleration

* bus stop location

* passenger load

### Use Cases

* **Maintenance Scheduling**:
With a predictive model of module degredation that is route and ridership specific, module replacement can be coordinated with other time intensive maintenance that takes busses out of service and into the shop.

* **Route planning**:
King County contains a wide variety of terrain features, and it is likely that certain routes require more energy than other possibilites that would serve the same riders. This package allows route designers to predict energy demand on numerous route possibilities in different conditions to optimize the fleet distribution.

### Tech. Specs.

The foundation of `route_dynamics` is a `RouteTrajectory` object, that holds route data and wraps a simple Newtonian mechanics model of the bus under force balance between frictional, gravitational, and motive forces. The various components neccesary to compute the energy demand of a particular bus route are:

* **GIS files**: The software first imports geographic information system (GIS) data files containing route coordinates and loads them into GeoPandas DataFrames.

* **Elevation LIDAR data** on King County is loaded for given latitude and longitude coordinate defining a specific route to calculate the route steepness/grade.

* **Bus stop dependent ridership**: Bus stop coordinates and associated ridership for specific routes influence the bus speed, acceleration, and mass that can fluctuate up to 3x the unloaded bus mass when at passenger capacity.

* **Modular integration of bus speed model** will allow for continued development towards parameter-free prediction.
The package is currently equipped with a "speed up, speed limit, slow down" model, which assumes:

    1) the bus stops at all declared bus stops,

    2) the bus accelerates away from bus stops following user-definied accleration profile and decelerates at a constant rate towards oncoming stops,

    3) the bus travels at the speed limit when between stops far enough apart to facilitate acceleration and deceleration.

* **Visualize Subpackage**: All routes can be displayed on interactive maps with elevation in color.

Thanks to modular design, all of the above components can be specified manually to facilitate optimization of route design and energy demand research.


### Work Flow

The battery's power output is predicted from the simple force balance on a bus moving along its route. This dynamical model is contained in the module `route_dynamics/route_elevation/long_dynam_model`, and use is demonstrated in the jupyter notebook `examples/use_example__longi_dynam_model.ipynb`.

The flexibility of the model for setting the passenger load per bus stop is demonstrated the jupyter notebook `examples/use_example__loaded_bus_mass_per_stop.ipynb`.

Total package structure and function are illustrated in notebook `examples/spring_quarter_example.ipynb`.

![alt text][flowchart]

[flowchart]: https://github.com/metromojo/Route_Dynamics/blob/master/Documentation/FlowChart_2020.PNG


### Repository structure

* **route_dynamics**: The package, contains subpackages, modules and tests.

* **Documentation**: Contains project information, such as Use
Cases, work flow, and DIRECT poster

* **data**: King County Metro route shapefiles

* **examples**: Contains example Jupyter notebooks detailing how the package is used.


### Software Dependencies and Packages

* python 3.6
* folium
* geopandas
* matplotlib
* numpy
* pandas
* rasterio
* rasterstats
* branca

A virtual environment is included in the repository called environment.yml.

### Getting Started

1. Use `git clone` to download the repository.
2. [Follow instructions](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file) to set up a conda environment from file `environment.yml`.
3. Download an elevation raster dataset and place it into the repository on your local
machine. The raster file used for the example (seattle_dtm.tif) can be found
[here](https://drive.google.com/open?id=1V8-VIPGcNJ4l7Bd7OYDjIstFb1dsyhxH) with a .uw email address.

#### Have questions?
You can open an Issue or contact the corresponding author: Erica Eggleton (egglee@uw.edu)

### Example Outputs
___

#### Interactive Map:
Route 45
![map]

[map]: https://github.com/metromojo/Route_Dynamics/blob/master/examples/README_results/map45.PNG

#### Example of Load Profile with different constant accelerations:


![acceloutput]

[acceloutput]: https://github.com/metromojo/Route_Dynamics/blob/master/Documentation/Figures/Acceloutput.png

#### Segment of above plot showing loading and unloading:


Green bar indicates maximum loading and unloading power for battery modules
![accelsegment]

[accelsegment]: https://github.com/metromojo/Route_Dynamics/blob/master/Documentation/Figures/Acceloutput_segment.png

#### Example notebook video
Check out a short video that runs through the package functions in the example notebook and shows the corresponding results
[here](https://drive.google.com/open?id=1ZpiIEzNWV0T_pzcjw9jkn3GkSxMLdkwo).


### Acknowledements

We would like to thank Dr. David Beck, Chad Curtis, and all DIRECT 2019 TA's for their
instruction, guidance, and support. We would also like to thank Dr. Dan Schwartz for advising this project.

## Concepts & Architecture

We have created Move Base Flex for a larger target group besides the standard developers and users of move_base and 2D navigation based on costmaps, as well as addressed move_base's limitations. Since robot navigation can be separated into planning and controlling in many cases, even for outdoor scenarios without the benefits of flat terrain, we designed MBF based on ***abstract planner-, controller- and recovery behavior-execution classes for maximal flexibility***. 

To accomplish this goal, we 

1. created abstract base classes for the nav core BaseLocalPlanner, BaseGlobalPlanner and RecoveryBehavior plugin interfaces, extending the API to provide a richer and more expressive interface without breaking the current move_base plugin API. 
***The new abstract interfaces allow plugins to return valuable information in each execution cycle***, e.g. why a valid plan or a velocity command could not be computed. This information is then passed to the external executive logic through MBF planning, navigation or recovering actions’ feedback and result. 

2. The planner, controller and recovery behavior execution is implemented in the abstract execution classes *without* binding the software implementation to 2D costmaps (as in move_base). In our framework, move_base is just a particular implementation of a navigation system: its execution classes implement the abstract ones and bind the system to the costmaps. 
***Thereby, the framework can easily be extended for customized navigation approaches***, e.g. navigation on meshes or 3D occupancy grid maps. However, we provide a SimpleNavigationServer class without a binding to costmaps.

## Flowchart
![MBF architecture](./../img/move_base_flex.png)
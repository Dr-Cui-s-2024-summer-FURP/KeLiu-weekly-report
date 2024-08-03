# Week 7 Report
## Video Demonstration of Multi-robot navigation
-- **Click [here](https://nottinghamedu1-my.sharepoint.com/:v:/g/personal/scykl2_nottingham_edu_cn/EfNp9rG-MRJIsAoBV6zqkugBFrXVd3gSmt_ufK_5GTn7OQ?e=WkFzym) or the picture below** to watch a demonstration video of multi-robot navigation in office envirionment.


  <a href="videos/multi-robot_navigation_office_demo.webm" target="_blank"><img src="images/multi-robot_navigation_office.png" alt="Demo of multi-robot navigation (click to see a video)" width="864" height="540" border="0" /></a>

## Add robots in navigation scenarios

### - In the office example:

- 1. Drag a new robot from assets to the viewport.
- 2. Change the code in the launch file under the path `<your workspace's path>/humble_ws/install/carter_navigation/share/carter_navigation/launch`, in this case `multiple_robot_carter_navigation_office.launch.py`. 

For example, add some code:
```python
    declare_robot4_params_file_cmd = DeclareLaunchArgument(
        "carter4_params_file",
        default_value=os.path.join(
            carter_nav2_bringup_dir, "params", "office", "multi_robot_carter_navigation_params_4.yaml"
        ),
        description="Full path to the ROS2 parameters file to use for robot4 launched nodes",
    )
```
- 3. Create a new file in the path `<your workspace's path>/humble_ws/install/carter_navigation/share/carter_navigation/params/office`, and name it `multi_robot_carter_navigation_params_4.yaml`. In the new file, use the code in similar files and adjust it to set up the parameters for the new robot which is the fourth robot.

- 4. In Isaac Sim, expand the added robot folder in the stage, and ensure that the input value of the node namespace or similar nodes in all the action graphs are properly set such that it corresponds to the code in the launch file.

- 5. Play the USD example in Isaac Sim and then run the launch file in a new terminal after sourcing the ROS2 installation and workspace.

### - In the warehouse example:

- Similarly, follow the steps above to have more robots in the navigation. However, more changes should be made compared with the original launch file `carter_navigation.launch.py`.

-- **Click [here](https://nottinghamedu1-my.sharepoint.com/:v:/g/personal/scykl2_nottingham_edu_cn/EeqSwU_d-zBFn2XzM-k5oIEB-oxSYBaV_KXKdRShjWJOpA?e=tW09gO)** to watch a demonstration video of five robots navigation in the warehouse scenario.


### Solved problems met using the office example

- 1. When running the launch file in the terminal, the system automatically finds the file within the folder `install` in your workspace. If the new launch file is created within other folders, such as `src`, the system will not find it.

- 2. For the newly-added robot, the value for the namespace nodes in its action graphs should properly set as mentioned above. Otherwise, you may encounter errors shown in the following image.

  <a target="_blank"><img src="images/office_error2_1.png" alt="Image showing an error: `Timed out waiting for transform from base_link to map to become available, tf error: Invalid frame ID 'map' passed to canTransform argument target_frame - frame does not exist`" width="864" height="540" border="0" /></a>

- 3. The intial position and pose of the new robot should be the same as the corresponding parameters in the parameters file. Otherwise, what is shown in Isaac Sim can be different from what is shown in the visulization of RViz2.

### Challenges

- After having the fouth robot in the scenario, playing the simulation and running the launch file, it is usually the situation where the map area is black in the RViz window that is shown lastly. It can be solved by setting `export LIBGL_ALWAYS_SOFTWARE=1` in the terminal before running the launch file although this method sometimes fails.

- In the warehouse scenario, the GPU (12G) used does not have enough memory after the number of robots increases to 6, so at most 5 robots can be used for navigation in this scenario.  
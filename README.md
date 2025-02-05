# Normal-Estimation-2d

PCL add-on to compute normal estimation for 2D point clouds.  
This repository provides a `Normal2dEstimation` class that accepts 3D points but ignores the z component.

You can see an example result below:
![normal_illustration](https://user-images.githubusercontent.com/22777836/62471207-79ef0700-b79c-11e9-8c34-2a45c079acce.png)

## Why

The PCL library doesn't support pure 2D points. You have to use 3D points with a z component equal to 0. While many algorithms (like centroid computation, ICP, RANSAC, etc.) work with this trick, normal estimation does not, because all normals end up as (0,0,1).  
My implementation solves this problem by ignoring the z component.

Here you can see the problem with PCL 3D normal estimation: 
![problem_normal](https://user-images.githubusercontent.com/22777836/62474444-30ee8100-b7a3-11e9-9ee8-de2866f65ec8.png)

## Changelog

### 2025-02-05
- **CMake Enhancements:**  
  - Updated CMake configuration to require **C++17** and to follow modern CMake practices.
  - Removed Boost dependency entirely.
  - Made building the executable optional (default is off).
  - The executable target now uses the project name defined in the `project()` command.
- **Header Adjustments:**  
  - Updated header file definitions to use `std::shared_ptr` instead of `boost::shared_ptr` for indices.


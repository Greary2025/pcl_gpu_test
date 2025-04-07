cmake_minimum_required(VERSION 3.5)

project(PCL_GPU_TEST)

# find_package(PCL REQUIRED)
# 指定查找PCL 1.15版本
find_package(PCL 1.15 REQUIRED)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

add_executable (pcl_gpu pcl_gpu.cpp)
target_link_libraries (pcl_gpu ${PCL_LIBRARIES})

# sample.pcd用时
# cpu use :276.346[msec] 
# gpu use :943.197[msec]
# sample.pcd用时
# cpu use :7870.46[msec] 
# gpu use :1180.71[msec] 
# 这个结果和点云的数量有关
# 使用GPU计算法向量时用时最多的是点云邻域搜索这一块，
# 而这一块是用CPU计算的，邻域搜索点设置的越多，计算时间越久，
# 也就是说GPU计算法向量本身的速度是非常快的，用时主要在是用CPU搜索领域这一块。
# 不过在test文件里有利用GPU和八叉树搜索邻域的方法。
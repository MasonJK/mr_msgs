cmake_minimum_required(VERSION 3.8)
project(mr_msgs)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic")
endif()

################################################################################
# Find and load build settings from external packages
################################################################################
find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(geometry_msgs REQUIRED)

################################################################################
# Declare ROS messages, services and actions
################################################################################
set(msg_files
  "msg/RobotPose.msg"
  "msg/FleetRobotPose.msg"
  "msg/MissionData.msg"
  "msg/Log.msg"
)

set(srv_files
  "srv/MissionGoal.srv"
  "srv/MissionStateChange.srv"
  "srv/MissionCancel.srv"
)

# set(action_files
#   "action/SingleGoalMission.action"
# )

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  ${action_files}
  DEPENDENCIES builtin_interfaces geometry_msgs
)

################################################################################
# Macro for ament package
################################################################################
ament_export_dependencies(rosidl_default_runtime)
ament_package()

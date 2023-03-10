cmake_minimum_required(VERSION 3.5)

project(sensor_msgs)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)

set(msg_files
  "msg/BatteryState.msg"
  "msg/CameraInfo.msg"
  "msg/ChannelFloat32.msg"
  "msg/CompressedImage.msg"
  "msg/FluidPressure.msg"
  "msg/Illuminance.msg"
  "msg/Image.msg"
  "msg/Imu.msg"
  "msg/JointState.msg"
  "msg/Joy.msg"
  "msg/JoyFeedback.msg"
  "msg/JoyFeedbackArray.msg"
  "msg/LaserEcho.msg"
  "msg/LaserScan.msg"
  "msg/MagneticField.msg"
  "msg/MultiDOFJointState.msg"
  "msg/MultiEchoLaserScan.msg"
  "msg/NavSatFix.msg"
  "msg/NavSatStatus.msg"
  "msg/Array256.msg"
  "msg/Array512.msg"
  "msg/Array1k.msg"
  "msg/Array4k.msg"
  "msg/Array8k.msg"
  "msg/Array16k.msg"
  "msg/Array32k.msg"
  "msg/Array64k.msg"
  "msg/Array128k.msg"
  "msg/Array256k.msg"
  "msg/PointCloud.msg"
  "msg/PointCloud2.msg"
  "msg/PointCloud1m.msg"
  "msg/PointCloud2m.msg"
  "msg/PointCloud4m.msg"
  "msg/PointCloud512k.msg"
  "msg/PointCloud8m.msg"
  "msg/PointField.msg"
  "msg/Range.msg"
  "msg/RegionOfInterest.msg"
  "msg/RelativeHumidity.msg"
  "msg/Temperature.msg"
  "msg/TimeReference.msg"
)
set(srv_files
  "srv/SetCameraInfo.srv"
)
rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  DEPENDENCIES builtin_interfaces geometry_msgs std_msgs
  ADD_LINTER_TESTS
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_cmake_gtest REQUIRED)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()

  include_directories(include)
  ament_add_gtest(test_sensor_msgs
    test/test_image_encodings.cpp
    test/test_pointcloud_conversion.cpp
    test/test_pointcloud_iterator.cpp)
  if(TARGET test_sensor_msgs)
    rosidl_target_interfaces(test_sensor_msgs ${PROJECT_NAME} "rosidl_typesupport_cpp")
  endif()
endif()

ament_export_dependencies(rosidl_default_runtime)
ament_export_include_directories(include)

ament_package()

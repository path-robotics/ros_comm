# Archived - ROS 1 End-of-life

This repository contains ROS 1 packages.
The last supported ROS 1 release, ROS Noetic, [officially reached end of life on May 31st, 2025](https://bit.ly/NoeticEOL).

## Path Robotics Fork Notes

This repository was forked in September 2025 to address logging issues introduced by [ros/ros_comm#2277]
(https://github.com/ros/ros_comm/pull/2277). The PR was reverted and the library was bumped to 1.17.5.

Since `ros_comm` is a Debian metapackage, only the affected package `xmlrpcpp` needed to be rebuilt and republished.
The following steps accomplished this on Ubuntu 20.04 Focal:

```
# clone and initialize
mkdir -p ~/ros_comm_ws/src
cd ~/ros_comm_ws/src
git clone git@github.com/path-robotics/ros_comm -b noetic-devel
cd ~/ros_comm_ws/src/ros_comm/utilities/xmlrpcpp

# generate debian configuration
bloom-generate rosdebian --ros-distro noetic --os-name ubuntu --os-version focal .

# build and package
dpkg-buildpackage -us -uc -b
```

Once this was completed, the debian file `ros-noetic-xmlrpcpp_1.17.5-0focal_amd64.deb` was created. This package
can be installed alongside the rest of the unmodified `ros_comm` packages.

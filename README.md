# MAVLINK-DDS MSG IDL

## Installation
1. To download FastDDS if you have not
```bash
# Refer to https://fast-dds.docs.eprosima.com/en/latest/installation/sources/sources_linux.html#local-installation-sl

# 3 things to install
# Foonathan memory
# Fast CDR
# Fast DDS

git clone https://github.com/eProsima/foonathan_memory_vendor.git
mkdir -p foonathan_memory_vendor/build && cd foonathan_memory_vendor/build
cmake .. -DCMAKE_INSTALL_PREFIX=/usr/local/ -DBUILD_SHARED_LIBS=ON
sudo cmake --build . --target install

cd
git clone https://github.com/eProsima/Fast-CDR.git
mkdir -p Fast-CDR/build && cd Fast-CDR/build
cmake ..
sudo cmake --build . --target install

cd
git clone https://github.com/eProsima/Fast-DDS.git
mkdir -p Fast-DDS/build && cd Fast-DDS/build
cmake ..
sudo cmake --build . --target install
```

2. Install FastDDSGen
```bash
sudo apt install openjdk-11-jdk
cd
git clone --recursive https://github.com/eProsima/Fast-DDS-Gen.git
cd Fast-DDS-Gen
./gradlew assemble
```

## Run
The executable is in `Fast-DDS-Gen/scripts` named `./fastddsgen`, we must be mindful of a few arguments
- `-replace` = Replaces existing generated files
- `-ppDisable` = Disables the preprocessor
- `-ppPath` = Specifies the preprocessor path
- `-typeros2` = Generates type naming compatible with ROS2
- `-I <path>` = Add directory to preprocessor include paths
- `-d <path>` = Sets an output directory for generated files
- `-cs` = IDL grammar apply case sensitive matching

### Example
```bash
sudo ./fastddsgen \
-I /opt/ros/galactic/share/ \
-d <output_directory> \
-typeros2 \
/opt/ros/$ROS_DISTRO/share/geometry_msgs/msg/PoseStamped.idl 
-cs \
-example CMake
```
- IDL formats can be found inside `/opt/ros/$ROS_DISTRO/share/`
- Do note that `-cs` is needed since ROS2 IDL variables are similar, but are case sensitive
- `-I` is needed since precompilation of files takes place (etc for nested types)
- `-example` is needed so a sample of publisher and subscriber can be used or edited
- Do not include `*Main.cxx` since these are not needed, and they also have main() functions that will cause compile errors 
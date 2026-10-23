# ubuntu server 24.04 for aarch64, preinstalled for raspberry
```https://cdimage.ubuntu.com/ubuntu/releases/24.04/release/ubuntu-24.04.4-preinstalled-server-arm64+raspi.img.xz```
right click on img and use disk image writer on sd card

# if you didn't boot the rpi yet, open sd card content on your pc
open system-boot/network-config to add first boot wifi:
```
  wifis:
    wlan0:
      optional: true
      access-points:
        "partage_de_connexion":
          password: "mdp"
      dhcp4: true
```
open system-boot/user-data set
```ssh_pwauth: true```

in /home/ubuntu/.ssh edit authaurized_keys with own ssh public key :
copy paste cat ~/.ssh/id_rsa.pub

# if it's not the first boot, open sd card content on your pc
for network edit file in /etc/netplan/50-.....yaml
in writable/home/ubuntu/.ssh edit authaurized_keys with own ssh public key :
copy paste cat ~/.ssh/id_rsa.pub

# to find the rpi ip, use the software angry ip scanner on network to find mac adress like 88:A2:9E ....
```ssh ubuntu@<ip>```
change password from ubuntu to 123456

# copy paste to setup and install navigator lib
```
sudo apt update
sudo apt install pip
python3 -m pip install --break-system-packages bluerobotics_navigator
python3 -m pip install --break-system-packages imufusion
python3 -m pip install --break-system-packages scipy
sudo su -c 'curl -fsSL https://raw.githubusercontent.com/bluerobotics/blueos-docker/master/install/boards/configure_board.sh | bash'
sudo apt install python3-rosdep
sudo apt install python3-smbus2
sudo apt install i2c-tools
sudo adduser "$USER" dialout
sudo adduser "$USER" i2c
sudo reboot
```

# ros2 jazzy install (no dev tools, no GUI) follow
```https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html```

# useful commands
cd ros2_ws/
colcon build --packages-select navigator && source install/setup.bash
rosdep install --from-paths src/navigator/ --ignore-src -r -y

# pour opencv
sudo apt install ros-$ROS_DISTRO-cv-bridge
sudo apt install ros-$ROS_DISTRO-sensor-msgs
sudo apt install python3-opencv

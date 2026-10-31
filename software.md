# Software

[Back to the index](README.md)

Every workstation carries the same image, so the versions below are the versions on all ten.

## Base system

| Component | Version |
|---|---|
| Operating system | Ubuntu 24.04 LTS Desktop |
| Kernel | 7.0.0-38-generic, the hardware enablement kernel |
| NVIDIA driver | 580.178.04, open kernel modules |
| CUDA reported by the driver | 13.0 |
| ROS 2 | Jazzy Jalisco |

> **Do not run `do-release-upgrade` on these machines.** Ubuntu advertises a newer release at
> every login. ROS 2 Jazzy targets this release and no other, so accepting that upgrade removes
> the working robotics stack. The distribution is pinned deliberately, not merely the packages.

## Python environments

Two environments are installed, because Isaac Sim requires a different interpreter and a
different build of PyTorch from everything else.

### `/opt/isl-venv`, the default

Python 3.12. This environment is activated automatically in every new terminal, so there is
nothing to set up before starting work.

| Package | Version |
|---|---|
| torch / torchvision | 2.11.0+cu128 / 0.26.0+cu128 |
| trossen-arm | 1.10.0 |
| modern-robotics | 1.1.1 |
| open3d | 0.20.0 |
| mujoco | 3.15.0 |
| pyrealsense2 | 2.58.4.10922 |
| depthai | 3.10.0 |
| scikit-learn | 1.9.1 |
| opencv-python | 4.11.0.86 |

PyTorch is built against CUDA 12.8 while the driver reports 13.0. The driver is backward
compatible, and what matters is that the wheel contains `sm_120` kernels for the RTX 5080.

**`trossen-arm` is pinned to 1.10.0** to match the firmware on the arm controllers. A newer
release will refuse to communicate with them, failing at `configure()`. Leave the pin in place.

### `/opt/isaac-venv`, entered deliberately

Python 3.11, holding Isaac Sim 5.x and Isaac Lab with their own `torch 2.7.0+cu128`. Reach it
through the wrapper rather than by activating it:

```bash
isaac your_script.py
```

Everything outside Isaac runs in `/opt/isl-venv`.

### Installing your own packages

The shared environments are read-only to users, and lab accounts carry no administrative
privileges. For packages of your own, create a virtual environment in your home directory:

```bash
deactivate                      # leave the shared environment first
python3 -m venv ~/myenv
source ~/myenv/bin/activate
```

If something is missing that several people need, ask rather than working around it. Packages
belonging in the shared environment are better installed once on all ten machines.

## ROS 2 and the Interbotix workspace

ROS 2 Jazzy and the Interbotix RX150 packages are sourced automatically in every new terminal.
The workspace is at `/opt/interbotix_ws` and is shared and read-only.

Launching the RX150 description and the control stack:

```bash
ros2 launch interbotix_xsarm_descriptions xsarm_description.launch.py \
  robot_model:=rx150 use_joint_pub_gui:=true

ros2 launch interbotix_xsarm_control xsarm_control.launch.py robot_model:=rx150
```

The WidowX AI does not use ROS. It is commanded directly from Python through `trossen_arm`, as
described in [Machine and robot hardware](hardware.md).

## Simulators

| Simulator | Notes |
|---|---|
| Gazebo Harmonic | The release that pairs with ROS 2 Jazzy, installed through `ros-jazzy-ros-gz` |
| MuJoCo | In `/opt/isl-venv`. Runs on the CPU, so it does not compete with PyTorch for the GPU |
| Isaac Sim 5.x and Isaac Lab | In `/opt/isaac-venv`, reached through the `isaac` wrapper |

Trossen publishes `trossen_arm_mujoco` with WidowX AI assets, which is a reasonable starting
point for simulation work with those arms.

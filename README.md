# Hand_Eye_Extrinsic_Calibration

**This repository is currently in progress.**

MATLAB code for LiDAR-GPS/IMU and Camera-GPS/IMU extrinsic calibration based on hand-eye calibration method.

The extrinsic can be obtained by optimizing `x y z yaw pitch roll` or `x y z qw qx qy qz`. We recommend using quaternions to represent rotation.

## LiDAR to GPS/IMU

### Data Preparation

1. Drive the vehicle in a "$\infty$" shaped trajectory.
2. Record pose estimates of a SLAM algorithm (e.g. [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)) and GPS/IMU pose output. (This can also be done in an offline manner.)

    ```shell
    rosbag record -o out /aft_mapped_to_init_high_frec /novatel/inspvax
    ```

3. Convert rosbag to `.csv` format.
    - Use [rosbag_to_csv](https://github.com/AtsushiSakai/rosbag_to_csv).
    - Change `line 80` in `/scripts/rosbag_to_csv.py`
        from:

        ```python
        stream.write(datetime.fromtimestamp(time.to_time()).strftime('%Y/%m/%d/%H:%M:%S.%f'))
        ```

        to:

        ```python
        stream.write(str(time))
        ```

### Calibration

1. Change filenames of `.csv` files.

    ```matlab
    %% Pose Filename Setup
    filename_1 = "pose1.csv"; % LiDAR Odometry
    filename_2 = "pose2.csv"; % GPS/IMU
    ```

2. Run `main_calibration_L2I_quat.m`

## Camera to GPS/IMU

### Data Preparation



### Calibration

1. Change filenames of `.csv` files.

    ```matlab
    %% Pose Filename Setup
    filename_1 = "pose1.csv"; % Visual Odometry
    filename_2 = "pose2.csv"; % GPS/IMU
    ```

2. Run `main_calibration_C2I_quat.m`

## Reference

1. [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM)
2. [rosbag_to_csv](https://github.com/AtsushiSakai/rosbag_to_csv)
3. [MATLAB-GPS-Calculations](https://github.com/alexbuczynsky/MATLAB-GPS-Calculations)
4. [COLMAP](https://github.com/colmap/colmap)
5. Dornaika F, Horaud R. Simultaneous Robot-World and Hand-Eye Calibration[J]. IEEE Trans Robotics Automat, 1998, 14(4):617-622. [[LINK](https://ieeexplore.ieee.org/document/704233)]

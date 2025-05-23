# piper_ros2
Explanation of piper setup for ROS2_humble


## 動作環境
・ubuntu22.04 humble

## セットアップ
- ワークスペース作成
   ```bash
   mkdir -p piper_ros2/src
   cd piper_ros2/src
   git clone --branch humble https://github.com/agilexrobotics/piper_ros.git
   ```

noeticの場合
   ```bash
   mkdir -p piper_ros2/src
   cd piper_ros2/src
   git clone --branch noetic https://github.com/agilexrobotics/piper_ros.git
   ```

foxyの場合
   ```bash
   mkdir -p piper_ros2/src
   cd piper_ros2/src
   git clone --branch foxy https://github.com/agilexrobotics/piper_ros.git
   ```

- CANモジュールの接続

コンセントもUSB CANもつなげていない状態からコンセントを差し、その後にUSB CANをつなげて、次のコマンドを実行
   ```bash
   bash can_activate.sh can0 1000000
   ```

- ビルド
   ```bash
   colcon build
   source install/setup.bash
   ```
- 制御コードの実行(グリッパー部分の制御も可能)
   ```bash
   ros2 launch piper start_single_piper.launch.py can_port:=can0 auto_enable:=true gripper_exist:=true gripper_val_mutiple:=2
   ```

   ```bash
   ros2 launch piper start_single_piper_rviz.launch.py
   ```
   
⚠️ 青色、黄色の配線の接続不良が原因でpiperとPCが繋がらなくなることがあるので注意

⚠️ 周りの障害物にあたってしまうと自動的にプログラムが終了し、動かなくなるので、その際は、コンセントとUSB CANを抜き、同じ手順でセットアップを再度行う


#  AIServer_for_video
演示了一个AI服务器的应用场景，AI服务器是基于AI芯片硬件加速的，具有如下功能

1. AI Server 通过rtsp协议获取录像机的视频流，进行AI处理（如人脸检测等），并保存AI处理结果。
2. AI处理结果只保存特征数据或者结果标签，同时还可保存快照，用于在检索时快速浏览。
3. 客户端可以检索AI Server的处理结果，并在回放录像时将AI处理结果重新合入视频。


## 运行Server
```
cd data
python3 -m http.server  8000

cd ../snapshot
python3 -m http.server 8001

cd ..
# -v参数挂载当前git目录到docker的home目录
sudo docker run --runtime=nvidia -it -v /home/test/sunqiliang/video_stream_convert:/home stream-test3 bash

# 在docker里运行以下指令
cd /home
python3 AIServerDemo.py live
```

## 客户端运行
```
python3 playGUI.py
```

## 其他命令

```
# 参数为需要处理的录像时间段，分别为开始时间和结束时间,处理后的数据保存在data和snapshot目录下
python AIServerDemo.py  2019_05_27_17_30_00  2019_05_27_17_40_00

# 参数为需要处理的录像时间段，分别为开始时间和结束时间
python3 playDemo.py  2019_05_27_17_30_00  2019_05_27_17_35_00

# 播放录像
python getStream.py  2019_05_27_17_30_00  2019_05_27_17_35_00

# 播放实时流
python getStream.py  -1  -1
```

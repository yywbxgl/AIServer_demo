#  AIServer_for_video

1. AI Server 通过rtsp协议拉取前录像，进行AI处理（如MTCNN人脸检测），并保存AI处理结果。
2. 保存特征数据的同时可保存快照，短视频等用于快速浏览与检索。


## docker server 运行
```
sudo docker run --runtime=nvidia -it -v /home/test/sunqiliang/video_stream_convert:/home stream-test3 bash

cd /home
python AIServerDemo.py live

cd data
python -m http.server  8000

cd ../snapshot
python -m http.server 8001

````



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
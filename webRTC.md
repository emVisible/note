![image-20230703230037125](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703230037125.png)

![image-20230703230241056](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703230241056.png)

![image-20230703230839578](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703230839578.png)

![image-20230703231126716](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703231126716.png)

![image-20230703231329825](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703231329825.png)

---



WebRTC采用p2p传输

# 核心概念

## 轨 && 流

轨 Track

- 音频与视频不相交

- 音频与音频之间，视频与视频之间不相交

媒体流 MediaStream

- 音频轨
- 视频轨
- 字幕轨

## WebRTC重要的类

MediaStream 流 

RTCPeerConnection 大而全的类，应用层使用便捷 

RTCDataChannel 非音视频数据传输，通过PeerConnection引入

## PeerConnection调用过程

![image-20230703232055858](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703232055858.png)

## 调用时序图

![image-20230703232410999](C:\Users\16193\AppData\Roaming\Typora\typora-user-images\image-20230703232410999.png)
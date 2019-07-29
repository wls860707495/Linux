# Opencv-Keypoint
## 描述
```
sift算法使用的是模板匹配，而模板的特征点是固定的，每次进行计算将消耗大量的资源，而将特征点进行保存则会节省大量的计算时间。
```
## 问题
```
python中有一种轻量级的对象存储方式shelve，但是只能对基本的数据类型进行存储，故不能存储使用sift算法计算出的特征点对象。

```
## 解决方案
将每个KeyPoint对象中的属性值（包括pt、size、angle、response、octave）加入到列表中利用shelve进行保存，之后分别创建KeyPoint对象进行取出，即可解决问题。
### 存储部分
```
index = []
for point in all_kd[1][0]:
    temp = (point.pt, point.size, point.angle, point.response, point.octave,
     point.class_id)
    index.append(temp)

print(all_kd[1][0])

with shelve.open('character.txt') as f:
    f['kps'] = index
    f['des'] = all_kd[1][1]
```
### 取出部分
```
with shelve.open('character.txt')as f:
    index2 = f.get('kps')
    des1 = f.get('des')
    kp1 = []
for point in index2:
    temp = cv2.KeyPoint(x=point[0][0],y=point[0][1],_size=point[1], _angle=point[2],
          _response=point[3], _octave=point[4], _class_id=point[5])
    kp1.append(temp)
```

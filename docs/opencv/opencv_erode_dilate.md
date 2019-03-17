---
title: "opencv erode & dilate"
categories: opencv
---


![image](https://user-images.githubusercontent.com/2216970/50380954-e22d2480-06b4-11e9-89f5-0fa653e94fff.png)

- cv2.erode()
- cv2.dilate()
- cv2.morphologyEx()

# 腐蚀
```
#coding=utf-8
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread('t.png', 0)
#img = cv2.cvtColor(oimg, cv2.COLOR_BGR2RGB)

m1 = plt.imshow(img)
m1.set_cmap('gray')
plt.show()

kernel = np.ones((5, 5), np.uint8)
erosion = cv2.erode(img, kernel)  # 腐蚀
fig = plt.figure()
m1 = plt.imshow(erosion)
m1.set_cmap('gray')
plt.show()

kernel = np.ones((10, 10), np.uint8)
erosion = cv2.erode(img, kernel)  # 腐蚀
fig = plt.figure()
m1 = plt.imshow(erosion)
m1.set_cmap('gray')
plt.show()
```
![image](https://user-images.githubusercontent.com/2216970/50381148-2ff85b80-06ba-11e9-84a7-9b2b13841edb.png)
![image](https://user-images.githubusercontent.com/2216970/50381149-31c21f00-06ba-11e9-93d0-5d01d9608603.png)
![image](https://user-images.githubusercontent.com/2216970/50381151-34247900-06ba-11e9-9692-474e2a4d4d6c.png)

```
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (10, 10))  # 矩形结构
erosion = cv2.erode(img, kernel)  # 腐蚀
fig = plt.figure()
m1 = plt.imshow(erosion)
m1.set_cmap('gray')
plt.show()

kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (10, 10))  # 椭圆结构
erosion = cv2.erode(img, kernel)  # 腐蚀
fig = plt.figure()
m1 = plt.imshow(erosion)
m1.set_cmap('gray')
plt.show()

kernel = cv2.getStructuringElement(cv2.MORPH_CROSS, (10, 10))  # 十字形结构
erosion = cv2.erode(img, kernel)  # 腐蚀
fig = plt.figure()
m1 = plt.imshow(erosion)
m1.set_cmap('gray')
plt.show()
```
![image](https://user-images.githubusercontent.com/2216970/50381158-4dc5c080-06ba-11e9-8ca7-4723ac372034.png)
![image](https://user-images.githubusercontent.com/2216970/50381159-4f8f8400-06ba-11e9-843c-1cc57c32d517.png)
![image](https://user-images.githubusercontent.com/2216970/50381160-51594780-06ba-11e9-995b-afb51561f168.png)



# 膨胀
```
kernel = np.ones((5, 5), np.uint8)
dilation = cv2.dilate(img, kernel)  # 膨胀
fig = plt.figure()
m1 = plt.imshow(dilation)
m1.set_cmap('gray')
plt.show()

kernel = np.ones((10, 10), np.uint8)
dilation = cv2.dilate(img, kernel)  # 膨胀
fig = plt.figure()
m1 = plt.imshow(dilation)
m1.set_cmap('gray')
plt.show()
```
![image](https://user-images.githubusercontent.com/2216970/50381161-5cac7300-06ba-11e9-91d6-ff597e71a2dd.png)
![image](https://user-images.githubusercontent.com/2216970/50381162-5f0ecd00-06ba-11e9-81bf-f7a520703b2d.png)


# 开运算
> 先腐蚀后膨胀叫开运算（因为先腐蚀会分开物体，这样容易记住），其作用是：分离物体，消除小区域。
闭运算则相反：先膨胀后腐蚀（先膨胀会使白色的部分扩张，以至于消除/"闭合"物体里面的小黑洞，所以叫闭运算）
![image](https://user-images.githubusercontent.com/2216970/50381209-f294cd80-06bb-11e9-9513-dde626d07125.png)
```
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))  # 定义结构元素

img = cv2.imread('t.png', 0)
plt.imshow(img, cmap='gray')
plt.show()

opening = cv2.morphologyEx(img, cv2.MORPH_OPEN, kernel)  # 开运算
fig = plt.figure()
plt.imshow(opening, cmap='gray')
plt.show()


closing = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel)  # 闭运算
fig = plt.figure()
plt.imshow(closing, cmap='gray')
plt.show()

```
![image](https://user-images.githubusercontent.com/2216970/50381222-89fa2080-06bc-11e9-8fc7-6c65dae993b5.png)
![image](https://user-images.githubusercontent.com/2216970/50381223-8bc3e400-06bc-11e9-8b8e-625065d4218a.png)
![image](https://user-images.githubusercontent.com/2216970/50381224-8f576b00-06bc-11e9-9d44-e0d99f53172f.png)

## 形态学梯度/顶帽/黑帽
```
img = cv2.imread('t.png', 0)
plt.imshow(img, cmap='gray')
plt.show()

gradient = cv2.morphologyEx(img, cv2.MORPH_GRADIENT, kernel)
plt.imshow(gradient, cmap='gray')
plt.show()

tophat = cv2.morphologyEx(img, cv2.MORPH_TOPHAT, kernel)
plt.imshow(tophat, cmap='gray')
plt.show()

blackhat = cv2.morphologyEx(img, cv2.MORPH_BLACKHAT, kernel)
plt.imshow(blackhat, cmap='gray')
plt.show()
```
![image](https://user-images.githubusercontent.com/2216970/50381396-f70fb500-06c0-11e9-86d1-02c7b1ad0292.png)
![image](https://user-images.githubusercontent.com/2216970/50381397-f840e200-06c0-11e9-8778-2119e09af8f2.png)
![image](https://user-images.githubusercontent.com/2216970/50381401-1870a100-06c1-11e9-878c-aff085e8af2f.png)
![image](https://user-images.githubusercontent.com/2216970/50381402-1a3a6480-06c1-11e9-9c23-7084ae6c9f5b.png)



## 打开图片

```python
# 打开图片
img = Image.open('2.jpg')

# 显示图片信息
print(img.format)
print(img.size)
print(img.height)
print(img.width)
print(img.getpixel((100, 100)))

# 显示图片
img.show()
```

## 创建图片

+ new(mode, size, color=0)

## 图片混合

+ 透明度混合
  + blend(img1, img2, alpha)
  + (img1x(1-alpha) + img2xalpha)
+ 遮罩混合

##  图像复制、剪切、粘贴、缩放

```python
from PIL import Image

img1 = Image.open('3.jpg')
img1.show()
print(img1.size)

# 图像缩放,只能缩放到大致的分辨率，不会完全一样
# img1.thumbnail((300, 500))
# print(img1.size)

# eval,对于每个像素点进行处理
# Image.eval(img1, lambda x: x*2).show()

# 图像剪切
box = (100, 100, 200, 200)
region = img1.crop(box)
# region.show()

# 图像粘贴
img1.paste(region, (0, 0))
img1.show()
```


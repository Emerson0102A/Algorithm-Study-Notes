```python
#制作灰度滤镜
#导入模块
from PIL import Image
#打开图片
image1 = Image.open("/Users/baizhi/beauty.jpg")
#转换图片格式
gray_image = image1.convert("L")
#保存图片
gray_image.save("/Users/baizhi/beauty_gray.jpg")
#展示图片
gray_image.show()
```

![img](https://cdn.penpencode.com/upload/5d47e6392f8474aa046eb8d5cb4ed6f1/633x617/Group%20374.png)

![img](https://cdn.penpencode.com/upload/a1844c42275a2f6dbc969c6811d8d3c1/386x375/Image%E5%87%BD%E6%95%B0.png)
title: PPT/PPTX转image图片
date: 2018-06-01 17:57:21
tags: POI
---

## PPT/PPTX转image图片
By KimmKing 2018年6月1日

### 功能需求与技术分析
最近有一个需求，在Java环境下把PPT/PPTX转换成图片展示。
一般来说，这个需求用dotnet来实现非常合适：
- 最简单的可以通过VSTO之类的，直接调用PowerPoint来实现转存图片。
- 也可以不依赖于dotnet，使用手法的Aspose组件，效果非常棒，就是不便宜。

这里提供一种跨平台的Java&开源处理方式：Apache POI实现PPT/PPTX的文件处理。
核心原理就是获取每一页的PPT对象，然后输出到内存图像对象，再保存为图片文件：
```
Slide.draw(graphics);
```

### Github开源项目
操作代码已经封装到这里：
[https://github.com/kkstudy/PPT2Image](https://github.com/kkstudy/PPT2Image)

PPT2Image 是一个把PPT 或 PPTX 的每一页转换成一个图片的库。 

### 使用说明

```
File file = new File("D:\\git\\PPT2Image\\1.pptx");
List<String> images = convertPPTtoImage(file,"D:\\git\\PPT2Image\\images\\pptx");
```

列表images里就是每一个图片的路径。

### 测试效果
1. POI对于PPTX格式的处理要比PPT好，特别是文本框和字体上更精确。
1. 转换速度PPTX要比PPT慢，PPT大概1s一张，PPTX大概需要1.6s。

### 效果对比
- PPTX to Images
![PPTX1](https://raw.githubusercontent.com/kkstudy/PPT2Image/master/images/pptx/1.jpg)

<!-- more -->

![PPTX2](https://raw.githubusercontent.com/kkstudy/PPT2Image/master/images/pptx/2.jpg)
![PPTX3](https://raw.githubusercontent.com/kkstudy/PPT2Image/master/images/pptx/3.jpg)
- PPT to Images
![PPT1](https://raw.githubusercontent.com/kkstudy/PPT2Image/master/images/ppt/1.jpg)
![PPT2](https://raw.githubusercontent.com/kkstudy/PPT2Image/master/images/ppt/2.jpg)
![PPT3](https://raw.githubusercontent.com/kkstudy/PPT2Image/master/images/ppt/3.jpg)

使用的测试文件在此：[https://github.com/kkstudy/PPT2Image](https://github.com/kkstudy/PPT2Image)
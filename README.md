## PaddleOCR arm64 docker镜像


## 公司试用了一款商用`ocr`，部署在`arm`平台上，我只是想那它来和`PaddleOcr`做个对比，但官方没有出相关教程（只有移动平台的），然后废了2天时间，主要参考[这篇文章](https://blog.csdn.net/qq_39056987/article/details/121078743?spm=1001.2014.3001.5501)，终于能成功运行了（没用交叉编译），遂顺手做个`docker`镜像，方便你我他~


# 快速使用
- 拉取镜像：`docker pull steinvenior/paddle_lite_ocr_linux_arm64:all`

- 设置别名，方便使用：`alias pdocr='docker run --rm  -i --user "$(id -u):$(id -g)" --workdir /data -v "$PWD:/data" steinvenior/paddle_lite_ocr_linux_arm64:all'`

- 例子：`pdocr ./ocr-test.jpg`,注意！！，后面的图片资源路径只能为当前路径下的相对路径，简单来讲就是：在待识别的图片相同目录下执行该命令

# 截图

![image](https://user-images.githubusercontent.com/18524326/149324039-f014e942-f2a9-42be-a348-ac8439fd10ce.png)

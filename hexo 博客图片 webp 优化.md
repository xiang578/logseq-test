---
tags:
  - hexo
  - blog
  - webp
  - qcloud
public: true
categories: 不老阁
toc: true
date:
  - 2024/06/23
permalink: post/hexo_photo_webp
title: hexo 博客图片 webp 优化
updated: 2024-10-05
mathjax: true
---

近期打算写一些游记，一看手机拍的照片大小都在 5Mb 以上，所以想着研究一下图片优化方法。主要了解了Imgbot 和 Webp 两种方法，最后选择通过腾讯云来优化图片。

<!--more-->

## Imgbot

  + 从这篇文章了解到 [使用 ImgBot 无损压缩博客中的图片 – Mogeko's Blog](https://mogeko.me/zh-cn/posts/zh-cn/066/)，大概用法是将 [Imgbot App](https://imgbot.net/) 添加到 Github 指定的库内，它会递归遍历所有的图片，然后再发起一个 pull request 用压缩后的图片替换原始图片。如下图所示：

![image.png](/assets/image_1719146689648_0.png)

  + 看起来挺方便的一个工具，不过可惜的是只有 public 库可以免费使用，最低付费价格 79 刀一个月。。。另外建了一个测试库，1 个小时过去也没给我压缩好。。。

## Webp

  + Webp 最早从木子博文 [让图片飞起来 oh-my-webp.sh ！ | Reimu's blog (k8s.li)](https://blog.k8s.li/oh-my-webpsh.html) 里了解，是一种为网页而生的图像格式。很香，但需要自己自建服务器进行一系列的操作。

  + 不过这次又找到一篇新的文章 [个人博客访问速度优化：CDN, 图片压缩, HTTP2 (selfboot.cn)](https://selfboot.cn/2024/01/03/hexo_blog_speed/#%E5%9B%BE%E7%89%87%E4%BC%98%E5%8C%96)，selfboot 通过腾讯云将图床上的文件处理成不同大小的 webp 图片，hexo 生成 html 时用新的图片链接替换原始图片链接，最后实现不同尺寸的设备能加载不同图片，更进一步优化图片访问体验。

  + ### 图片格式优化

    + 一直以来使用腾讯云的图床托管图片，链接类似于 `https://blog.xiang578.com/assets/image_1718352560106_0.png`。腾讯云提供在图片链接添加不同后缀返回不同方式处理后的图片的功能，比如 `https://blog.xiang578.com/assets/image_1718352560106_0.png/webp` 会返回根据用户定义 webp 规则处理的图片。

    + 从 [数据万象CI购买_数据万象CI选购 - 腾讯云 (tencent.com)](https://buy.cloud.tencent.com/ci) 看，基础图片处理价格起步是25 元 1 年 1 TB ，也不是很贵。

  + ### 图片处理

    + 用户规则在桶的 `规则管理 - 数据处理 - 图片处理 - 图片处理样式里指定`

![image.png](/assets/image_1719147728947_0.png)

    + selfboot 定义了 4 种规则（原始/1600/800/400 等不同大小的 web，直接 copy 人家的方案。

```
styleName: webp, styleBody: imageMogr2/format/webp/interlace/1
styleName: webp1600, styleBody: imageMogr2/thumbnail/1600x>/format/webp/interlace/0
styleName: webp400, styleBody: imageMogr2/thumbnail/400x>/format/webp/interlace/0
styleName: webp800, styleBody: imageMogr2/thumbnail/800x>/format/webp/interlace/0

```

  + ### 压缩效果

    + 随便找了一张图片，用规则 `imageMogr2/format/webp/interlace/1` 直接把图片从 2.63 mb 压缩到 161 kb。。。

![image.png](/assets/image_1719147936870_0.png)

  + ### 自适应图片

    + 完成压缩配置后，不可能手动将原来的所有图片链接都添加上相关的后缀。所以 selfboot 提供一个脚本，实现 hexo 渲染 html 时替换图片链接以及增加 scrset、sizes 等属性。

    + 在 hexo 项目根目录创建文件 `scripts/img.js`，具体代码如下。不过要注意一点，`const imgPath = path.join(__dirname, "../images", imgPathPart)` 中的 `"../images"` 需要改成你的图片文件地址。比如我的图片放在根目录下的 `source/assets` 就改成`"../source/assets"`。

```javascript
const cheerio = require("cheerio");
const path = require("path");
const imageSize = require("image-size");
const url = require("url");
const fs = require("fs");
hexo.extend.filter.register("after_render:html", function (str, data) {
    const $ = cheerio.load(str);
    $("img").each(function () {
        const img = $(this);
        const src = img.attr("src");
        if (
            src &&
            (src.endsWith(".png") ||
                src.endsWith(".jpeg") ||
                src.endsWith(".jpg") ||
                src.endsWith(".gif") ||
                src.endsWith(".webp"))
        ) {
            const parsedUrl = url.parse(src);
            const imgPathPart = parsedUrl.path;
            const imgPath = path.join(__dirname, "../source/assets", imgPathPart);
            // 检查文件是否存在
            if (fs.existsSync(imgPath)) {
                const dimensions = imageSize(imgPath);
                const width = dimensions.width;
                const small = src + "/webp400";
                const middle = src + "/webp800";
                const large = src + "/webp1600";
                const origin = src + "/webp";
                let srcset = `${origin} ${width}w`;
                if (width > 400) srcset += `, ${small} 400w`;
                if (width > 800) srcset += `, ${middle} 800w`;
                if (width > 1600) srcset += `, ${large} 1600w`;
                img.attr("srcset", srcset);
                let sizes;
                if (width <= 400) {
                    sizes = `${width}px`;
                } else {
                    sizes = "(min-width: 1150px) 723px, (min-width: 48em) calc((100vw - 120px) * 3 / 4 - 50px), (min-width: 35.5em) calc((100vw - 75px), calc(100vw - 40px)"
                }
                img.attr("sizes", sizes);
                img.attr("src", origin);
                const height = dimensions.height;
                img.attr("width", width);
                img.attr("height", height);
            }
        }
    });
    return $.html();
});
```

  + ### 效果测试

    + selfboot 提到一个工具 [RespImageLint (ausi.github.io)](https://ausi.github.io/respimagelint/)，不过不知道自己为什么一直使用不成功。

![image.png](/assets/image_1719143918263_0.png)

    + 另外一个方法就是通过开发者工具，查看请求的图片是否符合预期。

![image.png](/assets/image_1719149013375_0.png)

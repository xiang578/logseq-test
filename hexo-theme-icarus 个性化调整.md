---
tags:
- hexo
- hexo-theme-icarus
public: true
categories: 不老阁
title: hexo-theme-icarus 个性化调整
date: 2024-10-05
lastMod: 2024-10-05
toc: "true"
---

主题链接：[ppoffice/hexo-theme-icarus: A simple, delicate, and modern theme for the static site generator Hexo. (github.com)](https://github.com/ppoffice/hexo-theme-icarus)
## 文章预览

主页文章预览的默认效果是左侧显示一个「阅读更多」按钮，修改成左侧显示文章的标签+右侧显示「阅读更多」按钮。
![最终效果](https://media.xiang578.com/202303251246107-icarus-index-preview.png)
修改 `layout/common/article.jsx` 文件中的 `{/* Tags */}` 和 `{/* "Read more" button */}` 两部分代码
```jsx
{/* Tags */}
<hr style="height:1px;margin:1rem 0"/>
<div className="level is-mobile is-flex">
  {page.tags && page.tags.length ? <div class="article-tags is-size-7 is-uppercase">
    <i class="fas fa-tags has-text-grey"></i>&nbsp;
    {page.tags.map((tag, index) => {
      return <a class="link-muted" rel="tag" href={url_for(tag.path)}>{tag.name}{index !== page.tags.length-1? ', ':''}</a>;
    })}
  </div> : null}
  {/* "Read more" button */}
  {index && page.excerpt ? <a class="article-more button is-small is-size-7" href={`${url_for(page.link || page.path)}#more`}><i class="fas fa-book-reader has-text-grey"></i>&nbsp;&nbsp;{__('article.more')}</a> : null}
</div>
```
## 文章页面双栏显示
站点目录创建文件 `_config.post.yml`
## TOC
该主题文章需要在 Front-Matter 中声明 `toc: true` 才展示目录。参考 [记第三次博客切换主题以及主题优化 - 编程技术笔记 (yxchangingself.xyz)](*https://yxchangingself.xyz/posts/hexo_blog_switch_theme_3/*) 通过正则表达式批量为历史文章增加 `toc: true` 属性。打开 VS Code，查找内容设置为 `---\ntitle(.*)` 替换内容设置为 `---\ntitle$1\ntoc: true`，点批量替换。
## 修改默认字体
最近有挺多人推荐这款字体 [lxgw/LxgwWenKai: An open-source Chinese font derived from Fontworks' Klee One. 一款开源中文字体，基于 FONTWORKS 出品字体 Klee One 衍生。](https://github.com/lxgw/LxgwWenKai) 根据项目主页的介绍，个人博客比较适合使用 [霞鹜文楷屏幕阅读版 / LXGW WenKai Screen](https://github.com/lxgw/LxgwWenKai-Screen) 。从 [【如需网页上嵌入，请看这里】webfont npm 包 · Issue #24](https://github.com/lxgw/LxgwWenKai/issues/24) 中找到其他人提供的 webfont 地址 `https://cdn.staticfile.org/lxgw-wenkai-screen-webfont/1.6.0/lxgwwenkaiscreen.css`。
借助 [hexo 注入器](https://hexo.io/zh-cn/api/injector.html) 将 webfont 地址写到生成 html 页面的  `<head>` 标签中。在 `icarus/scripts/injector.js` 文件中添加一行：
`hexo.extend.injects.register('head_begin', '<link rel="stylesheet" href="https://cdn.staticfile.org/lxgw-wenkai-screen-webfont/1.6.0/lxgwwenkaiscreen.css">', 'default');`
icarus 主题的默认字体是在 `icarus/include/style/base.styl` 中声明，相应增加上 `LXGW WenKai Screen` 即刻。具体修改如下：
`$family-sans-serif ?=  "LXGW WenKai Screen", Ubuntu, Roboto, 'Open Sans', 'Microsoft YaHei', sans-serif`
## Umami 统计
主题自带 GA 和百度统计，但是这两种方式都不方便分享统计结果。所以个人还是更加喜欢 Umami 统计，目前 Umami Cloud 可以免费试用，可以省去自己部署的麻烦。本博客的访问数据在 [Blog Analytics](https://analytics.umami.is/share/6fJ2QrDdHeYWEHvd/Blog)。
借助 [hexo 注入器](https://hexo.io/zh-cn/api/injector.html) 将 Umami 的统计代码写到生成 html 页面的  `<head>` 标签中。在 `icarus/scripts/injector.js` 文件中添加一行：`hexo.extend.injector.register('head_begin', '<script async defer data-website-id="your-umami-id" src="https://analytics.umami.is/script.js"></script>', 'default');`
## 备案号
主题默认不支持，网上可以找到下面三种实现方式
[Hexo博客Icarus主题添加备案号 - legendsmb](https://www.legendsmb.com/2020/05/13/Hexo%E5%8D%9A%E5%AE%A2Icarus%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E5%A4%87%E6%A1%88%E5%8F%B7/)：修改 footer.jsx
[希望提供备案配置功能 · Issue #792 · ppoffice/hexo-theme-icarus (github.com)](https://github.com/ppoffice/hexo-theme-icarus/issues/792#issuecomment-1225913348)：新增相关脚本，然后配置
[hexo-icarus-主题安装使用中遇到的问题以及解决方案---龙爪槐守望者-(ftium4.com)](https://www.ftium4.com/hexo-icarus-config-fix.html#%e5%9c%a8-footer-%e6%98%be%e7%a4%ba%e5%a4%87%e6%a1%88%e5%8f%b7)：利用-links-功能
看起来第三种实现难度最低，打开 `_config_icarus.yml` 找到 `footer` 修改成：
id:: 641e922e-046d-46f9-9b1e-dd75610c9b04
```yml
footer:
    # Links to be shown on the right of the footer section
    links:
        浙ICP备17004638号-1: https://beian.miit.gov.cn/#/Integrated/index
```
## 评论系统
参考 [Icarus用户指南 - 用户评论插件 - Icarus (ppoffice.github.io)](https://ppoffice.github.io/hexo-theme-icarus/Plugins/Comment/icarus%E7%94%A8%E6%88%B7%E6%8C%87%E5%8D%97-%E7%94%A8%E6%88%B7%E8%AF%84%E8%AE%BA%E6%8F%92%E4%BB%B6/#Waline) 选择 Waline
[开通微信通知](https://waline.js.org/guide/features/notification.html#%E5%BE%AE%E4%BF%A1%E9%80%9A%E7%9F%A5)
[使用 Gmail 发送邮件通知](https://blog.wingszeng.top/waline-sent-gmail/)
### 增加最新评论 Widget
TODO 等博客有 10 条评论再说……
参考 [你好，麻烦问下有没有计划在右侧的Widgets一栏加一个最近评论的项呢？类似于http://kevin.doyeden.com/ 这个主题这种的 谢谢啦 · Issue #157 · ppoffice/hexo-theme-icarus (github.com)](https://github.com/ppoffice/hexo-theme-icarus/issues/157)
[maupassant-hexo/recent_comments.pug at master · tufu9441/maupassant-hexo · GitHub](https://github.com/tufu9441/maupassant-hexo/blob/master/layout/_widget/recent_comments.pug)
## 相关文章/推荐文章
参考 [hexo icarus主题添加相关文章 - Zhh Blog (huihongcloud.com)](https://www.huihongcloud.com/2021/10/02/hexo/hexo%20icarus%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E7%9B%B8%E5%85%B3%E6%96%87%E7%AB%A0/)
通过插件 `hexo-related-popular-posts` 生成相关文章或者热门文章数据
创建 `layout/common/related.jsx` 文件
```jsx
const logger = require('hexo-log')();
const { Component } = require('inferno');
const view = require('hexo-component-inferno/lib/core/view');


module.exports = class extends Component {
    render() {
        const { config, helper, page } = this.props;
        const { __, popular_posts } = helper;
        let relatedText = popular_posts( {} , page )
        if (!relatedText || relatedText.length == 0) {
            return null;
        }
        return <div class="card">
            <div class="card-content">
                <h2>相关文章</h2>
                <span
            dangerouslySetInnerHTML={{__html:(relatedText) }}>
            </span>
            </div>
        </div>;
    }
};
```
在 `article.jsx` 中添加一行 `const Related = require('./related');` 导入上一步新增的 related 模块，然后再把 related 模块添加到 Donate 之后。
```jsx
            {/* Donate button */}
            {/* {!index ? <Donates config={config} helper={helper} /> : null} */}
            {/* Related Post*/}
            {!index ? <Related config={config} page={page} helper={helper}/> :null}
            {/* Post navigation */}
```
## CDN 优化
默认 FontAwesome CDN 在国内访问实在是太慢，参考 [优化博客 - XiaoYe's Blog (starx.win)](https://blog.starx.win/optimize-blog/) 改成 [字节跳动静态资源公共库 (bytedance.com)](https://cdn.bytedance.com/)。
`iconcdn` 改成 `https://lf6-cdn-tos.bytecdntp.com/cdn/expire-1-M/font-awesome/6.0.0/css/all.min.css`
## 提交搜索引擎
[cjh0613/hexo-submit-urls-to-search-engine: Hexo plugin to submit URLs of new posts to Google, Bing, Baidu search engine , that make search engines index your pages earlier. Hexo插件：主动推送Hexo博客新链接至谷歌必应百度搜索引擎，提升网站收录质量和速度。 (github.com)](https://github.com/cjh0613/hexo-submit-urls-to-search-engine)
## 参考
[引入自定义 JS / CSS 的功能 · Issue #1009 · ppoffice/hexo-theme-icarus (github.com)](https://github.com/ppoffice/hexo-theme-icarus/issues/1009)
[博客源码分享 - 辣椒の酱 (removeif.github.io)](https://removeif.github.io/theme/%E5%8D%9A%E5%AE%A2%E6%BA%90%E7%A0%81%E5%88%86%E4%BA%AB.html)：gitalk 和 valine 最新评论widget、博客样式修改、推荐文章模块、影音数据文件、推荐文章模块
[个人博客优化记录 - Challenging-eXtraordinary (chuxin911.com)](https://www.chuxin911.com/blog_update_record_20210721/)
键位效果 `hexo-tag-kbd` 例子 `{% kbd Ctrl %} + {% kbd ALT %} + {% kbd DELETE %}`
[Hexo-Icarus主题配置建议 - Andy' s Blog (andycen.com)](https://blog.andycen.com/2020/03/07/Hexo-Icarus%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E5%BB%BA%E8%AE%AE/) 目录粘性布局、文章预览效果优化
[创造 CANDY 主题，只为更好的交互 - 安子璠的个人主页 (anzifan-old.vercel.app)](https://anzifan-old.vercel.app/post/icarus_to_candy_1)  导航栏优化、TOC 优化
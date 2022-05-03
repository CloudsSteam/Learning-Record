

### 个人博客初建

于 20 年 11 月 24 日搭成的 Trojan 协议跑在阿里云香港服务器，用了一年其效果 YouTube 奈飞 4k 秒加载。闲来无事想探索新技术把它重置搭建 x-ui 管理面板和宝塔面板部署 WordPress 博客共存。使用两天感觉网速变得很慢，WordPress 还老是访问不了，香港服务器配置不高带不动二者。无奈只能加钱换服务器，正值黑色星期五活动期间，搬瓦工日本软银 GIA 线路年付 81 刀。相比阿里云 30M 的带宽搬瓦工 1GB 看上去真的很诱人，可月底捉襟见肘还是没有考虑。于是改变方案继续用阿里云香港服务器搭建 Trojan（日常使用足够），博客得用国内服务器考虑访问速度(但我现在又在纠结要不要 cloudflare 套 cdn)。没想到月底了阿里云还有双十一新人福利，189 元 3 年 2 核 4Gcpu80G 存储，配置价格很不错了赶快让女友注册了个新账户薅了一把羊毛。不过后续续费价格太感人了:cold_sweat:，不行到时候再迁移服务器吧。

#### 博客部署

先前的 WordPress 使用体验不佳，其操作适合新手建站。考虑到访问速度上和学习上的需要，从 WordPress 迁到了 HEXO。服务器也从香港迁回了大陆。域名也备了案。至少访问速度是得到了质的提升。至于转成 [HEXO](https://github.com/hexojs/hexo)，通过 Md 文件高速渲染静态页面其次就是基于 nodejs*想着静态存储也方便后期迁移服务器*,又一次有了折腾的冲动。然没有那么直观的后台管理了,但是命令行界面用起来也是爽爽自己也从最初的惧怕命令行到现在些许成就感还算熟练。其配置主题选用的是 [hexo-theme-melody](https://github.com/Molunerfinn/hexo-theme-melody),由于有着薄弱的前端知识对其其主题的效果不能满足自己的就自己开始琢磨改配置文件，随着时间的摸索也是让我一步一步达成我想要的效果，这个转变大概自己也觉得惊讶。后期有空也将逐步复习的时候把之前记录的笔记整理分类上传![](https://cdn.jsdelivr.net/gh/licensor0/PicGo//img/202112081435435.png)

#### 配置文件修改

先是在自己电脑上 npm 安装 hexo， 命令创建生成启动初始文件发布打包再通过 git 配置部署到服务器，nginx 配置域名能照常访问，再根据自我情况修改配置文件

> 主要修改如下

1. git 配置
2. Acme 脚本 zerossl 自动申请 ssl 证书
3. nginx 配置
4. 创建导航栏
5. 搜索

   - Algolia-search
   - generator-search.

6. PicGo 图床建立
7. top_img 选用高度
8. 代码颜色换行
9. 鼠标特效
10. 背景彩带
11. font icons

    - rss 订阅

12. 自动节选
13. 文章版权
14. Gitalk 评论
15. Sharejs 分享
16. wordcount 字数统计
17. 文章广告区(后期整点音乐播放)
18. PWA 适配
19. 页脚配置
    - 不蒜子访客计算
    - ICP 备案
    - hitokoto
    - live2d 看板娘

#### 主要遇到问题

- git 部署
- 搜索本是采用 Algolia-search 的，可发现咋配置都只能通过标题检索不能检索文章内容，故换成 hexo-generator-search 能检索内容却不显示样式[后期补上](https://www.barretlee.com/blog/2017/06/04/hexo-search-insite/)。还是存在问题后期文章多存在检索工程量巨大(静态博客没有数据库缺点)有了索引文件、搜索算法和搜索框。[改进](https://liam.page/2017/09/21/local-search-engine-in-Hexo-site/)激活搜索框时才调用，屏蔽回车，加载和解析索引文件给用户提示
- PicGo 图床建立选用的是 Githu&jsDelivr 搭建 CDN 加速免费图床，再加上 Typora 编写 md 文档一键上传。按要求配置好，可第二天重启 picgo 配置消失了?不知后期会不会存在问题
- 鼠标特效 meodyly 主题的鼠标点击效果，不是很喜欢单一了。改用鼠标点击蓄力释放各种颜色小球，随鼠标蓄力抬起时间决定改变参与动画的数量和距离(pc 端才有)，闲来解压很不错
- font icons 用的是 [font-awesome v5 free icons](https://fontawesome.com/v5.15/icons?d=gallery&m=free)其中 rss 配置琢磨了会儿
- Gitalk 评论 未找到相关的 Issues 进行评论 请联系其博主初始化创建，因为当时是跑在本地 4000 端口上，没有部署到服务器。后续部署上问题解决
- 经过几天运行感觉时常不蒜子不能正常返回访客和观看次数，超时每次最慢加载从而影响访问体验
- 本来是部署在香港服务器是不需要备案的，换回来了按要求提交手续 4 天才审核完成颁发 icp 备案号。
  然后就是根据配置修改 icp 和 hitokoto 共存了
- live2d 看板娘看了好久暂时还没有配置，怕影响加载速度。笑死，考虑加载速度还要 cloudflare 套 cdn 隐藏真实 ip

##### 至始至终个人寒酸博客也算建起来了

好了，就先写这么多吧。后续待我复习笔记慢慢更新博客了
感谢每一位观众能看到现在，期待下次与你们相见
一张白纸重新书写。
![](https://cdn.jsdelivr.net/gh/licensor0/PicGo//img/202112081707007.png)
![](https://cdn.jsdelivr.net/gh/licensor0/PicGo/img/202112050943345.jpg)
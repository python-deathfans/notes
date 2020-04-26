## 配置

+ 在_config.yml中修改大部分的配置



## 网站

| 参数        | 描述                                    |
| ----------- | --------------------------------------- |
| title       | 网站标题                                |
| subtitle    | 网站副标题                              |
| description | 网站描述，主要用于告诉SEO，告诉搜索引擎 |
| keywords    | 网站关键词。                            |
| author      | 作者                                    |
| language    | 网站使用语言。zh-CN 简体中文            |
| timezone    | 市区，默认使用电脑的时区                |



## 网址

| 参数               | 描述                                         |
| ------------------ | -------------------------------------------- |
| url                | 网址                                         |
| root               | 网站根目录                                   |
| permalink          | 文章的永久链接格式 :year/:month/:day/:title/ |
| permalink_defaults | 永久链接中各部分的默认值                     |
| pretty_urls        | 改写permalink的值来美化URL                   |



## init

+ hexo init[folder]
  + 新建一个网站。如果没有设置folder,默认在目前的文件夹建立网站



## new

+ hexo new [layout] <title>
  + 新建一篇文章，如果没有设置layout,默认使用的是post。
  + 如果标题包含空格，请使用引号括起来

+ | 参数          | 描述                                       |
  | ------------- | ------------------------------------------ |
  | -p, --path    | 自定义新文章的路径                         |
  | -r, --replace | 如果存在同名文章，将其替换                 |
  | -s, --slug    | 文章的slug,作为新文章的文件名和发布后的URL |

+ 默认情况，使用文章的标题来决定文章的路径。
+ 对于独立页面，Hexo会创建一个以标题为名字的目录，并在目录下放置一个index.md文件。



## generate

+ 生成静态文件

+ | 选项 | 描述                   |
  | ---- | ---------------------- |
  | -d   | 文件生成后立即部署网站 |
  | -w   | 监事文件变动           |
  | -s   | 启动本地渲染           |
  | -cl  | 清除公共文件夹和缓存   |



## publish

+ hexo publish [layout] <filename>
  + 发表草稿



## list

+ hexo list <type>
  + 列出网站资料



## version

+ hexo version
  + 显示hexo版本



## 写作

+ hexo new [layout] <title>
  + post
    + 默认，一篇文章
    + source/_posts
  + page
    + 独立页面
    + source
  + draft
    + 草稿
    + source/_drafts

+ 草稿
  + 可以使用publish命令将草稿移动到source/_posts文件夹，该命令的使用方式和new十分相似，您也可以在命令中指定layout来指定布局。
  + hexo publish [layout] <title>
  + 默认不会显示在页面中，您可以在执行时加上 --draft参数，或是把render_drafts参数设置为true来预览草稿



## Front-matter

+ 是文件最上方以---分割的区域，用于指定个别文件的变量，举例来说：

  + ```
    ---
    title: Hello World
    date: 2013/7/13 20:46:25
    ---
    ```

+ 下面是预先定义的参数，可以在模板中使用这些参数值并加以利用。

+ | 参数       | 描述                 | 默认值       |
  | ---------- | -------------------- | ------------ |
  | layout     | 布局                 |              |
  | title      | 标题                 | 文章的文件名 |
  | date       | 建立日期             | 文件建立日期 |
  | updated    | 更新日期             | 文件更新日期 |
  | comments   | 开启文章的评论功能   | true         |
  | tags       | 标签（不适用于分页） |              |
  | categories | 分类（不适用于分页） |              |
  | permalink  | 覆盖文章网址         |              |
  | keywords   | 不推荐使用           |              |

+ 分类和标签

  + ```
    categories:
    - Diary
    tags:
    - PS3
    - Games
    ```

    


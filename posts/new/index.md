# 迭代


## 1. 2021-05-21 增加评论功能

难点在于找到的一个discus组件，居然被墙了。原理很简单，就是将评论的内容，挂给第三方，直接读写在第三方论坛里面就可以。联想一下，查看墙内的用法。结果发现一个 valine 比较好用。

参照[Hugo中加入Valine评论功能](http://inner-peace.cn/blog/hugo_valine/)进行处理，但是给的模版范例不太一样。为了快速上线评论功能，于是把模版又更新了一把。现在有了评论功能了。开心～

需要在 [leancloud](https://console.leancloud.cn/apps/S6pdpHK4l4LPLloXeQeoibI7-gzGzoHsz/settings/keys) 上注册账号，我用的免费版，不知道以后会不会收费，会不会挂掉。

## 2. 2021-05-22 增加站内检索功能

站检索能力和评论一样，独立于博客之外，查阅资料后发现，algolia 就是我想要的。选择站点是HK，同样一个月10w次查询以下免费。

[algolia教程](https://edward852.github.io/post/hugo%E6%B7%BB%E5%8A%A0algolia%E6%90%9C%E7%B4%A2%E6%94%AF%E6%8C%81/) 按照这个操作，并在配置中进行更新追加。

实操过程是编辑blog，提交blog之前。重新构造一个索引，并提交到algolia的项目。

```
1. 创建并编辑algolia配置文件，注意生成索引的目录条件。后面还可以扩展
# mkdir layout/_default 
# touch layout/_default/list.algolia.json

{{/* 生成Algolia搜索索引文件 */}}
{{- $.Scratch.Add "index" slice -}}
{{/* content/posts或content/post目录下的博文才生成索引 */}}
{{- range where (where .Site.Pages "Type" "in" (slice "posts" "post" "life" "tech")) "IsPage" true -}}
  {{- if and (not .Draft) (not .Params.private) -}}
    {{- $.Scratch.Add "index" (dict "objectID" .File.UniqueID "url" .Permalink "content" (.Summary | plainify) "tags" .Params.Tags "lvl0" .Title "lvl1" .Params.Categories "lvl2" "摘要") -}}
  {{- end -}}
{{- end -}}
{{- $.Scratch.Get "index" | jsonify -}}
2. 增加配置信息
# 编辑完成后，config.atoml 中增加 algolia配置, 具体配置信息在 algolia 登陆后查询获取
[languages.zh-cn.params.search.algolia]
  index = "myBlog"
  appID = "********"
  searchKey = "**********"
3. 生成索引，并自动上传索引文件
# npm init //如果没有npm 则 brew install npm
# npm install atomic-algolia --save //这个命令会生成一个 json文件
# vim package.json
{
  "name": "mysite",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1", //这里多一个逗号
    "algolia": "atomic-algolia" //添加这一行
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "atomic-algolia": "^0.3.19"
  }
}
# 在hugo 工程的 跟目录 编辑 .env文件 如果没有则新创一个。 注意是admin_key
ALGOLIA_APP_ID=********
ALGOLIA_INDEX_NAME=myBlog
ALGOLIA_INDEX_FILE=public/algolia.json
ALGOLIA_ADMIN_KEY=********


```





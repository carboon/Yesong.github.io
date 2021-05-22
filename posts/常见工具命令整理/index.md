# 

### 背景

工作学习常见工具的使用，将案例和场景进行汇总，后续都丢到这里来。初步包括shell 命令，git命令，ide的使用等等

#### hugo

[官方文档](https://www.gohugo.org/ ) 在此。基本上照搬

1. 安装

   ```
   $ brew install hugo
   ```

2. 生成站点， 用一次后面就基本上不会再用第二次，而且还需要额外配置。

   ```
   $ hugo new site /path/to/site
   ```

3. 创建一个 新的 文档 about，主要是附带了时间戳，注意修改完毕后，把draft改为 false

   ```
   $ hugo new about.md
   ```

4. 本地运行hugo进行调试确认.后面默认，如果在config文件中配置完毕，不需要加

   ```
   $ hugo server --theme=hyde --buildDrafts
   ```

5. 最终部署。如果在config文件中配置完毕，不需要加配置

   ```
   $ hugo --theme=hyde --baseUrl="http://coderzh.github.io/"
   ```

   执行完毕后，会生成public中的静态文件，这些文件提交到github上即可进行展示。

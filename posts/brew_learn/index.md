# Brew_learn


## 记录下brew使用问题

### 安装失败

在安装flink的时候，用 brew install apache-flink 命令 报错。报错的信息如下，一开始认为是包的问题。后来发现哪怕是安装 wget 也会出问题。

![image-20210603113010210](https://github-1305981322.cos.ap-guangzhou.myqcloud.com/img/image-20210603113010210.png)

后来，推断是brew 安装出了问题。

- cd /usr/local/Homebrew/Library/Taps 删除 **homebrew**目录，再mkdir。
-  参照 这个 文章进行处理 https://zhuanlan.zhihu.com/p/90508170 ，重新安装。
- 主要是执行第二步：重新安装，第三步，设置镜像，第四步和第五步，设置bottles镜像。
- brew update

再次验证一下：brew install wget。问题解决。



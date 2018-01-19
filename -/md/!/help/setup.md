# 八卦博客 · 开始使用
## 如何安装

### MAC 系统

我们以github page为例（同样支持bitbucket page、gitee page）

1.  [点击这里](https://github.com/organizations/new)，在github上新建组织，比如 8gua-test
    
2.  在组织下面创建项目，项目名为『组织名称.github.io』( 比如 [8gua-test.github.io](http://8gua-test.github.io) )
    
3.  git clone 代码到本机，请通过ssh的方式克隆，以确保git push不需要输入密码
    
4.  进入代码目录，执行安装脚本  
    cd [8gua-test.github.io](http://8gua-test.github.io)  
    curl -Ls [https://git.io/vNRzu](https://git.io/vNRzu) | bash /dev/stdin
    
5.  部署代码
    
    ```
    git add . 
    git commit -m"init"
    git push -f 
    ```
6.  访问网站

命令用法

运行

```
8gua -h 
```

可以查看帮助，如果需要查看某个命令的参数的帮助，比如get命令，可以运行

```
8gua -h get 
```

### Linux

先用系统的包管理安装node和git 。

系统包中node版本有时候太老，我们运行以下命令更新。

```
npm install -g n
n stable 
```

接下来安装8gua

```
npm install -g 8gua 
```

最后，同样，进入github page仓库的目录，运行8gua

## 小技巧

如果你不小心在其他目录运行了8gua，多了一堆模板文件，可以运行以下的命令来清理。

```
git clean -f -d 
```

## 部署到私有服务器

静态博客，自然可以随处部署。

nginx配置文件[参考这里](https://gitee.com/u8gua/tool/blob/master/nginx.8gua.conf) ，其中用到的https免费证书，可使用 [acme.sh](https://github.com/Neilpang/acme.sh/wiki/%E8%AF%B4%E6%98%8E) 来自动生成。

caddy配置文件[参考这里](https://gitee.com/u8gua/tool/blob/master/Caddyfile)。

### 持续集成

持续集成，就是当后台自动push修改后，私有服务器上自动更新网页。

可以使用[Travis CI](https://travis-ci.org/)配合github来实现此需求。

1.  访问 [travis-ci.com](https://travis-ci.com/) ，打开项目构建开关
    
2.  在本机安装travis (先确保ruby已经安装，gem命令可用)。  
    sudo gem install travis
    
3.  运行 travis login ， 输入github的用户名密码。
    
4.  在仓库根目录新建 .travis.yml ，并git add
    
5.  用travis加密添加登录是有服务器的私钥到仓库
    
    `travis encrypt-file ~/.ssh/id_rsa --add`
    
    `git add id_rsa.enc`
    
    然后，请把 .travis.yml 中 openssl 这一行的 ~\\/.ssh 改为 ~/.ssh
    
6.  在私有服务器上git clone代码仓库到目录
    
7.  参考[此配置文件](https://gitee.com/u8gua/tool/blob/master/.travis.yml)，修改你的.travis.yml
    
8.  push仓库，即可实现自动触发更新
    

#### 拓展阅读

*   [持续集成服务 Travis CI 教程](http://www.ruanyifeng.com/blog/2017/12/travis_ci_tutorial.html)
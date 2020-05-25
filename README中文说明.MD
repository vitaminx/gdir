## 简易谷歌团队盘目录构建——gdir

### 安装步骤
    这里以安装在VPS上为例
    + 准备工作
    + 依赖环境安装
    + 安装及配置gdir
    + 调整设置

#### 准备工作

+ GitHub 账号和密码（没有请注册并前往邮箱激活）
+ Cloudflare 账号和密码（没有请注册并激活、创建workers）
+ Google 账户sa文件（Json文件，最好200个以上）
+ VPS准备

#### 依赖环境安装

    为了方便网友安装使用，作者写了一件安装脚本，方便快捷！必须点赞！但有时候一键脚本容易出问题，需要手动安装，本教程先提供一件安装脚本，再讲手动安装，一下是作者的一键安装脚本：
    
    eval "$(curl -Lso- https://gist.githubusercontent.com/rixtox/05d5ecd0b067f055cddda436efc9035f/raw/gdir-env-setup.sh)"
    
    以下为手动安装：
    
##### CentOS系统

+ 安装Git：yum install -y git
+ 安装Golang toolchain（GO）：
    + 先安装epel源：
        +  yum install -y epel-release
        +  yum clean all && yum makecache    
    + 安装Golang：
        + yum install -y golang

##### Debian系统安装

+ 安装Git：apt install -y git
+ 安装Golang toolchain（GO）：
    + 先安装epel源：
        +  apt install -y epel-release
        +  apt clean all && apt makecache    
    + 安装Golang：
        + apt install -y golang

#### GitHub和Cloudflare账号密码及授权文件

+ 注册GitHub账号，记录下账号和密码备用
+ 在GitHub里新建“Personal access token”：
    + 打开网址：https://github.com/settings/tokens
    + 点击右上角“Generate new token”,随意填写“Note”（最好能通过note知道这个token是干什么用的），下边权限只勾选“gist”一项，点击下方绿色的“Generate token”，保存好生产的Token代码（一串字符），以备后用
+ 注册Cloudflare账号，并登录查看“Global API Key”：
    + 打开网址：https://dash.cloudflare.com/profile/api-tokens
    + 点击下方的“Global API Key”右边的查看（View）,输入密码后即可看到一串字符，复制保存下来！    

把以上得到的“GitHub账号密码”“Personal access token”“Cloudflare账号”“Global API Key”准备好！

#### 安装及配置gdir

##### 安装gdir
+ 开启全局代理，登录VPS
+ 克隆gdir项目仓库并进入gdir目录
    + git clone https://github.com/workerindex/gdir.git && cd gdir
+ 上传sa到VPS用户目录下任意一文件夹（通常用“sa”或者“accounts”文件夹）

#### 配置gdir
+ 输入命令：go run ./tools/setup
+ 依次输入：
    + Global API key
    + “1”回车
    + “0”回车
    + Personal access token
    + 从这里开始以下6步均可直接“回车”选着默认值
    + 输入sa地址（如：/root/sa/）回车
    + 输入管理员账户名
    + 输入管理员密码（注意在linux下输入密码是没有任何提示的）回车执行下一步
    + 回车选择默认值
    + 输入GitHub账户名
    + 输入GitHub账户密码
    + 回车选择默认值
    + 输入GitHub账户名
    + 输入GitHub账户密码
    + 回车选着默认值
    + 输入GitHub账户名
    + 输入GitHub账户密码

##### 注意：
+ 此处需要输入“Cloudflare”账户1次，“Global API key”和“Personal access token”各一次，GitHub账户名密码各三次！
+ 至此配置完成可以使用，你可以在网址输入你配置的“Cloudflare”下的Worker项目网址（一般格式为：xxx.xxxx..workers.dev）

### 设置gdir
    设置的命令为： go run ./tools/adduser
    
#### 指定显示哪些盘/文件夹

+ 输入命令：go run ./tools/adduser
+ 按提示输入：用户名（可以是已有或者么有的，已有就是设置修改、新用户名就是设置增加新用户）
+ 输入密码
+ “y”确认以上输入信息后会显示该用户可以查看的全部团队盘
+ 选择“Convert to white-list access control list”转换为“白名单”，只能查看指定的盘
+ 输入想显示的团队盘id，多个的话用英文逗号分开，回车显示该用户所能查看的团队盘并显示选择菜单
+ 回车选择默认“确认”
+ 输入GitHub的用户名和密码更新 Gist

#### 修改添加用户

+ 输入命令：go run ./tools/adduser
+ 输入新用户名
+ 输入新用户密码
+ 把上面“指定显示哪些盘/文件夹”步骤中的流程再跑一遍

#### 写在后面

+ gdir可以在本地（Windows或linux）或者VPS上配置，但不论是在哪里配置，以上整个过程都是来生成GitHub的gist和CF Worker的配置文件，配置好后部署和数据传输都是走 CF；跟本地计算机和VPS无关
+ 配置好用可以删除环境依赖（装的各种软件）
+ 配好是生成的所有文件都在gdir文件夹下面，并且是绿色的，请备份好gdir文件夹，以备后面根性！和迁移到新的机器！
+ 更新请使用命令：git pull






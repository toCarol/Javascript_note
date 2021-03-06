## Jenkins安装
1. 安装JDK1.8+ 并配置环境变量
2. Jenkins官网下载Jenkins for windows
3. 点击Jenkins.msi文件，安装Jenkins,安装完毕后，在浏览器通过localhost:8080查看Jenkins页面

## Jenkins 插件安装
在左侧系统菜单中选择：系统管理 => 管理插件 => 可选插件
可搜索想要安装的插件

## Jenkins+SonarQube自动化部署
1. 安装插件：SonarQube Scanner for Jenkins / 

2. 系统配置：

**SonarQube Servers**
注意：
- 此处server URl填写你的sonarQube所在的服务器，由于我是安装在本地的，所以是localhost
- server authentication token: 需要在sonarQube中生成
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins1.PNG)

**gitHub**
注意：
- API URL：个人版和企业版的URl不一样，需要注意，此处我填写的是企业版的
- Credentials: 这里需要添加在github上生成的token. 添加后可以点击下面的“Test connection”按钮，检测token是否可以正常连接到github
- 点右下方的第二个“高级”按钮，添加Hook URL和 Shared secret.
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins2.PNG)
- 需要将Jenkins中生成的hook添加到github项目中。
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins13.PNG)


**GitHub pull Request Builder**
GitHub pull Request Builder 可以配置在github上提交pull request时触发Jenkins 构建
配置如下：
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins3.PNG)

3. 全局工具配置：
**JDK**
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins4.PNG)

**Git**
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins5.PNG)

**SonarQube Scanner**
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins6.PNG)

## 项目配置
1. 新建一个自由风格的项目
2. 填写基本配置
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins7.PNG)
3. 源码管理
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins8.PNG)
4. 构建触发器
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins9.PNG)
5. 构建，选择SonarQube Scanner
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins10.PNG)
6. 增加构建步骤
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins11.PNG)
7. 增加构建后操作
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins12.PNG)

## 执行构建
在github中提交代码后创建一条pull request,会在Jenkins中开始自动构建：
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins14.png)
在github的pull request中可以看到相应的Jenkins build的状态表示：
![avatar](https://raw.githubusercontent.com/toCarol/Javascript_note/master/image/Jenkins15.png)

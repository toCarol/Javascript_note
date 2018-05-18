## 操作系统
- windows

## SonarQube7.1
- SonarQube7.1  前往SonarQube官网下载SonarQube稳定版本（https://www.sonarqube.org/#_）
- SonarQube Scanner 3.1  下载插件（https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner）

## Java
- Oracle JRE8+
- JDK8+

## 开始安装
安装SonarQube
- 将下载的sonarqube-7.1.zip解压
- 进入目录sonar-7.1/bin/windows-x86-64
- 双击StartSonar.bat文件
- 在浏览器访问http://localhost:9000/ ,默认的用户名/密码：admin/admin

## 解析项目
1. 配置sonar Scanner
- 解压sonar-scanner-3.1.0.1141-windows.zip
- 配置环境变量：1.新建系统变量(变量名：SONAR_SCANNER ;变量值：即sonar-scanner解压后的路径） 2.在Path变量值的末尾添加%SONAR_SCANNER%\bin;
- 打开命令提示符：输入sonar-scanner -version 查看环境变量是否配置成功
- 修改sonar-scanner-3.1.0.1141-windows目录下conf/sonar-scanner.properties,将sonar.host.url改为sonar的ip,本地安装可以直接填写http://localhost:9000

2. 分析一个项目
- 在你想要分析的项目的根目录创建sonar-project.properties文件
- 在sonar-project.properties中配置一些基础参数：如下


    //项目的key
    sonar.projectKey=react-demo
    //项目的名字
    sonar.projectName=C:\Users\admin\Desktop\todomvc
    //项目的版本
    sonar.projectVersion=1.0.0
    //需要分析的源码目录
    sonar.sources=react
    //需要分析的语言
    sonar.language=js
    sonar.sourceEncoding=UTF-8

- 在项目目录下执行命令：sonar-scanner (即开始对项目进行分析)
- 分析结束后在分析结果中会有一个连接，打开该链接即可查看分析报告

3. 添加覆盖率扫描结果
使用istanbul扫描覆盖率(前提：已编写单元测试用例。这里我采用的mocha进行单元测试。)
- 在项目中安装istanbul


    cnpm install --save-dev istanbul@v1.1.0-alpha.1

- 在package.json中写入：

    "script": {
        "coverage": "istanbul cover node_modules/mocha/bin/_mocha -t 2000000 --compilers js:babel-register --recursive tools/testSetup.js test/contianers/*.spec.js"
    },

- 在项目下执行 npm run coverage,可以生成覆盖率报告
- 在新生成的coverage目录下可以看到生成了一个lcov.info文件，该文件用于向sonar提供覆盖率结果
- 在sonar-project.properties中添加配置：


    sonar.tests=test/containers       //需要测试的目录
    sonar.test.inclusions=/*.spec.js  //需要测试的文件 
    sonar.javascript.lcov.reportPaths=coverage/lcov.info       //覆盖率报告的路径

- 在项目下执行sonar-scanner 即可生成含有覆盖率数据的分析报告

## 在同一个项目中分析不同类型的文件配置方法

    sonar.projectKey=ncsDownload
    sonar.projectName=ncs-download
    sonar.projectVersion=1.0
    sonar.sourceEncoding=UTF-8
    sonar.modules=javascript-module,CSS-module,HTML-module

    ## JavaScrit module
    javascript-module.sonar.projectName=ncsDownload_js
    javascript-module.sonar.language=js
    javascript-module.sonar.sources=js
    javascript-module.sonar.projectBaseDir=.

    ## CSS module
    CSS-module.sonar.projectName=ncsDownload_css
    CSS-module.sonar.language=css
    CSS-module.sonar.sources=css
    CSS-module.sonar.projectBaseDir=.

    ## HTML module
    HTML-module.sonar.projectName=ncsDownload_HTML
    HTML-module.sonar.language=web
    HTML-module.sonar.sources=.
    HTML-module.sonar.exclusions=css/*.css,js/*.js,     //排除某些目录
    HTML-module.sonar.projectBaseDir=.










# 快速构建React项目，只需10个npm包



## **b话也不多说吧，直接切入正题，如何快速搭建一个React项目呢（包含webpack）**

## **一、创建文件夹**

```text
mkdir react-quick-project && cd react-quick-project
npm init -y  //这里是一个小技巧 不用敲回车直接一步生成起始项目
```

![img](https://pic4.zhimg.com/80/v2-a816aa8b3209a4319aeaf6f6b109b7eb_720w.jpg)

## **二、下载10个npm包**

```text
npm i react react-dom -S //生产用的
npm i babel-core babel-loader babel-preset-env babel-preset-react html-webpack-plugin webpack webpack-cli webpack-dev-server -D //开发用的
```

![img](https://pic3.zhimg.com/80/v2-3f5ccf93ad03ddf9035c89da971a0f7a_720w.jpg)package.json

## **三、编写webpack.config.js文件**

在项目根目录新建一个webpack.config.js文件，内容如图：

![img](https://pic2.zhimg.com/80/v2-be350be4ed86ac07dabe3a8fc50806f5_720w.jpg)

webpack.config.js



## **四、编写项目的入口index.js**

在根目录新建src文件夹，在src文件里新建一个index.js，内容如下

![img](https://pic3.zhimg.com/80/v2-ec0d6a4739b74448aff7735e7db5d762_720w.jpg)index.js入口

## **五、新建一个index.html作为项目的模板页面**

在src目录下新建一个index.html模板文件如图所示

webpack在构建的时候会通过htm-webpack-plugin去构建这个模板页面引入生产的bundle.js脚本

![img](https://pic4.zhimg.com/80/v2-b4a282d2f0f4c8dc2d4fde72405772b3_720w.jpg)index.html

## **六、新建一个App容器页面**

新建一个components文件夹，在文件夹里新建一个App.jsx 如图所示

![img](https://pic2.zhimg.com/80/v2-b7d824768a1ea7e130099fa873e209b9_720w.jpg)App.jsx

## **七、在根目录新建一个.babelrc**

新建一个.babelrc文件，babel编译代码的时候会取这个文件内的设置

.

![img](https://pic1.zhimg.com/80/v2-e7986d4bb884e5d454a747237c9a04c4_720w.jpg).babelrc

## **八、修改package.json**

scripts改为如图所示，webpack-dev-server开启本地开发环境，build打包项目生成静态资源

![img](https://pic3.zhimg.com/80/v2-88ba1b06bbe1169c5674d45400627332_720w.jpg)package.json

## **九、接下来就是见证奇迹的时刻**

回到命令行界面运行

```text
npm run start
```

本地默认打开http://localhost:8080端口监听开发页面

![img](https://pic1.zhimg.com/80/v2-816cc73392c60f8ecacdc5af6143ec9c_720w.jpg)编译成功

运行生产环境打包

```text
npm run build
```

![img](https://pic1.zhimg.com/80/v2-4dc27e8bcbc98a7a9609f4adfaa5ffbc_720w.jpg)

![img](https://pic1.zhimg.com/80/v2-5405a4f66af6bbd74724e6fc4d23f1a4_720w.jpg)



打包后生成的index.html可以直接在浏览器打开浏览，也可以直接把两个文件丢到cdn或是服务器都能正常跑。



![img](https://pic4.zhimg.com/80/v2-b1eac821b10c53fd8c152b5f16cb3993_720w.jpg)





**以上对React的一个构建做了一个简单的小教程，大家互相探讨学习。**

发布于 2018-12-07 17:33
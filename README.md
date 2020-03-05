## nCoV 
> 武汉加油🍻

## 功能
 - [x] 人数情况查看
 - [x] 全国和各省市疫情地图及其详细信息查看
 - [x] 最新消息
 - [x] 造谣信息
 - [x] 疫情趋势
 - [x] 死亡率和治愈率

## 快速开始
- clone项目: git clone https://github.com/ruanshr/nCoV-Virus.git
- 安装依赖: cd nCoV-Virus && npm install
- 运行: npm start
- 打包: npm run build

## 部署
通过docker的Dockerfile文件制作为镜像，然后通过nginx来进行部署。
Dockerfile:
```
# ncov Dockerfile

#指定node镜像对项目进行依赖安装和打包
FROM node:10.16.0 AS builder
# 将容器的工作目录设置为/app(当前目录，如果/app不存在，WORKDIR会创建/app文件夹)
WORKDIR /app 
COPY package.json /app/ 
RUN npm config set registry "https://registry.npm.taobao.org/" \
    && npm install
 
COPY . /app   
RUN npm run build 

#指定nginx配置项目，--from=builder 指的是从上一次 build 的结果中提取了编译结果(FROM node:alpine as builder)，即是把刚刚打包生成的dist放进nginx中
FROM nginx
COPY --from=builder app/build /usr/share/nginx/html/
COPY --from=builder app/nginx.conf /etc/nginx/nginx.conf


#暴露容器80端口
EXPOSE 80
```



## 数据来源
 - [天行数据-抗击肺炎](https://www.tianapi.com/apiview/169)
 - [地图Json](https://github.com/huanent/vue-echarts-map-demo)
 - [疫情发展趋势折线图](https://github.com/BlankerL/DXY-2019-nCoV-Crawler)

 在此特地鸣谢！  
 希望武汉疫情能够早日过去！
  
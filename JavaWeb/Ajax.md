# 什么是 Ajax？

- 概念: Asynchronous JavaScript And XML，**异步**的 JavaScript 和 XML。
- 作用:
  - 数据交换: 通过Aiax可以给服务器发送请求，并获取服务器响应的数据。
  - 异步交互: 可以在**不重新加载整个页面**的情况下，与服务器交换数据并**更新部分网页**的技术，如: 搜索联想、用户名是否可用的校验等等。

# 原生Ajax

1. 准备数据地址
2. 创建XMLHttpRequest对象: 用于和服务器交换数据
3. 向服务器发送请求
4. 获取服务器响应数据

# Axios

- 介绍: Axios 对原生的 Ajax 进行了封装，简化书写，快速开发。
- 官网: https://www.axios-http.cn/

## 1. 引入Axios的js文件

`<script src="js/axios-0.18.0.js"></script>`

## 2. 引入Axios的js文件

```javascript
axios({
	method: "get",
	url: "http://yapi.smart-xwork.cn/mock/169327/emp/list"}).then(result => {
	console.log(result.data);
});

axios({
	method:"post"
	url: "http://yapi.smart-xwork.cn/mock/169327/emp/deleteByld",
	data:"id=1"
}).then(result => {
	console.log(result.data);
});
```

### 请求方式别名

- axios.get(url [, config])

- axios.delete(url [, config])

- axios.post(url [, data[, config]])

- axios.put(url [, data[, config]])

### 发送GET请求

```javascript
axios.get("http://yapi.smart-xwork.cn/mock/169327/emp/list").then((result) => {
    console.log(result.data);
});
```

### 发送POST请求

```javascript
axios.post("http://yapi.smart-xwork.cn/mock/169327/emp/deleteByld","id=1").then((result) => {
    console.log(result.data);
});
```

 
## 概览

Ajax（Asynchronous JavaScript and XML）是基于浏览器原生 `XMLHttpRequest`（XHR）对象的异步请求技术，允许在不重新加载整个页面的情况下更新局部内容 。
jQuery 在其基础上提供了 `$.ajax` 等封装方法，简化配置与回调处理 。
xios 则是一个基于 Promise 的 HTTP 客户端，可运行于浏览器和 Node.js，自动处理 JSON 序列化、请求/响应拦截、取消请求等，API 设计更为现代和灵活。

* * *

## 原生 Ajax（XMLHttpRequest）

### 1. 核心对象与状态码

-   **XMLHttpRequest**：浏览器内置的 JavaScript API，用于发送 HTTP 请求并获取响应 citeturn0search0。

-   **readyState** 五个状态：

    1.  `0` UNSENT：`open()` 未调用 citeturn0search5
    1.  `1` OPENED：已调用 `open()`，未调用 `send()`
    1.  `2` HEADERS_RECEIVED：`send()` 后已接收响应头
    1.  `3` LOADING：接收响应主体中 citeturn0search0
    1.  `4` DONE：全量响应已就绪，可在浏览器中使用 citeturn0search12

-   **HTTP 状态码**：仅当 `readyState === 4` 且 `status` 在 200–299 范围内，才认为请求成功，并处理 `responseText` 或二进制 `response` citeturn0search2。

### 2. 基本使用流程

```
const xhr = new XMLHttpRequest();                                           // 创建 XHR 对象
xhr.onreadystatechange = () => {
  if (xhr.readyState !== 4) return;                                         // 等待 DONE
  if (xhr.status >= 200 && xhr.status < 300) {
    console.log(xhr.responseText);                                          // 处理响应
  }
};
xhr.open('GET', 'data.json', true);                                         // 初始化请求：方法、URL、异步
xhr.send(null);                                                             // 发送请求（GET 时参数为 null）
```

-   异步模式（`true`）下可在发送后继续执行其他 JS，不会阻塞界面渲染 citeturn0search6。
-   `xhr.responseType` 可设置 `"json"`、`"blob"`、`"arraybuffer"` 等，免去手动 `JSON.parse` 操作 citeturn0search0。

### 3. 高级配置与技巧

-   **超时控制**：`xhr.timeout = 5000; xhr.ontimeout = () => { /* 处理超时 */ }`。
-   **同步模式**（`open(..., false)`）会阻塞页面，不推荐使用。
-   **上传/下载进度**：`xhr.upload.onprogress` 与 `xhr.onprogress` 可获取进度信息。
-   **跨域请求**：需要服务器设置 CORS 头，如 `Access-Control-Allow-Origin`。

* * *

## jQuery Ajax 封装

### 1. `$.ajax()` 核心用法

```
$.ajax({
  url: '/api/data',
  method: 'POST',            // jQuery 1.9+ 可用 method，旧版用 type
  dataType: 'json',          // 自动将响应解析为 JSON
  data: { id: 123 },         // POST 请求体或 GET 查询参数
  timeout: 3000,             // 毫秒
  headers: { 'X-Auth': 'token' },
  beforeSend: xhr => { /* 发送前钩子 */ },
  success: (data, status, xhr) => { /* 成功回调 */ },
  error: (xhr, status, err) => { /* 失败回调 */ },
  complete: xhr => { /* 请求完成后 */ }
});
```

-   可通过 `$.ajaxSetup({})` 定义全局默认值 citeturn0search2。
-   简化方法：`$.get()`、`$.post()`、`$.getJSON()`、`$.load()` 等，分别对应常见场景 citeturn0search22。

### 2. 全局事件与封装

-   **全局事件**：`ajaxStart`、`ajaxSend`、`ajaxSuccess`、`ajaxError`、`ajaxComplete`、`ajaxStop`，便于统一显示加载进度或错误提示。
-   jQuery 本质上是对原生 XHR 的封装，统一处理了跨浏览器兼容性和回调管理，适合简单项目快速上手 citeturn0search12。

* * *

## Axios 深入

### 1. 安装与引入

```
npm install axios         # 或 yarn add axios
```

````
import axios from 'axios';                                           // ES Module
const axios = require('axios');                                      // CommonJS
``` citeturn0search1

### 2. 基本请求方法  

| 方法         | 用法                                        |
| ------------ | ------------------------------------------- |
| `axios.get`  | `axios.get(url[, config])`                  |
| `axios.post` | `axios.post(url[, data[, config]])`         |
| `axios.put`  | `axios.put(url[, data[, config]])`          |
| `axios.delete` | `axios.delete(url[, config])`             |
| `axios()`    | `axios(config)` —— 通用方法                  | citeturn0search11  

```js
axios.get('/users')
  .then(resp => console.log(resp.data))                                 // 自动 JSON 解析
  .catch(err => console.error(err));                                    // 捕获网络或响应错误
````

### 3. 全局配置与实例化

-   **默认配置**：

    ````
    axios.defaults.baseURL = 'https://api.example.com';
    axios.defaults.timeout = 5000;
    axios.defaults.headers.common['Authorization'] = 'Bearer TOKEN';
    ``` citeturn0search7  
    ````

-   **创建实例**：

    ````
    const api = axios.create({
      baseURL: '/v1',
      timeout: 3000,
      headers: { 'X-Custom': 'foo' }
    });
    api.get('/data').then(...);
    ``` citeturn0search9
    ````

### 4. 拦截器（Interceptors）

-   **请求拦截**：在请求发送前修改 `config`，添加认证、日志等。

    ````
    axios.interceptors.request.use(cfg => {
      cfg.headers['X-Auth'] = 'token';
      return cfg;
    }, err => Promise.reject(err));
    ``` citeturn0search3  
    ````

-   **响应拦截**：统一提取 `response.data`、错误转换等。

    ````
    axios.interceptors.response.use(res => res.data,
      err => Promise.reject(err));
    ``` citeturn0search13
    ````

### 5. 错误处理

```
axios.get('/items')
  .catch(error => {
    if (error.response) {
      console.error('服务器错误：', error.response.data);
    } else if (error.request) {
      console.error('未收到响应：', error.request);
    } else {
      console.error('其他错误：', error.message);
    }
  });
```

-   `validateStatus` 可自定义哪些 HTTP 状态视为成功 citeturn0search8。
-   `error.toJSON()` 可输出更详细的错误信息。

### 6. 取消请求

-   **CancelToken**（已废弃）：基于早期可取消 Promise 提案 citeturn0search4。

-   **AbortController**（推荐）：现代浏览器原生支持，更符合 Fetch API 规范。

    ```
    const controller = new AbortController();
    axios.get('/long', { signal: controller.signal });
    // …
    controller.abort();
    ```

### 7. 进阶功能

-   **并发请求**：`axios.all([req1, req2]).then(axios.spread((r1, r2) => {…}))`。
-   **数据转换**：`transformRequest`、`transformResponse` 可自定义序列化/反序列化 citeturn0search17。
-   **上传/下载进度**：`onUploadProgress`、`onDownloadProgress` 回调获取进度。

* * *

## Ajax vs. Axios 对比

| 特性         | 原生 XHR/Ajax      | Axios                                  |
| ---------- | ---------------- | -------------------------------------- |
| 体积         | 无外部依赖            | ~13KB gzip                             |
| API 样式     | 回调为主             | Promise + async/await                  |
| 自动 JSON 处理 | 需手动 `JSON.parse` | 自动解析                                   |
| 拦截器        | 需自行封装            | 原生支持                                   |
| 并发控制       | 需自行管理            | `axios.all`                            |
| 请求取消       | `xhr.abort()`    | `AbortController`（现代）/`CancelToken`（旧） |
| 浏览器兼容      | IE7+             | 与 XHR 相同                               |

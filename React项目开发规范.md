# React 项目开发规范

## 目录命名规范

### 项目整体目录
￼

![图片](https://user-images.githubusercontent.com/8686869/30628202-7007a27a-9e07-11e7-8055-ff80baa2ccc3.png)

### 按业务划分目录

同一业务类型的相关页面在业务目录下

### 一个组件一个目录

包含相关的 jsx、css、test、images 等相关资源，按照就近依赖原则

```
index.html
index.css
index.js
App.js
XXComponent.js
YYComponent.js
__tests__
  App.test.js
.....
```

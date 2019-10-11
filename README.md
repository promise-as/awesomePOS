## 项目打包上限

- 把绝对路径改为相对路径

  ```js
  // 修改之前
  build: { 
      assetsPublicPath: '/', 
  }
  // 修改之后
  build: { 
      assetsPublicPath: './', 
  }
  ```

  
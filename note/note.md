## 1、创建vue-js-demo项目

### 1.1. 创建项目

### 1.2. 配置代码格式化文件

 1. 创建`.prettierrc`文件

 2. 添加内容

    ```json
    {
      "semi": true,
      "singleQuote": true,
      "arrowParens": "always",
      "trailingComma": "all",
      "jsxSingleQuote": true
    }
    
    ```

    

## 2、使用GitHub-Actions发布初始项目

### 2.1. 创建vue.config.js文件

```javascript
//vue.config.js
module.exports = {
  // 选项
  publicPath: process.env.NODE_ENV === 'production' ? '/vue-js-demo/' : '/',
};

```

### 2.2. 创建actions工作文件

1.  创建`.github/workflow`文件夹

2.  创建yml文件(ci.yml)

   ```yaml
   name: GitHub Actions Build and Deploy Demo
   on:
     push:
       branches:
         - develop
   jobs:
     build-and-deploy:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout 🛎️
           uses: actions/checkout@v2.3.1 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
           with:
             persist-credentials: false
   
         - name: Install and Build 🔧 # This example project is built using npm and outputs the result to the 'build' folder. Replace with the commands required to build your project, or remove this step entirely if your site is pre-built.
           run: | #注意我这里是使用的yarn管理包，如果你使用的npm，请换成npm的命令：npm install和npm run build
             yarn
             yarn build
         - name: Deploy 🚀
           uses: JamesIves/github-pages-deploy-action@3.6.2
           with:
             ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }} #secrets.ACCESS_TOKEN是项目配置的密钥
             BRANCH: mantou-pages # The branch the action should deploy to.
             FOLDER: dist # The folder the action should deploy.
             CLEAN: true # Automatically remove deleted files from the deploy branch
   
   ```

## 3、添加内容






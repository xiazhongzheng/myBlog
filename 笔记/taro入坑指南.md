1. 安装

   ```
   npm install -g @tarojs/cli // 安装不成功，可能是npm地址是ymm的原因
   yarn global add @tarojs/cli // 安装成功，但是taro命令不存在。环境变量path，加上 yarn bin的地址
   ```

2. 多端同步调试

   ```
   在 config/index.js 中配置 outputRoot: `${process.env.TARO_ENV === 'h5' ? 'dist' : 'dist-' + process.env.TARO_ENV}`,
   在 project.config.json 文件的 miniprogramRoot 的值改为 dist-weapp/
   但是，definePageConfig 页面配置的导航标题 navigationBarTitleText 不生效了。。。
   ```

   
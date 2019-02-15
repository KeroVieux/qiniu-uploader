# qiniu-uploader

> 使用七牛的用户，想必大部分都是国人，这里就使用中文做一下简介吧！  
> Hey guy, perhaps it's a wrong way for you here, if you are doing the qiniu in vue and there is a little hassle , I am eager to help , email me.  
> 这是一个针对七牛上传文件的input[type="file"]，并不是一个封装完成的插件，仅供参考代码应用。但，加入了多选文件、loading效果、基础样式、用户体验的判断，只要照搬代码到你的项目中，基本能满足在客户端的上传动作，调用方法可以参见 [调用例子]('example/index.vue')
    
## 依赖
- axios - 上传和获取token需要
- font-awesome - 图标

## 组件说明
### props接收参数
- accepts - 限制上传文件类型，默认为图片
- multiple - 支持多选开关，true/false
- maxSize - 最大文件支持，默认为不限制（不建议）

### 方法说明
- upload - 选择文件后触发，从api获取token后上传文件到七牛服务器

## 使用例子说明
- 支持多选、选择完成后自动触发上传动作以及查看
- 并没有真正的删除已上传的文件

## 截图
![截图](http://img.hidoge.cn/FuInm-N6_6oH0cTTCweA2NHZU6r6 "截图")
![截图](http://img.hidoge.cn/FtFEqaFLB0sdhrSMptw5WhVbt-ve "截图")

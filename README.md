# 精品网址导航站

<p align="center">
  <img src="https://github.com/user-attachments/assets/c0200239-4b89-4f3f-9d5d-99f731661d7c" alt="Logo" width="200">
</p>

<p align="center">
  一个优雅的书签收藏与分享平台，基于Cloudflare Workers构建
</p>

<p align="center">
  <a href="#✨-特性">特性</a> •
  <a href="#🚀-快速开始">快速开始</a> •
  <a href="#📦-部署指南">部署指南</a> •
  <a href="#🔧-技术栈">技术栈</a> •
  <a href="#🌟-贡献">贡献</a>
</p>

## ✨ 特性

- 📱 **响应式设计** - 完美适配各种设备屏幕
- 📋 **分类浏览** - 按类别组织书签，简单直观
- 🔍 **站内搜索** - 快速查找需要的网站
- 📝 **书签提交** - 用户可申请添加新书签
- 🛡️ **审核机制** - 管理员审批流程保证内容质量
- 🔒 **安全认证** - 支持 KV 存储保存管理员凭据
- 📊 **后台管理** - 完整的书签管理界面
- 📤 **导入导出** - 支持批量导入导出书签

## 🖼️ 预览图

![image](https://github.com/user-attachments/assets/b12755c5-7669-408f-be05-2db6ba1b02cc)

![image](https://github.com/user-attachments/assets/d387794d-95f8-42e9-879d-41fc6c5f5fa8)

## 📦 部署指南

### 步骤 1: 创建 DB 数据库和 KV 键值对

创建 D1 数据库,输入名称**book** ,点击创建!

![image](https://github.com/user-attachments/assets/f49d61ea-a87b-42ed-a460-98e53fb340e0)

点击控制台,分别创建表**sites**,**pending_sites**,看下图字段!

![image](https://github.com/user-attachments/assets/fdc5c65d-3726-4e71-8163-62dc2ed1bbdf)

![image](https://github.com/user-attachments/assets/735e63b7-1ba8-49ce-94e6-0ccf9bf55042)

创建 KV,名称**NAV_AUTH**,根据自己实际情况修改密钥的值,这是后续用于登陆后台管理的账号密码!

![image](https://github.com/user-attachments/assets/ed274f2d-2bf0-4f26-aa86-90e22286e94b)

![image](https://github.com/user-attachments/assets/2fd5742f-5709-4ad9-b4fa-865cbca0bb8e)

### 步骤 2: 创建 workers

看下图,点击 hello worker 创建一个 workers,输入自定义名称进行创建!

![image](https://github.com/user-attachments/assets/02c3d4c4-6746-45fe-a428-516023fed880)

然后点击编辑代码,将本项目中的 worker.js 代码复制粘贴进去,替换原有代码,点击部署!

![image](https://github.com/user-attachments/assets/f2f4fe86-aab1-4805-9ba3-bac8b889875d)

然后前往设置中,绑定 KV 和 DB

![image](https://github.com/user-attachments/assets/269f4678-4e8a-4dbd-a8d7-f186466f4380)

然后访问页面即可,此时由于没有添加书签,访问首页会提示没有数据,可以前往 admin 后台登陆之后,添加一个书签,即可看到页面!

![image](https://github.com/user-attachments/assets/6f3e0185-25b4-423e-b34c-26f88aabb807)

页面提示这个信息!

![image](https://github.com/user-attachments/assets/9b9ae7fb-9857-4481-b758-b58a556abf6f)

网址后面拼接 /admin 即可进入后台页面,输入在 DB 中设置的密码,然后进行添加!

![image](https://github.com/user-attachments/assets/284e3560-284f-4313-a7c6-d651d2e25c00)

再回到首页,就能看到网站了!

![image](https://github.com/user-attachments/assets/99c27184-6688-4464-b6c9-d29882927032)

## 🔧 技术栈

- [Cloudflare Workers](https://workers.cloudflare.com/) - 边缘计算平台
- [Cloudflare D1](https://developers.cloudflare.com/d1/) - 边缘 SQL 数据库
- [Cloudflare KV](https://developers.cloudflare.com/workers/runtime-apis/kv/) - 键值存储
- [TailwindCSS](https://tailwindcss.com/) - 实用程序优先的 CSS 框架

## 💻 项目结构

```
nav/
├── worker.js          # 主应用代码
├── schema.sql         # 数据库结构
└── README.md          # 项目文档
```

## 🛠️ 自定义开发

### 修改样式和主题

编辑`worker.js`中的 TailwindCSS 配置部分：

```js
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: {
          // 修改主色调
          500: '#7209b7',
        },
        // ...其他颜色配置
      },
    },
  },
}
```

### 添加自定义功能

本项目使用 Cloudflare Workers 的单文件结构，所有逻辑都在`worker.js`中。主要模块:

- `api`: API 请求处理
- `admin`: 管理后台逻辑
- `handleRequest`: 前端页面渲染

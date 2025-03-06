# 分支修改

- 密码访问

使用变量PWD并且 浏览器访问主页需要列如 `home.com/?pwd=token`

- 照片墙

/gallery 访问照片墙

按照目录划分，文件名会当标签 列如 `标签1-标签2-标签3.webp`

# Luminest

一个基于 Cloudflare Workers 和 R2 存储的轻量级图床服务。

## 特性

- **便捷上传**：支持拖拽上传和多文件上传，极大提升上传效率。
- **文件夹管理**：具备文件夹管理功能，方便用户对图片进行分类整理。
- **自动重命名**：采用时间戳自动重命名机制，避免文件命名冲突。
- **灵活操作**：支持对图片进行移动和删除操作，便于管理。
- **链接生成**：自动生成 Markdown 格式链接，方便在文档中插入图片。
- **默认存储**：默认使用`blog`文件夹存储图片，条理清晰。

## 部署步骤

**安装依赖**

执行命令：`npm install`

**配置 wrangler.toml**

在`wrangler.toml`文件中进行如下配置：

```
name = "r2-picbed" # 你的 Worker 名称
main = "src/worker.js"
compatibility_date = "2023-12-01"
[[r2_buckets]]
binding = "MY_BUCKET"
bucket_name = "images" # 你的 R2 bucket 名称
preview_bucket_name = "images" # 本地开发用的 bucket 名称
[vars]
R2_DOMAIN = "https://your-domain.com" # 你的 R2 自定义域名
```

**创建 R2 bucket**

登录 Cloudflare

执行`wrangler login`

创建 R2 bucket：`wrangler r2 bucket create images`

**部署与调试**

部署：`npm run deploy`

调试：`npm run dev`，访问`http://localhost:8787`进行调试

## 注意事项

**Cloudflare 设置**

确保已在 Cloudflare 控制面板中创建 R2 bucket。

（可选）配置自定义域名。

设置适当的 CORS 策略。

**文件夹命名规则**

文件夹只能包含字母、数字、下划线和横线。

默认使用`blog`文件夹。

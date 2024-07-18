# hammal

Hammal 是运行于 cloudflare workers 上的 Docker 镜像加速工具，用于解决获取 Docker 官方镜像无法正常访问的问题。

文档： https://singee.atlassian.net/wiki/spaces/MAIN/pages/5079084/Cloudflare+Workers+Docker 


## 启动

安装wrangler

```bash
npm install wrangler --save-dev
```

登录

```bash
wrangler login
```

创建KV namespace

```bash
wrangler kv namespace create docker_cache
```

基于·wrangler.toml.sample·创建wrangler.toml

```toml
name = "hammal" //要创建的cloudflare worlers 应用程序的名称
account_id = "1492*********" //上一步查看到的account id
workers_dev = true
main = "./src/index.ts"
compatibility_date = "2021-12-07"
//将创建KV namespace 中的id 写入下方，注意 binding = "HAMMAL_CACHE" 不需要修改
kv_namespaces = [
         { binding = "HAMMAL_CACHE", id = "00fe55d3*****95ac1063847bf" }
]
```

部署

```bash
wrangler deploy
```

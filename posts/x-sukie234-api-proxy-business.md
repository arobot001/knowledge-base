# X Post: 运营中转站开源教程

**来源**: https://x.com/sukie234/status/2052064204132155676  
**作者**: @sukie234  
**发布时间**: 2025年（根据推文ID推断）  
**抓取时间**: 2026-05-07

---

## 原文内容

运营中转站这段时间是真没赚到钱，只能说勉强cover了我自己用ai的消费。
所以目前打算把开中转站的一切全部开源，包含如何建站+营销，门槛最低，让这个行业更卷一点。

### 系统架构（3个部分）

1. **CN2 回国专线服务器**：放在海外但回国速度极快的 VPS，作为运行核心
2. **sub2api**：核心程序，负责把网页账号转成 API 接口
3. **Cloudflare**：把流量再绕一道，提升国内访问速度，同时隐藏真实服务器 IP

### 需要准备的资源

- 一台 **CN2 GIA 或 CN2 GT** 线路的海外 VPS（推荐配置：2核 CPU、2GB 内存、20GB 硬盘以上）
  - 普通海外 VPS 在国内晚高峰几乎不可用
  - CN2 GIA 通过专线绕开拥堵公网节点，国内访问延迟一般在 150ms 以内
- 一个域名（建议在 Cloudflare 或 Namecheap 购买，便宜的 .top 或 .xyz 也行）
- 一个 Cloudflare 账号（免费）
- **号池**：初期可用 Claude Code Pro 账户 + 注册大量 GPT 账户，后期可转 Claude Code Max/Kiro，反代 AWS Bedrock（可谈到 7.2 折）

### 完整请求路径

```
国内用户客户端 → Cloudflare IP → Cloudflare 边缘节点 → CN2 专线回源 → 服务器
→ 宝塔面板 Nginx 反向代理 → sub2api 程序 → 号池 → ChatGPT/Claude 网页
→ 数据原路返回
```

### CN2 服务商推荐

- **BandwagonHost（搬瓦工）**：CN2 GIA-E 套餐，稳定但价格略贵
- **RackNerd**、**CloudCone**、**Lisahost**
- 预算紧推荐 **Lisahost 香港 CN2**

### 部署步骤

1. **服务器初始化**：安装 Linux + Nginx + MySQL + PHP（可用宝塔面板一键安装）
2. **设置防火墙**，购买域名，添加 DNS 解析
3. **验证**：ping api.你的域名，应返回服务器 IP
4. **搭建 sub2api**：
   - 安装 Docker
   - 拉取并启动 sub2api 容器
   - 号池数据放 `/www/sub2api/data` 目录
5. **Nginx 反向代理**：目标 URL 设为 `127.0.0.1:8080`
6. **优化 Nginx 配置**：关闭 `proxy_buffering`，确保 SSE 流式响应正常
7. **申请 HTTPS 证书**：Let's Encrypt，开启"强制 HTTPS"

### Cloudflare 配置优化

**SSL 模式**：必须设为 **Full (strict)**

**关闭的优化选项**（会破坏流式响应）：
- Auto Minify（自动压缩 HTML/CSS/JS）
- Rocket Loader
- Mirage
- Polish

**缓存规则**：
- Caching Level 选 Bypass
- 或创建页面规则：`api.example.com/*` → Cache Level = Bypass

**防火墙规则**：
- 限制单个 IP 频率：每 10 秒最多 30 次请求
- 屏蔽恶意爬虫：User Agent 包含 `python-requests`

**可选加速**：
- Cloudflare Argo Smart Routing（$5/月），国内访问速度提升 30-50%

### 测试与监控

- 用 curl 或 CherryStudio/ChatBox 测试 API
- 监控：Prometheus/Grafana 或宝塔面板，关注 CPU、内存、流量
- 如 sub2api 容器经常吃满 CPU，考虑升级服务器配置

---

## 互动数据

- 👍 点赞：714
- 🔁 转推：105
- 👁️ 浏览：56,574

---

## 标签/关键词

#AI #API #中转站 #Claude #ChatGPT #开源教程 #Cloudflare #CN2 #副业

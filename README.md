# argo-cfs-ecloudserv

ecloudserv.fr 部署专用仓库（Git 源码部署，Node.js PaaS，不构建 Docker 镜像）。

- `index.js` 混淆，内嵌部署配置（不可读）
- 依赖 axios（部署时自动 `npm install`）
- 运行时自动下载缺失的二进制：xray 代理 / cloudflared 隧道 / cf-probe 探针
  （首次启动自动从 oooen.com + GitHub 拉取，无需镜像内预置 `/opt/bin`）
- 含 CF 探针 + Argo 固定隧道 + 书签首页

## 部署填法

| 字段 | 值 |
|------|-----|
| 仓库 | `nicsrvdev/argo-cfs-ecloudserv` |
| 分支 | `main` |
| 安装命令 | `npm install`（或留空，平台自动运行） |
| 构建命令 | 留空 |
| 启动命令 | `node index.js` |

无需在平台配置任何环境变量——配置已内嵌进混淆的 `index.js`。

## 说明

- 首次启动需下载约 84MB 二进制（xray 36MB + cloudflared 41MB + cf-probe 7.5MB），之后常驻 `/opt/bin`
- 三个二进制以随机文件名运行（防检测）
- 干净源码见 [nicsrvdev/argo-cfs](https://github.com/nicsrvdev/argo-cfs) 的 `index-src.js`

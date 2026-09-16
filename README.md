# config-repo

Spring Cloud Config 远程配置仓库，为 `cloud-config-center1` 等微服务客户端提供多环境 YAML 配置。

## 配置文件一览

| 文件 | 端口 | 用途 |
|------|------|------|
| `config-client.yml` | 7777 | 默认/基础环境 |
| `config-client-dev.yml` | 7778 | 开发环境（`login.log` 标识 dev） |
| `config-client-text.yml` | — | 测试环境 |
| `config-client-prod.yml` | 7780 | 生产环境 |

各文件均包含：

- `server.port`：服务端口
- `spring.application.name`：注册到 Eureka 的服务名 `cloud-config-center1`
- `login.log`：环境标识日志字段，便于区分配置来源

## 示例（config-client.yml）

```yaml
server:
  port: 7777
---
spring:
  application:
    name: cloud-config-center1
---
login:
  log: com1-is-config-client------------
```

## 使用说明

1. 在 Config Server 中配置本 Git 仓库地址与分支（`main`）。
2. 客户端通过 `spring.cloud.config.uri` 拉取对应 profile 的配置。
3. 修改配置后 push 到本仓库，触发 Config Server 刷新或客户端 `/actuator/refresh`。

## 仓库信息

- **GitHub**：https://github.com/hubaolong3632/config-repo
- **默认分支**：`main`

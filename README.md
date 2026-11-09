# point-service

会员积分服务｜承载积分账户、积分明细、积分流水查询等能力。

当前迭代：**积分明细查询 v2**（多条件筛选 + 分页 + 缓存），需求单 `PRD-20431`，技术任务 `AONE-88217`。

## 技术栈

| 层次 | 选型 |
|---|---|
| 语言 / 框架 | Java 17 · Spring Boot 2.7 |
| 架构 | COLA 4.x 分层（adapter / app / domain / infrastructure / client） |
| 持久化 | MySQL 8.0 · MyBatis |
| 缓存 | Tair（Redis 协议） |
| 配置 | Diamond |
| 服务调用 | HSF |
| 构建 | Maven |

## 模块结构

```
point-service
├── point-client          # 对外二方包：DTO / Query / Service 接口 / 异常码
├── point-adapter         # 接入层：Controller、VO、参数校验、异常转换
├── point-app             # 应用层：Exe 编排、事务边界
├── point-domain          # 领域层：实体、值对象、Gateway 接口（禁止依赖 MyBatis / HSF）
└── point-infrastructure  # 基础设施：Mapper、GatewayImpl、缓存、外部调用
```

> 分层红线：`point-domain` 中出现 `org.apache.ibatis` 或 `com.taobao.hsf` 的 import，CR 直接打回。

## 分支规范

| 分支 | 用途 | 说明 |
|---|---|---|
| `main` | 生产分支 | 受保护，只接受 PR 合入，禁止直推 |
| `develop` | 集成分支 | 日常开发的基线，feature 从这里切出 |
| `feature/*` | 功能分支 | 命名 `feature/point_detail_v2`，合入后删除 |
| `hotfix/*` | 紧急修复 | 从 `main` 切出，修完同时回合 `develop` |

## 提交规范

```
<type>: <简述>

type: feat | fix | docs | refactor | test | chore
示例：feat: 积分明细分页查询主链路
```

## 本周任务

任务拆分与验收口径见 [docs/任务清单.md](docs/任务清单.md)，逐条对应 Issues。
详细排期见 [docs/本周工作安排_2026W46_后端开发.pdf](docs/本周工作安排_2026W46_后端开发.pdf)。

## 本地启动

> 由开发侧在首次提交时补充（JDK 版本、Maven 命令、本地配置项、依赖的中间件）。

## 相关文档

- [接口设计：积分明细查询 v2](docs/接口设计-积分明细查询v2.md)
- [协作规范](CONTRIBUTING.md)

## 联系人

| 角色 | 账号 |
|---|---|
| Leader / Reviewer | （leader 账号） |
| 开发 | 508764625 |

# 协作规范

## 1. 分支

- `main`：生产分支，受保护。禁止直接 push，只能通过 Pull Request 合入，且至少 1 人 approve。
- `develop`：集成分支，所有 feature 从这里切出。
- `feature/<模块>_<简述>`：如 `feature/point_detail_v2`。合入 develop 后删除。
- `hotfix/<简述>`：从 main 切出，修完同时回合 develop。

## 2. 提交

```
<type>: <简述>

type 取值：feat | fix | docs | refactor | test | chore
```

要求：

- 一次提交只做一件事，不要把「改格式」和「改逻辑」混在一起；
- 提交信息写清「做了什么」，必要时正文补「为什么」；
- 提交前必须本地编译通过，不允许提交编译不过的代码。

## 3. Pull Request

- 标题格式与 commit 一致，正文按模板写：改动点 / 影响面 / 自测结论 / 风险点；
- 关联对应 Issue，用 `close #12` 自动关闭；
- 单个 PR 改动控制在 400 行以内，超过先拆分；
- 提交前自查（Reviewer 会逐条看）：

| # | 检查项 | 不合格示例 |
|---|---|---|
| 1 | 无魔法值 | `if (bizType == 1)` → 用枚举 |
| 2 | 不吞异常 | `catch (Exception e) {}` 是红线 |
| 3 | 日志可排查 | 带 userId、key、耗时；不打全量对象与敏感字段 |
| 4 | 已防 NPE | 拆箱、Map.get、远程返回都可能为 null |
| 5 | 方法不过长 | 单方法 > 80 行、嵌套 > 3 层需抽方法 |
| 6 | 无调试残留 | System.out、TODO、写死的测试数据 |
| 7 | 事务边界正确 | 查询不开事务；事务内不调 RPC |
| 8 | 向后兼容 | 二方包新增字段是否影响老调用方 |

## 4. Code Review

- 提交后 4 小时内请求 Review，Reviewer 24 小时内回复；
- 意见分三级：`[blocking]` 必须改、`[suggestion]` 建议改、`[nit]` 可选；
- 有分歧时以「线上稳定性」为第一优先级，不以个人偏好为准。

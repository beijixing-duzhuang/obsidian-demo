# favorite - 收藏表

## 表说明

用户收藏商品表，记录用户收藏的商品信息。

## 基本信息

| 属性 | 值 |
|------|-----|
| 表名 | favorite |
| 引擎 | InnoDB |
| 字符集 | utf8mb4 |
| 排序规则 | utf8mb4_unicode_ci |
| 主键 | VARCHAR(32)（V33 后原 INT 自增改为 VARCHAR(32)） |

## 字段列表

| 字段名 | 类型 | 允许空 | 默认值 | 说明 |
|--------|------|--------|--------|------|
| id | VARCHAR(32) | 否 | - | 收藏ID（主键） |
| user_id | VARCHAR(32) | 否 | - | 用户ID（外键；V15 由 INT 改 VARCHAR） |
| product_id | VARCHAR(32) | 否 | - | 商品ID（外键） |
| create_time | DATETIME | 是 | CURRENT_TIMESTAMP | 创建时间 |

## 索引

| 索引名 | 索引字段 | 索引类型 | 说明 |
|--------|----------|----------|------|
| PRIMARY | id | 主键索引 | 主键 |
| uk_user_product | user_id, product_id | 唯一索引 | 用户商品唯一约束 |
| idx_user | user_id | 普通索引 | 用户收藏查询优化 |

## 变更历史

- **V15 (2026-03-12)**: user_id 字段类型由 INT 改为 VARCHAR(32)
- **V33**: id / product_id 由 INT 改为 VARCHAR(32)

> **注意**：本表**没有** `type` 字段，也**没有** `update_time` 字段（实体与 schema 均一致）。

## 关联关系

### 作为从表（引用其他表）

| 主表 | 外键字段 | 关系类型 | 说明 |
|------|----------|----------|------|
| [[wx_users]] | user_id | 多对一 | 收藏属于某个用户 |
| [[product]] | product_id | 多对一 | 收藏的是某个商品 |

## 关系图

```mermaid
erDiagram
    favorite {
        VARCHAR id PK
        VARCHAR user_id FK
        VARCHAR product_id FK
    }
    
    wx_users ||--o{ favorite : "收藏"
    product ||--o{ favorite : "被收藏"
```

## 唯一约束说明

`uk_user_product` 唯一索引确保同一用户对同一商品只能收藏一次。
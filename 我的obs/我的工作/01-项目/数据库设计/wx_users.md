# wx_users - 小程序用户表

## 表说明

微信小程序用户信息表，存储小程序端用户的基本信息和微信相关数据。

## 基本信息

| 属性 | 值 |
|------|-----|
| 表名 | wx_users |
| 引擎 | InnoDB |
| 字符集 | utf8mb4 |
| 排序规则 | utf8mb4_unicode_ci |
| 主键 | VARCHAR(64)（V9 由 INT 自增改为 VARCHAR(64)） |

## 字段列表

| 字段名 | 类型 | 允许空 | 默认值 | 说明 |
|--------|------|--------|--------|------|
| id | VARCHAR(64) | 否 | - | 用户ID（主键） |
| openid | VARCHAR(100) | 否 | - | 微信openid（唯一） |
| union_id | VARCHAR(100) | 是 | NULL | 微信unionid |
| session_key | VARCHAR(100) | 是 | NULL | 会话密钥 |
| nickname | VARCHAR(50) | 是 | NULL | 昵称 |
| avatar | VARCHAR(255) | 是 | NULL | 头像URL |
| phone | VARCHAR(20) | 是 | NULL | 手机号 |
| gender | TINYINT | 是 | 0 | 性别: 0未知 1男 2女 |
| language | VARCHAR(20) | 是 | NULL | 语言（V8 新增） |
| city | VARCHAR(50) | 是 | NULL | 城市（V8 新增） |
| province | VARCHAR(50) | 是 | NULL | 省份（V8 新增） |
| country | VARCHAR(50) | 是 | NULL | 国家（V8 新增） |
| status | TINYINT | 是 | 1 | 状态: 0禁用 1启用 |
| is_operator | TINYINT | 是 | 0 | 是否为操作员: 0否 1是 |
| remove | VARCHAR(10) | 是 | '1' | 删除标记: 0已删除 1未删除（V9 添加 TINYINT，V36 改 VARCHAR） |
| last_login_time | DATETIME | 是 | NULL | 最后登录时间 |
| create_time | DATETIME | 是 | CURRENT_TIMESTAMP | 创建时间 |
| update_time | DATETIME | 是 | CURRENT_TIMESTAMP ON UPDATE | 更新时间 |

## 索引

| 索引名 | 索引字段 | 索引类型 | 说明 |
|--------|----------|----------|------|
| PRIMARY | id | 主键索引 | 主键 |
| uk_openid | openid | 唯一索引 | openid 唯一 |

## 变更历史

- **V6 (2026-03-02)**: 创建小程序用户表
- **V8**: 新增 language / city / province / country 位置字段
- **V9 (2026-03-07)**: id 改为 VARCHAR(64)，新增 remove 字段支持软删除
- **V17 (2026-03-16)**: 新增 is_operator 字段，标识用户是否为操作员
- **V27**: 新增手机号索引
- **V36**: remove 字段统一为 VARCHAR(10)

## 关联关系

### 作为主表（被引用）

| 关联表 | 外键字段 | 关系类型 | 说明 |
|--------|----------|----------|------|
| [[orders]] | user_id | 一对多 | 用户可以创建多个订单 |
| [[cart]] | user_id | 一对多 | 用户可以有多个购物车商品 |
| [[favorite]] | user_id | 一对多 | 用户可以收藏多个商品 |
| [[feedback]] | user_id | 一对多 | 用户可以提交多条反馈 |
| [[tool_rental]] | user_id | 一对多 | 用户可以有多条租赁记录 |
| [[tool_rental_notification]] | user_id | 一对多 | 用户可以收到多条通知 |
| [[tool_review]] | user_id | 一对多 | 用户可以发表多条评价 |
| [[tool_stock_alert_registration]] | user_id | 一对多 | 用户可以进行多次缺货登记 |
| [[wx_grey_list]] | user_id | 一对多 | 用户可以被加入灰名单 |

## 关系图

```mermaid
erDiagram
    wx_users {
        VARCHAR id PK
        VARCHAR openid US
        VARCHAR nickname
        VARCHAR phone
    }
    
    wx_users ||--o{ orders : "下单"
    wx_users ||--o{ cart : "购物车"
    wx_users ||--o{ favorite : "收藏"
    wx_users ||--o{ feedback : "反馈"
    wx_users ||--o{ tool_rental : "租赁"
    wx_users ||--o{ tool_rental_notification : "通知"
    wx_users ||--o{ tool_review : "评价"
    wx_users ||--o{ tool_stock_alert_registration : "缺货登记"
    wx_users ||--o{ wx_grey_list : "灰名单"
```

## 状态说明

| 状态值 | 说明 |
|--------|------|
| 0 | 禁用 |
| 1 | 启用 |

## 删除标记说明

| 值 | 说明 |
|----|------|
| 0 | 已删除 |
| 1 | 未删除 |

## 操作员说明

| 值 | 说明 |
|----|------|
| 0 | 普通用户 |
| 1 | 操作员（具有管理权限） |
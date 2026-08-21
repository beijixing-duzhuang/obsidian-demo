# users - 管理后台用户表

## 表说明

管理后台的用户信息表，用于登录管理后台进行商品、订单等管理操作。

## 基本信息

| 属性 | 值 |
|------|-----|
| 表名 | users |
| 引擎 | InnoDB |
| 字符集 | utf8mb4 |
| 排序规则 | utf8mb4_unicode_ci |
| 主键 | VARCHAR(32)（V33 后原 INT 自增改为 VARCHAR(32)） |

## 字段列表

| 字段名 | 类型 | 允许空 | 默认值 | 说明 |
|--------|------|--------|--------|------|
| id | VARCHAR(32) | 否 | - | 用户ID（主键） |
| username | VARCHAR(50) | 否 | - | 用户名（唯一） |
| password | VARCHAR(255) | 否 | - | 密码（加密存储） |
| nickname | VARCHAR(50) | 是 | NULL | 昵称 |
| phone | VARCHAR(20) | 是 | NULL | 手机号 |
| avatar | VARCHAR(255) | 是 | NULL | 头像URL |
| gender | TINYINT | 是 | 0 | 性别: 0未知 1男 2女 |
| email | VARCHAR(100) | 是 | NULL | 邮箱 |
| status | TINYINT | 是 | 1 | 状态: 0禁用 1启用 |
| create_time | DATETIME | 是 | CURRENT_TIMESTAMP | 创建时间 |
| update_time | DATETIME | 是 | CURRENT_TIMESTAMP ON UPDATE | 更新时间 |

## 索引

| 索引名 | 索引字段 | 索引类型 | 说明 |
|--------|----------|----------|------|
| PRIMARY | id | 主键索引 | 主键 |
| uk_username | username | 唯一索引 | 用户名唯一约束 |

## 关联关系

### 作为主表（被引用）

该表目前没有外键关联关系。

## 状态说明

| 状态值 | 说明 |
|--------|------|
| 0 | 禁用 |
| 1 | 启用 |

## 性别说明

| 值 | 说明 |
|----|------|
| 0 | 未知 |
| 1 | 男 |
| 2 | 女 |
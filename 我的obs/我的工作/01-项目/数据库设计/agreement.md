# agreement - 协议表

## 表说明

协议表，存储租用协议、用户协议、隐私协议等协议内容。

## 基本信息

| 属性 | 值 |
|------|-----|
| 表名 | agreement |
| 引擎 | InnoDB |
| 字符集 | utf8mb4 |
| 排序规则 | utf8mb4_unicode_ci |
| 主键 | VARCHAR(32) |

## 字段列表

| 字段名 | 类型 | 允许空 | 默认值 | 说明 |
|--------|------|--------|--------|------|
| id | VARCHAR(32) | 否 | - | 协议ID（主键） |
| name | VARCHAR(100) | 否 | - | 协议名称 |
| type | VARCHAR(50) | 是 | 'rental' | 协议类型: rental=租用协议 user=用户协议 privacy=隐私协议 |
| content | TEXT | 是 | NULL | 协议内容 |
| status | TINYINT | 是 | 1 | 状态: 0禁用 1启用 |
| sort | INT | 是 | 0 | 排序 |
| create_time | DATETIME | 是 | CURRENT_TIMESTAMP | 创建时间 |
| update_time | DATETIME | 是 | CURRENT_TIMESTAMP ON UPDATE | 更新时间 |

## 索引

| 索引名 | 索引字段 | 索引类型 | 说明 |
|--------|----------|----------|------|
| PRIMARY | id | 主键索引 | 主键 |
| idx_type | type | 普通索引 | 按类型查询协议 |
| idx_status | status | 普通索引 | 按状态查询 |

## 关联关系

该表没有外键关联关系。

## 协议类型说明

| 类型 | 说明 |
|------|------|
| rental | 租用协议 |
| user | 用户协议 |
| privacy | 隐私协议 |

## 状态说明

| 状态值 | 说明 |
|--------|------|
| 0 | 禁用 |
| 1 | 启用 |
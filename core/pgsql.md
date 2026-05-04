# PostgreSQL 5432

## Install

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib -y
```

## Commands

| 命令                                             | 作用说明                         |
| ------------------------------------------------ | -------------------------------- |
| sudo systemctl start postgresql                  | 启动 PostgreSQL 服务             |
| sudo systemctl stop postgresql                   | 关闭 PostgreSQL 服务             |
| sudo -u postgres psql                            | 以 postgres 超级用户进入 psql    |
| CREATE ROLE myuser WITH LOGIN PASSWORD '123456'; | 创建可登录用户（角色）           |
| CREATE DATABASE mydb OWNER myuser;               | 创建数据库并指定所有者           |
| ALTER ROLE myuser WITH SUPERUSER;                | 赋予超级管理员权限（开发环境用） |
| \du                                              | 查看所有角色（用户）             |
| \dt | 查看所有表 |
| \l                                               | 查看所有数据库                   |
| \r                                               | 重置当前输入（清空命令）         |
| \q                                               | 退出 psql                        |
| psql -U myuser -d mydb -h localhost              | 使用指定用户连接数据库           |

## SQL

```bash
# 建表
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT,
    age INT
);

CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    order_number INT
);


# 增
INSERT INTO users(name, age) VALUES ('Tom', 18);

# 查
SELECT * FROM users;

# 改
UPDATE users SET age = 20 WHERE name = 'Tom';

# 删
DELETE FROM users WHERE name = 'Tom';
```

```bash
# 条件查
SELECT * FROM users WHERE age > 18;

# 排序 / 分页
SELECT * FROM users ORDER BY age DESC LIMIT 10 OFFSET 0;

# 聚合
SELECT COUNT(*), AVG(age) FROM users;

# 内联表
SELECT u.name, o.order_number FROM users u JOIN orders o ON u.id = o.user_id;

# 左联表
SELECT u.name, o.order_number FROM users u LEFT JOIN orders o ON u.id = o.user_id;

# 视图
CREATE VIEW user_task AS SELECT u.name, t.task_name FROM users u JOIN tasks t ON t.user_id = u.id;

SELECT * FROM user_task;
```

## Keyword

| 分类        | 关键字        | 作用说明 |
|------------|--------------|----------|
| 查询基础    | SELECT       | 指定要查询的字段 |
|            | FROM         | 指定数据来源表 |
|            | AS           | 设置别名 |
| 条件过滤    | WHERE        | 行级过滤条件 |
|            | AND / OR     | 多条件组合 |
|            | IN           | 在某个集合中 |
|            | BETWEEN      | 范围查询 |
|            | LIKE / ILIKE | 模糊匹配（ILIKE 忽略大小写） |
|            | IS NULL      | 判断为空 |
|            | IS NOT NULL  | 判断非空 |
| 排序分页    | ORDER BY     | 排序 |
|            | ASC / DESC   | 升序 / 降序 |
|            | LIMIT        | 限制返回行数 |
|            | OFFSET       | 偏移量（分页） |
| 聚合统计    | COUNT        | 计数 |
|            | SUM          | 求和 |
|            | AVG          | 平均值 |
|            | MAX / MIN    | 最大 / 最小值 |
| 分组        | GROUP BY     | 分组 |
|            | HAVING       | 分组后过滤 |
| 连接查询    | JOIN         | 内连接 |
|            | INNER JOIN   | 内连接（等价 JOIN） |
|            | LEFT JOIN    | 左连接 |
|            | RIGHT JOIN   | 右连接 |
|            | FULL JOIN    | 全连接 |
|            | ON           | 连接条件 |
| 子查询      | EXISTS       | 判断子查询是否有结果 |
|            | NOT EXISTS   | 子查询无结果 |
|            | ANY / ALL    | 与子查询比较 |
| 去重        | DISTINCT     | 去重 |
| 数据操作    | INSERT INTO  | 插入数据 |
|            | VALUES       | 插入的值 |
|            | UPDATE       | 更新数据 |
|            | SET          | 设置更新字段 |
|            | DELETE       | 删除数据 |
| 表操作      | CREATE TABLE | 创建表 |
|            | DROP TABLE   | 删除表 |
|            | ALTER TABLE  | 修改表结构 |
|            | ADD COLUMN   | 添加字段 |
|            | DROP COLUMN  | 删除字段 |
| 约束        | PRIMARY KEY  | 主键 |
|            | FOREIGN KEY  | 外键 |
|            | UNIQUE       | 唯一约束 |
|            | NOT NULL     | 非空 |
|            | DEFAULT      | 默认值 |
| 视图索引    | CREATE VIEW  | 创建视图 |
|            | CREATE INDEX | 创建索引 |
|            | DROP INDEX   | 删除索引 |
| 事务        | BEGIN        | 开启事务 |
|            | COMMIT       | 提交事务 |
|            | ROLLBACK     | 回滚事务 |
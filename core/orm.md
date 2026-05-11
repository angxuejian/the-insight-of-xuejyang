# ORM

Using SQLAlchemy ORM with Python

## Install
```
pip install sqlalchemy psycopg[binary] alembic
```

<details>
    <summary>Example</summary>

```py
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship
from sqlalchemy import String, Text, Integer, Float, Boolean, Date, DateTime, TIMESTAMP, func, ForeignKey, Enum as SqlEnum, SmallInteger
from datetime import datetime, date
from enum import Enum, IntEnum
from sqlalchemy.dialects.postgresql import UUID as PG_UUID
from uuid import uuid4, UUID

class Base(DeclarativeBase):
    __abstract__ = True

    # TIMESTAMP(timezone=True): sql层
    created_time: Mapped[datetime] = mapped_column(TIMESTAMP(timezone=True), server_default=func.now(), nullable=False, index=True)

    # DateTime(timezone=True): orm层
    updated_time: Mapped[datetime] = mapped_column(DateTime(timezone=True), server_default=func.now(), onupdate=func.now(), nullable=False, index=True)


class Role(str, Enum):
    admin = 'superuser'
    user = 'user'

class Gender(IntEnum):
    male = 0
    female = 1

class User(Base):
    __tablename__ = 'users'

    id: Mapped[UUID] = mapped_column(PG_UUID(as_uuid=True), primary_key=True, default=uuid4, index=True)
    role: Mapped[Role] = mapped_column(SqlEnum(Role, name='role_enum'), nullable=False)
    gender: Mapped[Gender] = mapped_column(SqlEnum(Gender, name='gender_enum'), nullable=False)
    email: Mapped[str] = mapped_column(String(255), unique=True, index=True, nullable=False)
    age: Mapped[int] = mapped_column(Integer, nullable=False)
    is_active: Mapped[bool] = mapped_column(Boolean, default=False, nullable=False)
    address: Mapped[str | None] = mapped_column(String(200))
    introduction: Mapped[str | None] = mapped_column(Text)
    height: Mapped[float | None] = mapped_column(Float)
    weight: Mapped[float | None] = mapped_column(Float)
    birthday: Mapped[date | None] = mapped_column(Date)

    orders_rel: Mapped[list["Order"]] = relationship(back_populates="user_rel", cascade="all, delete-orphan", passive_deletes=True)



class Order(Base):
    __tablename__ = 'orders'

    id: Mapped[int] = mapped_column(primary_key=True)
    user_id: Mapped[UUID] = mapped_column(ForeignKey('users.id', ondelete="CASCADE"))

    user_rel: Mapped["User"] = relationship(back_populates="orders_rel")

```
</details>


## Sqlalchemy


### 1、操作语法

| 命令                                | 作用说明               |
|------------------------------------|------------------------|
| create_engine(url)               | 创建数据库引擎（连接） |
| Session(engine)                  | 创建数据库会话         |
| Base.metadata.create_all(engine) | 根据模型自动创建所有表 |
| db.add(user)                     | 添加单个 ORM 对象      |
| db.add_all(users)                | 批量添加 ORM 对象      |
| db.commit()                      | 提交事务               |
| db.rollback()                    | 回滚事务               |
| db.refresh(user)                 | 刷新对象最新数据       |
| db.delete(user)                  | 删除 ORM 对象          |
| db.get(User, 1)                  | 通过主键查询（推荐）   |
| db.execute(stmt)                 | 执行 SQL Statement     |

### 2. 查询与 Statement 构建

| 命令                          | 作用说明                  |
|------------------------------|---------------------------|
| select(User)               | 构建 SELECT 查询          |
| update(User)               | 构建 UPDATE 语句          |
| delete(User)               | 构建 DELETE 语句          |
| insert(User)               | 构建 INSERT 语句          |
| .where(User.id == 1)       | 添加 WHERE 条件           |
| .where(a, b)               | 多条件（AND）             |
| .order_by(User.id.desc())  | 排序                      |
| .limit(10)                 | 限制返回条数              |
| .offset(20)                | 结果偏移（分页）          |
| .join(Task)                | INNER JOIN                |
| .outerjoin(Task)           | LEFT OUTER JOIN           |
| .group_by(User.id)         | 分组                      |
| .having(func.count() > 1)  | 分组后过滤（HAVING）      |
| .distinct()                | 去重                      |

### 3. 常用过滤条件

| 条件                               | 作用说明                  |
|-----------------------------------|---------------------------|
| User.id.in_([1,2,3])            | IN 查询                   |
| ~User.id.in_([1,2,3])           | NOT IN 查询               |
| User.name.like("%Tom%")         | 模糊匹配（区分大小写）    |
| User.name.ilike("%tom%")        | 模糊匹配（忽略大小写）    |
| User.name.is_(None)             | 判断 IS NULL              |
| User.name.is_not(None)          | 判断 IS NOT NULL          |
| exists().where(...)             | EXISTS 子查询             |

### 4. 聚合函数
| 函数                    | 作用说明 |
|------------------------|----------|
| func.count(User.id)  | COUNT    |
| func.max(User.age)   | MAX      |
| func.min(User.age)   | MIN      |
| func.avg(User.age)   | AVG      |
| func.sum(User.age)   | SUM      |

### 5. Result API（执行结果处理）

| 方法                        | 作用说明                     |
|----------------------------|-----------------------------|
| .all()                   | 返回所有结果（列表）         |
| .first()                 | 返回第一条记录（或 None）    |
| .one()                   | 必须且仅有一条，否则抛异常   |
| .one_or_none()           | 0 或 1 条（多条抛异常）      |
| .scalar()                | 返回单个标量值               |
| .scalar_one()            | 必须返回单个标量值           |
| .scalar_one_or_none()    | 返回单个标量值或 None        |
| .scalars()               | 返回 ORM 对象标量集合        |

## Alembic

| 命令                                       | 作用说明                  |
| ---------------------------------------- | --------------------- |
| alembic init alembic                     | 初始化 Alembic           |
| alembic revision -m "msg"                | 创建空 migration 文件      |
| alembic revision --autogenerate -m "init" | 根据 ORM 自动生成 migration |
| alembic upgrade head                     | 升级到最新版本               |
| alembic upgrade +1                       | 升级一个版本                |
| alembic upgrade <revision>               | 升级到指定版本               |
| alembic downgrade -1                     | 回退一个版本                |
| alembic downgrade base                   | 回退到初始状态               |
| alembic downgrade <revision>             | 回退到指定版本               |
| alembic current                          | 查看当前数据库版本             |
| alembic history                          | 查看 migration 历史       |
| alembic heads                            | 查看最新 revision         |
| alembic branches                         | 查看分支 migration        |
| alembic show <revision>                  | 查看某个 revision 详情      |
| alembic stamp head                       | 仅标记版本，不执行 migration   |
| alembic stamp base                       | 清除版本记录                |

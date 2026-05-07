# ORM

Using SQLAlchemy ORM with Python

```
pip install sqlalchemy psycopg[binary]
```
<!-- alembic -->

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

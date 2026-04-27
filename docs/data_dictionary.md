# 数据字典与数据库设计 (Data Dictionary & Schema)

## 1. 设计原则
- 使用 SQLAlchemy ORM 进行定义。
- 开发阶段使用 SQLite，生产阶段切换为 PostgreSQL。
- 所有表包含 `created_at` 和 `updated_at` 时间戳字段。

## 2. ER 图描述 (Entity-Relationship)
- **Employees** (1) ---- (<N>) **Projects**
  - 一个员工可以负责多个项目。
  - 一个项目只能有一个主要负责人。

## 3. 表结构定义

### 3.1 员工表 (`employees`)
| 字段名 | 类型 | 约束 | 描述 |
| :--- | :--- | :--- | :--- |
| id | Integer | PK, Auto Increment | 主键 |
| name | String(50) | Not Null | 员工姓名 |
| email | String(100) | Unique, Nullable | 工作邮箱（用于登录账号） |
| password_hash | String(255) | Not Null | 密码哈希值 |
| role | String(20) | Default 'employee' | 角色: 'admin', 'employee' |
| created_at | DateTime | Default Now() | 创建时间 |
| updated_at | DateTime | On Update Now() | 更新时间 |

### 3.2 项目表 (`projects`)
| 字段名 | 类型 | 约束 | 描述 |
| :--- | :--- | :--- | :--- |
| id | Integer | PK, Auto Increment | 主键 |
| project_code | String(20) | Unique, Not Null | 项目编号 (如: DEC-2026-001) |
| name | String(200) | Not Null | 项目名称 |
| owner_id | Integer | FK -> employees.id | 负责人ID |
| start_date | Date | Not Null | 项目开始日期 |
| estimated_end_date | Date | Not Null | 预计结束日期 |
| actual_end_date | Date | Nullable | 实际结束日期 |
| client_contact_name | String(50) | Nullable | 甲方对接人姓名 |
| client_phone | String(20) | Nullable | 甲方联系电话 |
| client_email | String(100) | Nullable | 甲方邮箱 |
| status | String(20) | Default 'not_started' | 状态枚举: 'not_started', 'in_progress', 'pending_review', 'completed', 'delayed' |
| description | Text | Nullable | 项目备注 |
| created_at | DateTime | Default Now() | 创建时间 |
| updated_at | DateTime | On Update Now() | 更新时间 |

## 4. 状态枚举定义 (Status Enum)
- `not_started`: 未开始
- `in_progress`: 进行中
- `pending_review`: 待审核
- `completed`: 已完成
- `delayed`: 延期

## 5. JSON Schema 示例 (Project Response)
```json
{
  "id": 1,
  "project_code": "DEC-2026-042",
  "name": "上海中心大厦办公室改造",
  "owner": {
    "id": 3,
    "name": "张三"
  },
  "start_date": "2026-04-01",
  "estimated_end_date": "2026-05-15",
  "actual_end_date": null,
  "client_info": {
    "name": "李四",
    "phone": "13800138000",
    "email": "lisi@example.com"
  },
  "status": "in_progress",
  "created_at": "2026-04-27T10:00:00Z"
}

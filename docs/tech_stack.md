# 技术栈与工程规范 (Tech Stack & Standards)

## 1. 技术选型

### 前端 (Frontend)
- **Core**: Vue 3 (Composition API)
- **Build Tool**: Vite
- **UI Library**: Element Plus
- **State Management**: Pinia (轻量级，替代 Vuex)
- **HTTP Client**: Axios
- **Routing**: Vue Router 4
- **Utils**: Day.js (时间处理), XLSX (前端备用导出，主要靠后端)

### 后端 (Backend)
- **Framework**: FastAPI (Python 3.10+)
- **Server**: Uvicorn (ASGI)
- **ORM**: SQLAlchemy 2.0 (Async support optional, sync for simplicity in MVP)
- **Migration**: Alembic
- **Validation**: Pydantic V2
- **Excel Generation**: OpenPyXL
- **Auth**: JWT (PyJWT), Passlib (bcrypt)

### 数据库 (Database)
- **Dev**: SQLite (`./app.db`)
- **Prod**: PostgreSQL 15+

### 基础设施 (Infra)
- **Containerization**: Docker & Docker Compose

## 2. 目录结构规范

```text
project-root/
├── docs/                   # 项目文档
│   ├── requirements.md
│   ├── data_dictionary.md
│   ├── ui_prototype.md
│   └── tech_stack.md
├── backend/                # 后端代码
│   ├── app/
│   │   ├── api/            # API 路由 (endpoints)
│   │   ├── core/           # 配置、安全依赖
│   │   ├── models/         # SQLAlchemy 模型
│   │   ├── schemas/        # Pydantic 模式 (Request/Response)
│   │   ├── services/       # 业务逻辑 (Excel导出等)
│   │   └── main.py         # 入口文件
│   ├── tests/              # 测试用例
│   ├── requirements.txt    # Python 依赖
│   └── Dockerfile
├── frontend/               # 前端代码
│   ├── src/
│   │   ├── assets/
│   │   ├── components/     # 公共组件
│   │   ├── views/          # 页面视图
│   │   ├── router/         # 路由配置
│   │   ├── stores/         # Pinia Store
│   │   ├── utils/          # 工具函数 (axios实例)
│   │   ├── App.vue
│   │   └── main.js
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   └── Dockerfile
├── docker-compose.yml      # 服务编排
└── README.md

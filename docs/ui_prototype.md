# UI 原型与组件结构建议 (UI Prototype)

## 1. 设计风格
- **框架**: Element Plus (Vue 3)
- **主题**: 简洁商务风，主色调建议使用深蓝色 (#409EFF) 或品牌色。
- **布局**: 经典的 Admin Dashboard 布局（左侧侧边栏导航，顶部面包屑/用户信息，中间内容区）。

## 2. 关键页面线框描述

### 2.1 首页仪表盘 (Dashboard)
- **顶部区域**: 
  - 3-4 个统计卡片 (Stat Cards): [进行中: 12] [待审核: 3] [延期: 1] [本月完成: 5]。
- **中部区域**:
  - 筛选栏: [输入框: 搜索项目名] [下拉框: 选择状态] [下拉框: 选择负责人] [按钮: 查询] [按钮: 重置] [按钮: 导出Excel (右侧对齐)]。
  - 数据表格 (El-Table):
    - 列: 项目编号, 项目名称, 负责人(Tag标签), 预计结束(高亮显示临近日期), 状态(不同颜色Tag), 操作(查看/编辑)。
    - 分页器 (Pagination): 底部居中。

### 2.2 员工详情页 (Employee View)
- **头部**: 
  - 员工头像占位符 + 姓名 + 职位 + “负责项目总数”。
- **Tab 切换栏**:
  - Tab 1: **进行中项目** (默认激活)
    - 复用首页的数据表格组件，但数据源过滤为 `owner_id == current_employee_id` 且 `status != 'completed'`。
  - Tab 2: **历史项目**
    - 数据源过滤为 `owner_id == current_employee_id` 且 `status == 'completed'`。

### 2.3 项目新增/编辑弹窗 (Project Dialog)
- **形式**: 模态对话框 (El-Dialog)，宽度 600px。
- **表单布局 (El-Form)**:
  - **第一行**: 项目编号 (Input, 禁用或自动), 项目名称 (Input, 必填).
  - **第二行**: 负责人 (Select, 远程搜索或下拉), 状态 (Radio Group 或 Select).
  - **第三行**: 开始时间 (DatePicker), 预计结束时间 (DatePicker).
  - **第四行**: 实际结束时间 (DatePicker, 仅当状态选“已完成”时显示/必填).
  - **第五行 (分组标题: 甲方信息)**:
    - 对接人姓名 (Input)
    - 电话 (Input)
    - 邮箱 (Input)
  - **第六行**: 备注 (TextArea, 3行).
- **底部按钮**: [取消] [确认保存].

## 3. 组件复用策略
- `ProjectTable.vue`: 封装通用的项目表格，接收 `data` 和 `actions` props。
- `StatusTag.vue`: 根据状态字符串返回不同颜色的 El-Tag。
- `DateRangeFilter.vue`: 封装时间范围筛选组件。

# project3

# Pj4 — Django 博客/日志项目 📝✨

## 简介
Pj4 是一个基于 Django 的轻量级博客/日志示例项目，包含用户认证、主题管理、日志条目等核心功能。该项目适合作为学习 Django 模型、模板与视图的练习项目，也可作为小型个人博客系统的雏形。

## 功能特性 ✨
- **用户系统**: 注册、登录、注销
- **主题管理**: 创建、编辑、删除主题（topics）
- **日志条目**: 创建、编辑、删除日志条目（entries）
- **权限控制**: 基于所有者的访问权限管理
- **公开/私有设置**: 可设置条目为公开或私有
- **响应式界面**: 基于模板的页面渲染，易于定制

## 项目结构 📁
```
Pj4/
├── manage.py              # Django 项目管理脚本
├── db.sqlite3             # SQLite 数据库文件（开发用）
├── my_project/           # Django 项目配置
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── accounts/             # 用户认证应用
│   ├── templates/        # 注册/登录模板
│   ├── models.py
│   ├── views.py
│   ├── forms.py
│   └── urls.py
├── z_logs/               # 博客核心应用
│   ├── migrations/       # 数据库迁移文件
│   ├── templates/z_logs/ # 主要页面模板
│   ├── models.py
│   ├── views.py
│   ├── forms.py
│   └── urls.py
├── requirements.txt      # 项目依赖（如存在）
└── README.md            # 项目说明文档
```

## 快速开始 ⚙️

### 1. 环境准备
确保已安装 Python 3.8+ 和 pip

### 2. 克隆项目
```bash
git clone <项目地址>
cd Pj4
```

### 3. 创建虚拟环境（推荐）
```bash
# Windows (PowerShell)
python -m venv venv
venv\Scripts\Activate.ps1

# Windows (CMD)
venv\Scripts\activate.bat

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

> **注意**: 如果遇到 PowerShell 执行策略限制，可运行：
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

### 4. 安装依赖
```bash
# 如果有 requirements.txt
pip install -r requirements.txt

# 否则安装 Django
pip install django
```

### 5. 数据库配置
```bash
# 执行数据库迁移
python manage.py makemigrations
python manage.py migrate

# 创建超级用户
python manage.py createsuperuser
```

### 6. 运行开发服务器
```bash
python manage.py runserver
```

### 7. 访问应用
打开浏览器访问：http://127.0.0.1:8000/

## 数据库迁移 🗃️
项目使用 SQLite 作为默认数据库（开发环境）。迁移文件说明：
- `0004_blogpost_owner.py` - 为博客文章添加所有者字段
- `0005_blogpost_is_public.py` - 添加公开/私有标识字段

**生产环境建议**: 使用 PostgreSQL 或 MySQL，并更新 `my_project/settings.py` 中的数据库配置。

## 开发指南 🔧

### 模板位置
- 博客页面模板：`z_logs/templates/z_logs/`
- 用户认证模板：`accounts/templates/registration/`

### 常用命令
```bash
# 运行测试
python manage.py test

# 进入 Django shell
python manage.py shell

# 创建新的迁移文件
python manage.py makemigrations <appname>

# 查看项目 URL 配置
python manage.py show_urls  # 需要安装 django-extensions
```

## 测试策略 ✅
使用 Django 内置的 TestCase 编写单元测试：
```bash
# 运行所有测试
python manage.py test

# 运行特定应用的测试
python manage.py test accounts
python manage.py test z_logs
```

推荐为核心功能编写测试：
- 用户注册和登录
- 主题创建和编辑
- 条目权限控制
- 表单验证

## 部署建议 🚀

### 生产环境配置
1. 修改 `settings.py`：
   - 设置 `DEBUG = False`
   - 配置 `ALLOWED_HOSTS`
   - 更新数据库配置
   - 设置静态文件路径

2. 收集静态文件：
   ```bash
   python manage.py collectstatic
   ```

### 部署选项
- **Linux**: Gunicorn + Nginx
- **PaaS**: Heroku, PythonAnywhere, Railway
- **容器化**: Docker + Docker Compose

## 安全注意事项 ⚠️
1. 移除或加密 `superuser info` 等敏感文件
2. 不要在版本控制中提交：
   - 真实密码
   - API 密钥
   - 数据库凭据
3. 生产环境务必：
   - 使用强密码
   - 启用 HTTPS
   - 定期更新依赖

## 常见问题 💡

### Q: 无法激活虚拟环境
**A**: 
- PowerShell: 检查执行策略，使用 `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`
- CMD: 确保使用 `activate.bat` 而不是 PowerShell 脚本

### Q: 迁移失败
**A**:
```bash
# 尝试删除迁移历史并重新迁移
python manage.py makemigrations --name initial_migration
python manage.py migrate
```

### Q: 页面出现 500 错误
**A**: 
- 查看运行服务器的控制台输出
- 检查 Django 的完整 traceback
- 验证数据库连接和模型定义

## 贡献指南 🤝
1. Fork 本仓库
2. 创建功能分支：`git checkout -b feature/新功能`
3. 提交更改：`git commit -m '添加新功能'`
4. 推送到分支：`git push origin feature/新功能`
5. 提交 Pull Request

### 代码规范
- 使用 [Black](https://black.readthedocs.io/) 格式化代码
- 使用 [Flake8](https://flake8.pycqa.org/) 检查代码风格
- 保持提交信息清晰明确

## 许可证 📜
本项目采用 MIT 许可证。详情请参阅项目根目录下的 LICENSE 文件（如有）。

## 致谢
感谢 Django 官方文档和相关教程提供的灵感和指导。

---

**提示**: 此项目为学习目的而设计，适合 Django 初学者理解和实践 Web 开发基础概念。

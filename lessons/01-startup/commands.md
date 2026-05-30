# Commands

## 安装 FastAPI 标准依赖

```bash
uv add "fastapi[standard]"
```

`fastapi[standard]` 会安装 FastAPI CLI 和常用运行依赖。

## 安装 Uvicorn 标准依赖

```bash
uv add "uvicorn[standard]"
```

`uvicorn[standard]` 会安装性能和开发体验相关的可选依赖，例如更好的 reload 文件监听、WebSocket 支持和更快的协议解析。

## 通过项目启动入口运行

```bash
uv run python main.py
```

## 通过 Uvicorn 命令运行

```bash
uv run uvicorn main:app --host 0.0.0.0 --port 8562 --reload
```

## 临时覆盖环境变量运行

```bash
APP_RELOAD=false APP_PORT=8563 uv run python main.py
```

## 验证配置和应用可以导入

```bash
uv run python -c "from main import app; from config import settings; print(app.title); print(settings.app_host, settings.app_port, settings.app_reload)"
```

# 01 - Startup

本课目标：理解 FastAPI 项目的启动方式，以及如何把启动配置整理到独立模块。

## 当前项目结构

```text
main.py
config.py
lessons/
  01-startup/
    code/
      main.py
      config.py
```

职责划分：

- `main.py`：定义 FastAPI 应用实例、路由，并提供本地启动入口。
- `config.py`：读取 `.env` 和环境变量。
- `lessons/01-startup/code/`：保存第一课结束时的代码快照。

## 推荐启动方式

当前项目第一课阶段使用根目录入口启动：

```bash
uv run python main.py
```

这种方式会读取 `config.py` 中的配置，再调用 `uvicorn.run()`。

## Uvicorn 导入路径

```bash
uv run uvicorn main:app
```

`main:app` 的含义是：

- `main`：Python 模块路径，对应 `main.py`。
- `app`：模块里的 FastAPI 实例变量，对应 `app = FastAPI()`。

如果文件名或实例名变化，启动路径也要跟着变化。

## 环境变量配置

当前配置类：

```python
class Settings(BaseSettings):
    app_host: str = "0.0.0.0"
    app_port: int = 8562
    app_reload: bool = True
```

可以通过 `.env` 或真实环境变量覆盖：

```env
APP_HOST=0.0.0.0
APP_PORT=8562
APP_RELOAD=true
```

生产环境通常使用真实环境变量，不依赖本地 `.env` 文件。

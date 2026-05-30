# 02 - Dev Workflow

本课目标：建立 FastAPI 项目里的基础开发检查流程，包括 Ruff、Mypy 和 Pytest。

## 标准流程

推荐把代码质量工具放进开发依赖：

```bash
uv add --dev ruff mypy pytest
```

本课因为使用了 `fastapi.testclient.TestClient`，还需要安装测试客户端依赖：

```bash
uv add --dev httpx2
```

当前推荐检查顺序：

```bash
uv run ruff check . --fix
uv run ruff format .
uv run mypy .
uv run pytest
```

## 当前项目配置

运行依赖放在 `[project].dependencies`：

```toml
dependencies = [
    "fastapi>=0.136.3",
    "pydantic-settings>=2.14.1",
    "uvicorn[standard]>=0.48.0",
]
```

开发依赖放在 `[dependency-groups].dev`：

```toml
dev = [
    "httpx2>=2.2.0",
    "mypy>=2.1.0",
    "pytest>=9.0.3",
    "ruff>=0.15.15",
]
```

## 课程归档目录排除

`lessons/` 目录保存学习过程代码快照，不应该参与当前项目的 lint、type check 和 test。

原因：

- `mypy .` 会把 `lessons/01-startup/code/config.py` 和根目录 `config.py` 都识别成顶层模块 `config`，导致重复模块错误。
- `pytest` 递归扫描时可能收集课程快照里的 `test_*.py`。
- `ruff --fix` 和 `ruff format` 不应该自动修改课程快照。

因此在 `pyproject.toml` 中排除 `lessons/`：

```toml
[tool.ruff]
exclude = [
    "lessons",
]

[tool.mypy]
exclude = [
    "^lessons/",
]

[tool.pytest.ini_options]
norecursedirs = [
    "lessons",
]
```

## 本课代码快照

代码保存在：

```text
lessons/02-dev-workflow/code/
```

包含：

- `main.py`：当前 FastAPI 应用代码。
- `config.py`：当前 Settings 配置。
- `test_main.py`：当前测试样例。
- `pyproject.toml`：当前依赖和工具配置。

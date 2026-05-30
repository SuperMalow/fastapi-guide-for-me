# Notes

## `--dev` 的含义

`uv add pytest` 会把依赖加入生产依赖：

```toml
[project]
dependencies = [
    "pytest>=9.0.3",
]
```

`uv add --dev pytest` 会把依赖加入开发依赖：

```toml
[dependency-groups]
dev = [
    "pytest>=9.0.3",
]
```

开发依赖适合放：

- `ruff`
- `mypy`
- `pytest`
- `httpx2`

运行依赖适合放：

- `fastapi`
- `pydantic-settings`
- `uvicorn[standard]`

## `TestClient` 报错原因

测试代码：

```python
from fastapi.testclient import TestClient
```

`fastapi.testclient.TestClient` 来自 Starlette。当前 Starlette 版本会优先寻找 `httpx2`，找不到再尝试 `httpx`。

如果两个包都没有，会在 pytest 收集阶段报错：

```text
RuntimeError: The starlette.testclient module requires the httpx2 package to be installed.
```

解决方式：

```bash
uv add --dev httpx2
```

## `pytest` 的收集阶段

这次错误发生在测试收集阶段，还没有真正执行测试函数。

原因是 `test_main.py` 顶部导入了：

```python
from fastapi.testclient import TestClient
```

导入失败会导致 pytest 无法继续收集测试。

## 课程快照不参与检查

`lessons/` 是学习归档，不是当前应用源码。

如果不排除，工具会把课程快照也当成当前项目的一部分：

- `mypy .` 可能出现重复模块。
- `pytest` 可能重复运行旧测试。
- `ruff --fix` 可能修改历史课程代码。

所以课程快照目录要在 `pyproject.toml` 中排除。

## 和 Django 的类比

Django 项目也常见类似分层：

- 生产依赖：`django`、`gunicorn`、数据库驱动。
- 开发依赖：`pytest`、`mypy`、`ruff`、测试客户端扩展。

FastAPI 项目中也是同样原则：能被生产服务直接用到的是运行依赖，只服务开发流程的是开发依赖。

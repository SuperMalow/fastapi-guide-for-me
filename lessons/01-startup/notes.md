# Notes

## `uvicorn` 和 `uvicorn[standard]`

`uvicorn` 是最小安装，只包含核心运行能力。

`uvicorn[standard]` 是带官方推荐可选依赖的安装方式，更适合日常开发和常规生产部署。

`[standard]` 是 Python packaging 的 extras 语法，不是 `uv` 独有能力。

## `fastapi` 和 `fastapi[standard]`

只安装 `fastapi` 时，可以正常写：

```python
from fastapi import FastAPI
```

但不一定能使用：

```bash
fastapi dev main.py
```

FastAPI CLI 需要 `fastapi[standard]`。

## `main:app`

`main:app` 是：

```text
模块路径:ASGI 应用实例变量名
```

例如：

```python
# main.py
app = FastAPI()
```

对应：

```bash
uvicorn main:app
```

当前项目第一课阶段推荐：

```bash
uvicorn main:app
```

## 和 Django 的类比

Django 常见入口是：

```text
project.asgi:application
```

FastAPI 常见入口是：

```text
main:app
```

本质上都是告诉 ASGI 服务器：应用对象在哪里。

## 学习重点

这一课不重点学习路由和请求处理，只先确认三件事：

- 应用实例在哪里。
- 服务由谁启动。
- 配置从哪里读取。

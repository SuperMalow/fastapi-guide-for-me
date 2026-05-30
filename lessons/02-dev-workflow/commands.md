# Commands

## 安装开发依赖

```bash
uv add --dev ruff mypy pytest
```

## 安装 FastAPI TestClient 依赖

```bash
uv add --dev httpx2
```

## 自动修复 Ruff lint 问题

```bash
uv run ruff check . --fix
```

## 格式化代码

```bash
uv run ruff format .
```

## 类型检查

```bash
uv run mypy .
```

## 运行测试

```bash
uv run pytest
```

## 只读验证命令

归档前可以使用不改文件的版本：

```bash
uv run ruff check .
uv run ruff format --check .
uv run mypy .
uv run pytest
```

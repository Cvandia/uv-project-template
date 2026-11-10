# uv-project-template

使用 [uv](https://docs.astral.sh/uv/) 管理依赖、虚拟环境、构建和发布的 Python 项目模板，支持 Python 3.10 及以上版本。

## 开始使用

1. 在 GitHub 点击 **Use this template** 创建自己的仓库，或克隆本仓库：

   ```bash
   git clone https://github.com/Cvandia/uv-project-template.git
   cd uv-project-template
   ```

2. 按照 [官方文档](https://docs.astral.sh/uv/getting-started/installation/) 安装 uv，然后安装项目和开发依赖：

   ```bash
   uv sync --locked
   uv run pre-commit install
   ```

3. 修改 `pyproject.toml` 中的项目名称、描述、作者和版本，并将 `src/uv_project_template` 重命名为自己的 Python 包名（使用下划线）。同步修改测试导入和 README 中的仓库链接，然后执行 `uv lock` 更新锁文件。

## 常用命令

```bash
# 添加运行依赖 / 开发依赖
uv add httpx
uv add --dev pytest-cov

# 同步依赖并执行代码
uv sync --locked
uv run python -c "import uv_project_template"

# 代码检查、格式化和测试
uv run ruff check .
uv run ruff format .
uv run pytest
uv run pre-commit run --all-files

# 更新依赖（提交更新后的 uv.lock）
uv lock --upgrade

# 构建 wheel 和源码包，产物位于 dist/
uv build
```

`uv.lock` 应提交到版本控制；`.venv/` 和构建产物不提交。CI 使用 `uv sync --locked`，确保依赖声明和锁文件一致。

## 项目结构

```text
src/uv_project_template/    Python 包
tests/                     pytest 测试
pyproject.toml             项目元数据、依赖和 uv 构建后端
uv.lock                    依赖锁文件
.ruff.toml                 Ruff 规则
.pre-commit-config.yaml    提交前检查
.github/workflows/         检查、构建、发布与发布说明草稿
```

## 发布

先设置自己的包名和版本，并在仓库的 Actions secrets 中添加 `PYPI_API_TOKEN`。推送 `v*` 标签会通过 `uv build` 和 `uv publish` 发布到 PyPI；标签版本应与 `pyproject.toml` 中的版本一致。

```bash
git tag v0.1.0
git push origin v0.1.0
```

也可以在本地构建后运行 `uv publish`，按提示提供 PyPI 凭据。

## 许可证与来源

[MIT](LICENSE)。本模板改编自 [Cvandia/pdm-project-template](https://github.com/Cvandia/pdm-project-template)。

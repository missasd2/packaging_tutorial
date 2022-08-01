
# 说明
本仓库为测试打包分发 python项目之用 </br>
参考文档为：https://docs.python.org/3/tutorial/modules.html#packages



# 0 prequirements

This is a simple example package. You can use
[Github-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.


```python
py -m pip install --upgrade pip
```

# 1 创建目录及文件

```
packaging_tutorial/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── example_package_YOUR_USERNAME_HERE/
│       ├── __init__.py
│       └── example.py
└── tests/
```

文件说明：
- LICENSE: 许可文件
- pyproject.toml: 告知前端编译工具如pip，使用何种后端编译工具（如setuptools） ，以创建distribution packages。
- README.md 
- src: 代码目录
- example_package_YOUR_USERNAME_HERE：为project名称需独一无二
- tests：测试文件目录

# 2 创建pyproject.toml

```
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
[project]
name = "example_package_YOUR_USERNAME_HERE"
version = "0.0.1"
authors = [
  { name="Example Author", email="author@example.com" },
]
description = "A small example package"
readme = "README.md"
license = { file="LICENSE" }
requires-python = ">=3.7"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
"Homepage" = "https://github.com/pypa/sampleproject"
"Bug Tracker" = "https://github.com/pypa/sampleproject/issues"
```

requires：该列表表明 编译本package所需要的其他package；无需手动安装，pip在安装你的包时会自动安装requires列表中涉及到的包；

build-backend：表明前端编译将使用的pyhton对象；

## 2.2 配置metadata
name：表明该package的名称，需独一无二
version：表明package的版本，参看https://packaging.python.org/en/latest/specifications/version-specifiers/#version-specifiers
authors：作者名
description：描述
readme：指明README.md文件所在的路径
license：项目许可文件所在路径
requires-python：表明该项目所支持的python版本
classifiers：给出本packge的索引分类信息；可参看https://pypi.org/classifiers/
urls：列出的额外的链接

其他项目的metadata信息可参看：https://pypi.org/classifiers/



# 3 创建README.md

```markdown
# Example Package

This is a simple example package. You can use
[Github-flavored Markdown](https://guides.github.com/features/mastering-markdown/)
to write your content.
```

# 4 创建LICENSE文件

LICENSE的许可可参看：https://choosealicense.com/
以下是MIT许可
```LICENSE
Copyright (c) 2018 The Python Packaging Authority

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

# 创建distribuition archives

```bash
py -m pip install --upgrade build
py -m build
```

结果在项目中会生成 **dist** 目录

目录中文件为
dist/
├── example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
└── example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz

```
其中 .whl 文件为二进制文件

# 5 上传distribuition archives
上传至测试环境TestPyPI

1 注册账户 https://test.pypi.org/account/register/
2 创建 PyPI API token
- 进入https://test.pypi.org/manage/account/#api-tokens，创建token
- setting the “Scope” to “Entire account”
- 复制token值

3 上传distribuition

```
py -m pip install --upgrade twine
用户名输入：__token__
密码输入： token值 
```

# 6 验证
可进入https://test.pypi.org/project/example_package_YOUR_USERNAME_HERE.查看

# 7 安装已分发的包
创建virtualvenv虚拟环境

```shell
# --index-url: 添加该选项避免从已有的PyPI中下载包
# --no-deps：避免下载其他不必要的依赖包
py -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-package-YOUR-USERNAME-HERE

```


```shell
py
```


```python
from example_package_YOUR_USERNAME_HERE import example
example.add_one(2)
```



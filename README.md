# data-sience101

> 从零开始的机器学习入门 notebook 合集：用 NumPy、Matplotlib、seaborn 和 scikit-learn 一步步跑通经典算法。
> Hands-on scikit-learn starter notebooks — clustering, dimensionality reduction, regression, ensembles and model validation, explained step by step with plots.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
![Notebooks](https://img.shields.io/badge/notebooks-8-orange)
![Python](https://img.shields.io/badge/python-2.7%20(legacy)-blue)

---

## 这个仓库是什么

一份**面向初学者的动手教程**：每个 notebook 只讲一个算法，从数学直觉 → 代码 → 图 → 结论，适合刚接触 Jupyter、想先把 scikit-learn 的常用 API 跑一遍的人。

原始 notebook 改编自 Jake VanderPlas 的 [PyCon 2015 scikit-learn tutorial](https://github.com/jakevdp/sklearn_pycon2015)（配合《Python Data Science Handbook》），本仓库做了整理、补注与中文导读。

## 内容一览

| Notebook | 主题 | 涉及算法 / 要点 | 数据 |
| --- | --- | --- | --- |
| [`scikit-learn-intro`](./scikit-learn-intro.ipynb) | 机器学习入门 | 什么是机器学习、estimator API（fit/predict）、KNN 分类 | Iris |
| [`scikit-learn-linear-reg`](./scikit-learn-linear-reg.ipynb) | 线性回归 | 最小二乘、一维/多维拟合、损失函数 | 合成数据 |
| [`scikit-learn-validation`](./scikit-learn-validation.ipynb) | 验证与模型选择 | 验证集、K 折交叉验证、欠拟合/过拟合、偏差-方差权衡、验证曲线、学习曲线、Pipeline | Digits |
| [`scikit-learn-pca`](./scikit-learn-pca.ipynb) | 降维 | PCA 原理、主成分、特征脸式的可视化解释 | Iris |
| [`scikit-learn-k-means`](./scikit-learn-k-means.ipynb) | 聚类 | K-Means、EM 视角、K-Means 的坑（球形簇假设、初始化敏感） | Iris / make_blobs |
| [`scikit-learn-gmm`](./scikit-learn-gmm.ipynb) | 密度估计 | 高斯混合模型、如何选高斯个数、GMM 做离群点检测、与 KDE 等估计器对比 | 合成数据 |
| [`scikit-learn-random-forest`](./scikit-learn-random-forest.ipynb) | 集成学习 | 决策树、决策树过拟合、随机森林分类/回归、随机森林的局限 | 合成数据 |
| [`scikit-learn-svm`](./scikit-learn-svm.ipynb) | 支持向量机 | 最大间隔、软间隔、核技巧（linear / RBF / polynomial） | make_circles |

**推荐阅读顺序**：`intro` → `linear-reg` → `validation` → `pca` → `k-means` → `gmm` → `random-forest` → `svm`

## 快速开始

### 1. 安装 Miniconda（强烈推荐）

Miniconda 自带 conda 与 Jupyter，不需要手动折腾环境：
<https://docs.conda.io/en/latest/miniconda.html>

### 2. 启动 Notebook

```bash
git clone https://github.com/lcz007-ai/data-sience101.git
cd data-sience101
jupyter notebook        # 或 jupyter lab
```

然后逐个打开 `.ipynb` 文件，用 `Shift+Enter` 从上往下执行。

### 3. 依赖（实际用到的库）

一键安装：

```bash
pip install -r requirements.txt          # Python 3 现代环境（推荐）
# 或者（Miniconda 用户）
conda env create -f environment.yml && conda activate ds101
```

8 个 notebook 真正 `import` 的第三方库只有下面这几个（**没有用到 pandas**）：

| 库 | 用在哪 | 用途 |
| --- | --- | --- |
| `numpy` | 8/8 | 数组与向量化运算 |
| `matplotlib`（`pyplot` / `pylab` / `mpl_toolkits.mplot3d`） | 8/8 | 绘图、`%matplotlib inline`；SVM 的 3D 决策面 |
| `seaborn` | 8/8 | 绘图样式（`sns.set()`） |
| `scikit-learn` | 8/8 | 算法本体 |
| `scipy.stats` | gmm、intro、k-means、random-forest、svm | 分布拟合等统计辅助 |
| `ipywidgets`（原文写作 `IPython.html.widgets`） | random-forest、svm、validation | 交互式参数滑块（`intro` 另用到 `IPython.display.Image`） |
| `fig_code`（**本仓库缺失**的教程辅助模块） | intro、k-means、random-forest | 绘图与交互辅助函数，处理办法见下方「已知问题」 |

用到的 scikit-learn 子模块：`linear_model`、`neighbors`（KNN / KernelDensity）、`cluster`（KMeans）、`mixture`（GMM）、`decomposition`（PCA）、`tree`、`ensemble`、`svm`、`datasets`、`metrics`、`pipeline`、`preprocessing`、`cross_validation` / `learning_curve`。

| 依赖文件 | 说明 |
| --- | --- |
| [`requirements.txt`](./requirements.txt) | **推荐**：Python 3 现代环境，配合下方导入修改表使用 |
| [`environment.yml`](./environment.yml) | 上者的 conda 版本（Miniconda 用户） |
| [`requirements-legacy-py27.txt`](./requirements-legacy-py27.txt) | Python 2.7 原样运行（不改代码），含版本锁定理由 |

## ⚠️ 已知问题（务必先读）

这些 notebook 写于 2015 年前后，跑在 **Python 2.7 + scikit-learn 0.16/0.17** 上。直接在 Python 3 + 新版 scikit-learn 下运行会报 `ImportError`，按下面这张表改导入即可：

| 旧写法（notebook 现状） | 新写法（Python 3 / sklearn ≥ 0.22） |
| --- | --- |
| `from sklearn.cross_validation import train_test_split, KFold` | `from sklearn.model_selection import train_test_split, KFold` |
| `from sklearn.learning_curve import validation_curve, learning_curve` | `from sklearn.model_selection import validation_curve, learning_curve` |
| `from sklearn.datasets.samples_generator import make_blobs, make_circles` | `from sklearn.datasets import make_blobs, make_circles` |
| `from IPython.html.widgets import interact` | `from ipywidgets import interact` |
| `from fig_code import plot_...` | 见下条 |

- **缺少 `fig_code` 模块**：`intro`、`k-means`、`random-forest` 三个 notebook 依赖原教程仓库的绘图辅助模块 `fig_code.py`，本仓库未收录。请从 [jakevdp/sklearn_pycon2015](https://github.com/jakevdp/sklearn_pycon2015) 复制该文件到本目录，或把 `fig_code.plot_xxx(...)` 调用替换成普通 `matplotlib` 绘图。
- **输出与图片**：notebook 里已保存了执行结果，不想配环境时可直接在 GitHub 上阅读，或配合 <https://nbviewer.org> 查看。
- **仓库名拼写**：`data-sience` 应为 `data-science`（历史遗留）。改名后 GitHub 会自动重定向旧地址，但建议改名前先确认没有外部引用。

## 目录结构

```
data-sience101/
├── LICENSE                      # MIT
├── README.md
├── requirements.txt             # Python 3 现代依赖
├── requirements-legacy-py27.txt # Python 2.7 原样运行依赖
├── environment.yml              # conda 环境（Miniconda）
├── __init__.py
├── scikit-learn-intro.ipynb
├── scikit-learn-linear-reg.ipynb
├── scikit-learn-validation.ipynb
├── scikit-learn-pca.ipynb
├── scikit-learn-k-means.ipynb
├── scikit-learn-gmm.ipynb
├── scikit-learn-random-forest.ipynb
└── scikit-learn-svm.ipynb
```

## 进阶学习资源

- 理论：《机器学习》西瓜书的公式推导详解 —— [南瓜书 PumpkinBook](https://github.com/lcz007-ai/pumpkin-book)
- 代码：《机器学习》配套 toy code —— [datawhalechina/machine-learning-toy-code](https://github.com/datawhalechina/machine-learning-toy-code)
- 系统教材（英文，本仓库 notebook 的源头）—— [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)
- 深度学习入门 —— [《动手学深度学习》d2l-zh](https://github.com/d2l-ai/d2l-zh)

## 贡献

欢迎提 Issue / PR：修 bug、把 notebook 迁移到 Python 3、补中文注释、加新算法均可。提交前请确认 notebook 已从头到尾重新执行（Restart & Run All），避免留下失效的输出。

## License

[MIT](./LICENSE) © 2023 lichaozhao。原始教学 notebook 版权归 [Jake VanderPlas](https://github.com/jakevdp) 所有（[sklearn_pycon2015](https://github.com/jakevdp/sklearn_pycon2015)）。

---

## English Summary

Eight beginner-friendly scikit-learn notebooks, ported and reorganized from Jake VanderPlas' PyCon 2015 tutorial: **intro / linear regression / validation & model selection / PCA / K-Means / Gaussian Mixture Models / Random Forest / SVM**.

```bash
git clone https://github.com/lcz007-ai/data-sience101.git
cd data-sience101
pip install -r requirements.txt   # 或 conda env create -f environment.yml
jupyter lab
```

Dependencies used: `numpy`, `scipy`, `matplotlib`, `seaborn`, `scikit-learn`, `jupyterlab`, `ipywidgets` — plus the missing `fig_code` helper from the upstream tutorial (no `pandas`).

The notebooks were written for Python 2.7 and scikit-learn ~0.17, so on a modern stack you must update the deprecated imports (`sklearn.cross_validation` → `sklearn.model_selection`, `sklearn.datasets.samples_generator` → `sklearn.datasets`, `IPython.html.widgets` → `ipywidgets`) and grab the missing `fig_code.py` from the upstream tutorial. See [已知问题](#-已知问题务必先读) for the full mapping table. Saved outputs are included, so the notebooks can also be read directly on GitHub. MIT licensed.

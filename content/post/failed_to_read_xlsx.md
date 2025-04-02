+++
title = "pthon | 使用 xlrd 读取 .xlsx 文件失败"
author = "lyt"
date = "2021-03-31"
description = "failed to read .xlsx"
tags = [
    "python",
    "错误解决",
]
+++
​
你已在群集上安装 xlrd，并且在尝试读取 Excel .xlsx 格式的文件时遇到错误。如图。
![name](/images/pythonxlsximg.png)


错误提示：
```bash
XLRDError: Excel xlsx file; not supported
```

原因：

xlrd 2.0.0 及更高版本只能读取 .xls 文件。

由于潜在的安全漏洞，已从 `xlrd` 中删除对 .xlsx 文件的支持。


解决方案：

使用 `openpyxl` 而不是 `xlrd` 打开 .xlsx 文件。

```python
在使用 pandas 读取 .xlsx 文件时指定 openpyxl
import pandas as pd
contents = pd.read_excel(`<name-of-file>.xlsx`, engine=`openpyxl`)
```




​
# 插件商店 - .ltc文件格式规范

## 文件结构
.ltc文件是一个纯文本文件，使用UTF-8编码，包含以下部分：

```
[metadata]
name = 插件名称
author = 作者
version = 版本号
description = 插件描述
category = 分类
import = 库名（例如tkinter、PyQt5.QtWidgets等）

[code]
# 这里是插件的控件
# 示例：
```
<button>="示例插件"//在侧边栏创建一个按钮，名字是“示例插件”

<code>{
    from PyQt5.QtWidgets import QPushButton, QMessageBox
    
    def main():
        """插件入口函数
        Plugin entry function
        """
        # 创建按钮
        btn = QPushButton("点击我")
        btn.setToolTip("这是一个示例插件按钮")
        
        # 定义按钮点击事件
        def on_click():
            QMessageBox.information(None, "提示", "您点击了示例插件按钮")
            
        # 绑定点击事件
        btn.clicked.connect(on_click)
        
        # 返回按钮控件
        return btn
}


```

## 字段说明
1. `[metadata]` 部分包含插件的基本信息
   - `name`: 插件名称(必填)
   - `author`: 作者(可选)
   - `version`: 版本号(必填，格式: x.y.z)
   - `description`: 插件描述(必填)
   - `category`: 分类(必填)
   - `import`: 库名(必填)

2. `[code]` 部分包含插件的主要功能代码
   - 必须包含一个`main()`函数作为插件入口
   - 可以使用PyQt5创建UI界面
   - 可以使用标准库和项目已安装的第三方库

## 示例文件
```
[metadata]
name = 文本编辑器
author = Trae AI
version = 1.0.0
description = 一个简单的文本编辑工具
category = 工具

[code]
from PyQt5.QtWidgets import (QTextEdit, QVBoxLayout, QWidget, 
    QPushButton, QMessageBox, QApplication)

def main():
    """插件入口函数
    Plugin entry function
    """
    import sys
    app = QApplication.instance() or QApplication(sys.argv)
    editor = QTextEdit()
    editor.setWindowTitle("文本编辑器")
    editor.show()
    
    # 如果是新创建的QApplication实例，则启动事件循环
    if not QApplication.instance():
        sys.exit(app.exec_())
    return editor
```
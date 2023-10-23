- Suma128974*

## 不熟悉的命令

- s 删除单个字符并进入insert
- S 删除光标前的所有字符并进入insert2
- gd + ctrl o 查看引用位置并返回
- m 大写 / m 小写 多文件 & 单文件操作
- ’ 跳转
- ctrl + i / ctrl + o
- vim surround
  - c s " }  把双引号换为大括号
  - ⭐y s () () 添加
  - ⭐d s () () 删除
  - (可视化下) S
- 替换字符

  - %s/原字符/替换字符/模式(g, c)
  - $s/原字符/替换字符/模式
  - 数字, 数字/ 原字符/ 替换字符/ 模式
- 多选

  - gb
- 悬浮显示

  - ⭐gh 显示错误
- 大小写切换

  - normal
    - gu 小写
    - gU  大写
  - 可视化
    - u
    - U
- 窗口切换

  - vim
    - 新建
      - C-w v
      - C-w s
    - 关闭
      - C-w c
- 处理语句块

  - vaI / vai / vii

  - 删除函数 daI (在函数体内)

  - python中

    - vii

    - vai
- 宏

  - 开始录制 q + 寄存器存储名
  - 结束录制 q
  - 查看宏 :reg 寄存器名
  - 使用 @ 寄存器名
  - 调用最后一次使用的宏 @@
  - 重复执行    数字+使用
  - 修改
    - 追加 q+寄存器名
    - 取出 “ap / :put xxx
    - 修改 “ayy / *ayw
- 调用vscode

  - <Leader>f 格式化
  - <Leader> r 重命名
  - <Leader>[ 折叠
- 浏览器下H / L
- 快速修复 control .
- 跳转定义
- win + e 资源管理器


## 不熟悉的通用命令

- ; 下一个
- , 上一个

## 查找

单行查找

- ；     ，

  - 分号重复查找，逗号返回上一个查找
- 定位到查找之前的字符
  - t
  - T

全局查找

- /   ?
  - 向后 向前
- n   N
  - 下一个  上一个
- # 
  - 跳转相同单词
- *
  - 跳转相同单词

---

## 9

通过配置vim.sneak来替换s键功能：双字符查找，s向下，S向上

通过vim.normalModeBindingsNonRecursive配置映射：

- f => s(f变为vim.sneak触发键)  
- s => cl (同等效果替代)

---


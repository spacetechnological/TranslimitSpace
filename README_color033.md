# color033 - 终端24位ANSI色彩渲染库

> **让不会写代码的人，也能做出漂亮的终端配色。**

[![Python](https://img.shields.io/badge/Python-3.7+-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 📦 安装

```bash
pip install color033
```

---

## ⚡ 快速上手

```python
import color033 as c

# 直接用！会Python就会用
print(c.RED + "红色文字" + c.RESET)
print(c.GREEN + "绿色文字" + c.RESET)
print(c.COFFEE + "咖啡色，自带生活感" + c.RESET)

# input也能用
name = input(c.CYAN + "请输入你的名字：" + c.RESET)

# 支持f-string
print(f"{c.BLUE}姓名：{c.RESET}{name}")
```

---

## 🎯 为什么选 color033？

### 与 Rich 的核心差异

| 维度 | color033 | Rich |
|------|----------|------|
| **原生 print() 兼容** | ✅ 直接塞，会Python就会用 | ❌ 必须用 `console.print()` |
| **原生 input() 兼容** | ✅ 直接塞 | ❌ 必须用 `console.input()` |
| **颜色数量（开箱即用）** | **59 种基础色** | ~16 种 |
| **棕色系** | **11 种**（COFFEE, CARAMEL, WHEAT...） | 1 种 |
| **颜色预览** | ✅ `new_info()` 一行预览，带十六进制 | ❌ 自己写 |
| **颜色回收站** | ✅ `recycle()` 误删可恢复 | ❌ 删了就没了 |
| **颜色锁定** | ✅ `f_color()` / `f_lock()` 防误改 | ❌ 没有 |
| **虚拟环境** | ✅ `env` 配色隔离，可导出导入 | ❌ 没有 |
| **常用色字典** | ✅ `_often` 高频配色速查 | ❌ 自己维护 |
| **二维色彩表格** | ✅ 坐标存取，可读可写 | ❌ 只能渲染 |
| **256色渐变** | ✅ `fg_256()` 原生支持 | ❌ 不支持 |
| **随机配色** | ✅ 配合 `random` 无限生成 | ❌ 只有预设标签 |
| **学习成本** | 极低（会Python就会用） | 高（要学新语法） |
| **依赖体积** | 轻量 | ~20MB |

---

## 🔥 独有功能一览

### 1. 原生 `print()` / `input()` 无缝兼容

color033 的每个颜色都是**普通 Python 字符串**（ANSI 转义序列），可以放进任何接受字符串的地方：

```python
print(c.RED + "危险" + c.RESET)
input(c.GREEN + "输入：" + c.RESET)
sys.stdout.write(c.BLUE + "日志" + c.RESET)
logging.info(f"{c.YELLOW}警告{c.RESET}")
```

**Rich 做得到吗？做不到。**

---

### 2. 颜色回收站（`recycle`）

误删配色？从回收站捞回来！

```python
# 删除并备份
c.recycle(("my_color", c.RED), rec="default_rec")

# 查看回收站
c.recyls("default_rec")

# 恢复
c.recycle(("my_color", c.RED), oper=False, rec="default_rec")
```

支持 **覆盖/不覆盖** 模式，同名颜色可存为列表保留历史版本。

---

### 3. 颜色锁定（`f_color` / `f_lock`）

核心配色锁住，谁都改不了：

```python
c.hex_rgb("FF", "00", "00", "my_red")
c.f_color("my_red")              # 只读锁
c.del_color("my_red")            # 报错！禁止删除
c.r_color("my_red")              # 报错！禁止重置
```

**密钥锁（带注释、带预览）：**

```python
c.f_lock("my_red", lock=True, act="123")
c.f_info("my_red", "主色调", "用于错误提示")
c.f_read("my_red")               # 查看锁状态 + 注释 + 预览
c.f_lock("my_red", lock=False, act="123")  # 解锁
```

**忘记密钥？直接查字典：`c._key_lock_color["my_red"]["key"]`** ——你永远不会被自己的锁锁住。

---

### 4. 虚拟环境（`env`）

多套配色隔离，互不干扰：

```python
c.env_color("work", ("primary", c.BLUE), ("danger", c.RED))
c.env_color("play", ("primary", c.PINK), ("danger", c.ORANGE))

# 使用
print(c.envs().work.primary + "工作模式" + c.RESET)
print(c.envs().play.primary + "娱乐模式" + c.RESET)
```

**导出 / 导入（团队协作神器）：**

```python
c.env_save("work", "./work_theme.json")      # 导出
c.env_open("work_backup", "./work_theme.json") # 导入
```

**设计师也能调色**：改 JSON 文件就行，不需要写代码。

---

### 5. 高频常用色（`_often`）

最常用的颜色存起来，随取随用：

```python
c.often_color("primary", "#FF0000")
c.often_color("bg", "#000000")

print(c._often["primary"] + "重要文本" + c.RESET)
```

**Rich 永远做不到**——它没有“存储”的概念。

---

### 6. 二维色彩表格（`color_table`）

像 Excel 一样存颜色，按坐标取值：

```python
c.color_addt("my_palette")                  # 建表
c.color_addc("my_palette", 0, 0, c.RED)     # 在 (0,0) 存红
c.color_addc("my_palette", 0, 1, c.BLUE)    # 在 (0,1) 存蓝

my_red = c.color_table("my_palette", 0, 0)  # 取红
my_blue = c.color_table("my_palette", 0, 1) # 取蓝

c.colort_all("my_palette")                  # 查看整张表
```

**支持跳着存**——不强制连续，空着就空着，取空坐标会报 KeyError（不是 bug，是告诉你“这里没东西”）。

**无限扩展**——想存多少存多少，一张表不够就开第二张。

---

### 7. 颜色预览（`new_info` / `classic_info`）

想看颜色长什么样？一行搞定：

```python
c.new_info(c.COFFEE)   # 输出：#A84628 + 生活化文案 + 预览文本
c.classic_info(c.RED)  # 输出：#FF0000 + 狐狸句
```

**不用写 `print()`，不用建 `console`，直接看。**

---

### 8. 临时颜色（`TEMP`）

会话级临时色，反复使用，不想用就清掉：

```python
c.temp_color(255, 128, 0, "fg")  # 存橙色临时色
print(c.TEMP + "橙色文字" + c.RESET)
print(c.TEMP + "还是橙色" + c.RESET)
c.reset_temp()                    # 清空
```

**Rich 没有“临时色”这个概念，每次都要重新写标签。**

---

### 9. 256色渐变

```python
for i in range(16, 232):
    print(f"{c.fg_256(i)}█{c.RESET}", end="")
print()  # 彩虹渐变
```

**Rich 不支持 256 色索引，无法实现这种原生渐变。**

---

### 10. 随机配色

```python
import random
r, g, b = random.randint(0, 255), random.randint(0, 255), random.randint(0, 255)
print(f"{c.fg_rgb(r, g, b)}随机颜色{c.RESET}")
```

---

## 🎨 配色体系

| 层级 | 用户类型 | 功能 | 用途 |
|------|---------|------|------|
| 第一层 | 路人 | 12fg + 12bg | 日常够用，不费脑子 |
| 第二层 | 装饰者 | 24fg + 12bg + `_often` | 让终端好看，有格调 |
| 第三层 | 画家 | 59fg + 30bg + 函数 | 自由创作，不受限制 |

**59 种基础色（不含背景），开箱即用：**

- ANSI 基础 8 色 + 高亮 8 色
- 24 位真彩色 12 种（ORANGE、PINK、SKY_BLUE、PURPLE_DARK、VIOLET...）
- **棕色系 11 种**（COFFEE、CARAMEL、WHEAT、TAUPE、BROWN_DARK...）
- 代码色 8 种（CODE_KEYWORD、CODE_STRING...）
- 日志色 10 种（LOG_SUCCESS、LOG_ERROR...）
- 终端色 5 种

---

## 🛠️ 使用场景

### 场景1：日志输出（自带生活化文案）
```python
print(c.LOG_SUCCESS + "✅ 任务完成" + c.RESET)
print(c.LOG_ERROR + "❌ 出错了" + c.RESET)
print(c.LOG_WARN + "⚠️ 注意" + c.RESET)
```

### 场景2：代码高亮（code全套配色）
```python
print(c.CODE_KEYWORD + "def " + c.CODE_FUNCTION + "my_func" + c.CODE_OPERATOR + "():" + c.RESET)
```

### 场景3：制作彩虹文本
```python
colors = [c.RED, c.ORANGE, c.YELLOW, c.GREEN, c.BLUE, c.PURPLE_DARK]
for i, ch in enumerate("Hello World!"):
    print(colors[i % len(colors)] + ch + c.RESET, end="")
print()
```

### 场景4：团队协作统一配色
```python
# 成员A：导出
c.env_save("team_theme", "./team_theme.json")  # 提交到Git

# 成员B：导入
c.env_open("team_theme", "./team_theme.json")  # 配色完全一致
```

### 场景5：手动画彩色表格
```python
data = [["姓名", "年龄"], ["张三", "25"], ["李四", "30"]]
widths = [max(len(str(row[i])) for row in data) for i in range(len(data[0]))]

for row in data:
    for i, cell in enumerate(row):
        print(f"| {c.CYAN}{cell:<{widths[i]}}{c.RESET} ", end="")
    print("|")
```
**每一个边框、每一个文字都可以独立上色。**

---

## ⚠️ 使用建议

| 操作 | 推荐 | 说明 |
|------|------|------|
| 不确定是否需要 | `recycle` | 进回收站，随时可恢复 |
| 确定不需要了 | `del_color` | 最终删除，干净利落 |
| 团队协作 | 先用 `recycle`，确认无误再清空 | 避免误删 |
| 配色存储 | `env` | 有导出导入，适合长期保存 |
| 高频配色 | `_often` | 速查表，随取随用 |
| 网格收纳 | `color_table` | 按坐标存取，适合批量配色 |
| 临时配色 | `TEMP` | 会话级，用完即焚 |
| 忘记密钥 | `c._key_lock_color["my_color"]["key"]` | 直接查字典 |

**`recycle` 是安全网，不是储物间——定期清空，不要堆太多。真正要存的配色，请用 `env`。**

---

## 🔬 与 Rich 的深度对比

| 对比维度 | color033 | Rich |
|----------|----------|------|
| 设计哲学 | 给你颜色，你用 Python 自由组合 | 给你一套新语法，你学会再用 |
| 学习门槛 | 零（会 `print()` 就会用） | 高（要学 `Console`、`Style`） |
| 颜色存储 | 有（回收站、env、表格、often） | 无（用完即丢） |
| 颜色锁定 | ✅ 两层锁（只读锁 + 密钥锁） | ❌ |
| 配色备份 | ✅ `env_save` 导出 JSON | ❌ |
| 配色预览 | ✅ `new_info` / `classic_info` | ❌ |
| 256色渐变 | ✅ `fg_256()` | ❌ |
| 生活化配色 | ✅ COFFEE、CARAMEL、WHEAT | ❌ |
| 表格 | 可存可取，坐标定位 | 只能渲染 |
| 依赖 | 轻量 | ~20MB |

---

## 📚 API 速查

| 功能 | 函数 |
|------|------|
| 16/256/24位色 | `fg_256()`, `bg_256()`, `fg_rgb()`, `bg_rgb()` |
| 颜色预览 | `new_info()`, `classic_info()` |
| 颜色存储 | `hex_rgb()`, `del_color()`, `r_color()` |
| 颜色锁定 | `f_color()`, `f_lock()`, `f_info()`, `f_read()`, `f_edit()`, `f_del()` |
| 虚拟环境 | `env_color()`, `env_del()`, `env_ls()`, `env_save()`, `env_open()` |
| 回收站 | `recycle()`, `recycir()`, `recyls()`, `frecycle()`, `rPass()` |
| 常用色 | `often_color()` |
| 色彩表格 | `color_addt()`, `color_addc()`, `color_table()`, `color_tdel()`, `colort_all()` |
| 临时色 | `temp_color()`, `reset_temp()` |
| 样式控制 | `BOLD`, `ITALIC`, `UNDERLINE`, `RESET`, `RESET_BOLD`... |

---

## 🤝 贡献

欢迎提交 Issue 和 PR！

- 报告 Bug
- 提出新功能
- 改进文档

---

## 📄 许可证

MIT License

---

## 🌟 最后

> **Rich 让你学它的语法，color033 让你接着用自己的语法。**

> **Rich 是“瑞士军刀”，color033 是“调色盘”。**

> **Rich 帮你画表格，color033 让你自己画表格，并且让每一个边框、每一个字符都带上你想要的颜色。**

**color033 做的只有一件事——让终端颜色变得简单、自由、有趣。**

⭐ **如果这个项目对你有帮助，请给一个 Star！**

---

*Made with 🧡 by color033 team*

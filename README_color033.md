# color033 - 终端24位ANSI色彩渲染库

> **59种开箱即用的颜色，36.8KB源码，会Python就会用。**


## 📦 下载与安装

> ⚠️ **注意：color033 目前未发布在 PyPI，不支持 `pip install` 安装。**

直接前往 GitHub 仓库，点击绿色的 **Code** 按钮，选择 **Download ZIP** 即可下载使用。下载后，将 `color033.py` 放在你的项目目录中，然后：

```python
import color033 as c
```

**就是这么简单——下载即用，零依赖，零配置。**


## 🚀 快速上手

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

# 一行预览颜色
c.new_info(c.COFFEE)   # 输出十六进制 + 生活化文案 + 预览文本
```

**color033 的每个颜色都是普通 Python 字符串（ANSI 转义序列），可以放进任何接受字符串的地方。** 不需要学新API，不需要建 `console` 对象，会 `print()` 就会用。


## 🎯 与其他库的核心差异

| 对比维度 | **color033** | **Rich** | **Colorama** | **colorsys** | **ansi** |
|---|---|---|---|---|---|
| **颜色数量（开箱即用）** | **59种** | ~16种 | 16种（8+8） | 不支持终端颜色 | 256色 / RGB |
| **棕色系** | **11种**（COFFEE, CARAMEL, WHEAT…） | 1种（brown） | 无 | 无 | 无 |
| **原生 print() 兼容** | ✅ 直接塞，会Python就会用 | ❌ 必须用 `console.print()` | ✅ 直接塞 | ✅ 直接塞 | ✅ 直接塞 |
| **原生 input() 兼容** | ✅ 直接塞 | ❌ 必须用 `console.input()` | ✅ 直接塞 | ✅ 直接塞 | ✅ 直接塞 |
| **颜色回收站** | ✅ `recycle()` 误删可恢复 | ❌ | ❌ | ❌ | ❌ |
| **颜色锁定** | ✅ `f_color()` / `f_lock()` 防误改 | ❌ | ❌ | ❌ | ❌ |
| **虚拟环境** | ✅ `env` 配色隔离，可导出导入 | ❌ | ❌ | ❌ | ❌ |
| **二维色彩表格** | ✅ 坐标存取，可读可写 | ❌（只能渲染） | ❌ | ❌ | ❌ |
| **256色渐变** | ✅ `fg_256()` 原生支持 | ❌ | ❌ | ❌ | ✅ 支持 |
| **颜色预览** | ✅ `new_info()` 一行预览，带十六进制+文案 | ❌（需自己写） | ❌ | ❌ | ❌ |
| **生活化命名** | ✅ COFFEE、CARAMEL、WHEAT、PINK… | ❌（仅技术命名） | ❌（仅基础色名） | ❌ | ❌ |
| **批量平均填充** | ✅ `color_fill()` 自动分配颜色到文本 | ❌ | ❌ | ❌ | ❌ |
| **静默模式** | ✅ `log=False` 控制台安静 | ❌ | ❌ | ❌ | ❌ |
| **学习成本** | **极低**（会Python就会用） | 高（要学新语法） | 极低 | 低 | 中（需理解ANSI码） |
| **依赖体积** | **36.8KB** | ~20MB | 轻量 | 无（标准库） | 轻量 |
| **跨平台** | Linux/macOS/Windows | 全平台 | 全平台（专治Windows） | 全平台 | 取决于终端 |


## 🎨 配色体系

| 层级 | 用户类型 | 功能 | 用途 |
|---|---|---|---|
| 第一层 | 路人 | 12fg + 12bg | 日常够用，不费脑子 |
| 第二层 | 装饰者 | 24fg + 12bg + `_often` | 让终端好看，有格调 |
| 第三层 | 画家 | 59fg + 30bg + 函数 | 自由创作，不受限制 |


## 📚 完整 API 参考

### 一、基础颜色常量（开箱即用）

所有颜色常量都是 **ANSI 转义字符串**，可以直接拼接在 `print()` 或 `input()` 中使用。调用结束后，务必用 `RESET` 或对应的 `RESET_*` 结束样式，否则后续输出会继承当前颜色。

---

#### ① 基础8色前景

| 常量 | 颜色 | 说明 |
|---|---|---|
| `BLACK` | 黑色 | ANSI标准黑 |
| `RED` | 红色 | ANSI标准红 |
| `GREEN` | 绿色 | ANSI标准绿 |
| `YELLOW` | 黄色 | ANSI标准黄 |
| `BLUE` | 蓝色 | ANSI标准蓝 |
| `MAGENTA` | 洋红 | ANSI标准洋红 |
| `CYAN` | 青色 | ANSI标准青 |
| `WHITE` | 白色 | ANSI标准白 |

**使用方式：**

```python
print(c.RED + "这是红色文字" + c.RESET)
```

---

#### ② 高亮8色前景

| 常量 | 颜色 | 说明 |
|---|---|---|
| `GRAY` | 灰色 | 高亮灰 |
| `RED_LIGHT` | 亮红 | 高亮红 |
| `GREEN_LIGHT` | 亮绿 | 高亮绿 |
| `YELLOW_LIGHT` | 亮黄 | 高亮黄 |
| `BLUE_LIGHT` | 亮蓝 | 高亮蓝 |
| `MAGENTA_LIGHT` | 亮洋红 | 高亮洋红 |
| `CYAN_LIGHT` | 亮青 | 高亮青 |
| `WHITE_LIGHT` | 亮白 | 高亮白 |

**使用方式：**

```python
print(c.RED_LIGHT + "这是亮红色文字" + c.RESET)
```

---

#### ③ 基础8色背景

| 常量 | 颜色 | 说明 |
|---|---|---|
| `BG_BLACK` | 黑色背景 | ANSI标准黑底 |
| `BG_RED` | 红色背景 | ANSI标准红底 |
| `BG_GREEN` | 绿色背景 | ANSI标准绿底 |
| `BG_YELLOW` | 黄色背景 | ANSI标准黄底 |
| `BG_BLUE` | 蓝色背景 | ANSI标准蓝底 |
| `BG_MAGENTA` | 洋红背景 | ANSI标准洋红底 |
| `BG_CYAN` | 青色背景 | ANSI标准青底 |
| `BG_WHITE` | 白色背景 | ANSI标准白底 |

**使用方式：**

```python
print(c.BG_RED + c.WHITE + "红底白字" + c.RESET)
```

---

#### ④ 24位真彩色（生活化命名）

> 这些是 color033 的招牌颜色——每个颜色都配有生活化双语文案，让颜色更有温度。

| 常量 | 颜色 | RGB | 中文文案 |
|---|---|---|---|
| `TRUE_BLACK` | 纯黑 | `0,0,0` | 深夜街边黑巧克力冰淇淋 |
| `TRUE_WHITE` | 纯白 | `255,255,255` | 清晨奶油雪顶牛乳 |
| `ORANGE` | 橙色 | `255,128,0` | 傍晚路边橘子汽水小摊 |
| `PINK` | 粉色 | `255,105,180` | 春日樱花蜜桃奶茶三分糖 |
| `LIME` | 青柠色 | `120,255,0` | 夏日青柠鲜爽气泡冰水 |
| `SKY_BLUE` | 天空蓝 | `80,180,255` | 郊外晴天浅蓝天，治愈开阔 |
| `PURPLE_DARK` | 深紫 | `100,20,180` | 深夜葡萄果酒暗紫色 |
| `VIOLET` | 紫罗兰 | `200,80,255` | 傍晚薰衣草花田淡紫 |
| `BROWN` | 棕色 | `130,80,40` | 原木桌面复古咖啡馆底色 |
| `GRAY_DARK` | 深灰 | `60,60,60` | 雨天路边水泥墙面 |
| `GRAY_MID` | 中灰 | `140,140,140` | 阴天户外石板小路 |
| `GRAY_LIGHT` | 浅灰 | `200,200,200` | 清晨雾蒙蒙浅灰马路 |

**使用方式：**

```python
print(c.ORANGE + "橙色文字" + c.RESET)
c.new_info(c.ORANGE)  # 查看颜色详情 + 生活化文案
```

---

#### ⑤ 咖啡系列（11种棕色系）

> 这是 color033 的独家特色——市面上唯一提供完整棕色系终端颜色库。

| 常量 | 颜色 | RGB | 中文文案 |
|---|---|---|---|
| `BROWN_DARK` | 深棕 | `90,50,30` | 深夜加班靠浓缩咖啡提神 |
| `BROWN_MEDIUM` | 中棕 | `160,100,60` | 周末坐在咖啡馆看书发呆 |
| `BROWN_LIGHT` | 浅棕 | `210,140,90` | 下午茶搭配曲奇和浅烘咖啡 |
| `COFFEE` | 咖啡色 | `120,70,40` | 前往瑞幸咖啡喝一杯生椰拿铁 |
| `COCOA` | 可可色 | `150,90,55` | 冬天在家冲一杯热可可暖手 |
| `CARAMEL` | 焦糖色 | `210,150,80` | 焦糖玛奇朵的甜香飘满门店 |
| `WHEAT` | 小麦色 | `245,220,160` | 清晨去面包店买刚出炉小麦吐司 |
| `TAUPE` | 灰褐色 | `150,120,90` | 咖啡店灰褐色水泥调桌面 |
| `MAROON` | 栗色 | `120,30,30` | 复古红酒棕咖啡杯很出片 |
| `SAND` | 沙色 | `230,190,130` | 窗边沙米色桌面摆一杯冷萃 |

**使用方式：**

```python
print(c.COFFEE + "喝一杯咖啡色文字" + c.RESET)
print(c.CARAMEL + "焦糖色的温暖" + c.RESET)
```

---

#### ⑥ 代码高亮色系

| 常量 | 颜色 | 用途 | RGB |
|---|---|---|---|
| `CODE_KEYWORD` | 橙色 | 关键字 | `255,130,0` |
| `CODE_STRING` | 亮绿 | 字符串 | `60,220,100` |
| `CODE_NUMBER` | 亮蓝 | 数字 | `60,160,255` |
| `CODE_COMMENT` | 灰紫 | 注释 | `90,90,120` |
| `CODE_FUNCTION` | 淡紫 | 函数名 | `180,120,255` |
| `CODE_VARIABLE` | 金色 | 变量 | `210,160,0` |
| `CODE_OPERATOR` | 浅灰 | 运算符 | `200,200,200` |
| `CODE_TYPE` | 浅蓝 | 类型 | `60,180,220` |
| `CODE_ERROR_UNDERLINE` | 红色 | 错误下划线 | `255,80,80` |
| `CODE_WARN_UNDERLINE` | 橙色 | 警告下划线 | `255,180,0` |

**使用方式：**

```python
print(c.CODE_KEYWORD + "def " + c.CODE_FUNCTION + "my_func" + c.CODE_OPERATOR + "():" + c.RESET)
```

---

#### ⑦ 日志色系

| 常量 | 颜色 | 用途 | RGB |
|---|---|---|---|
| `LOG_SUCCESS` | 亮绿 | 成功信息 | `40,220,80` |
| `LOG_ERROR` | 亮红 | 错误信息 | `255,40,40` |
| `LOG_WARN` | 橙色 | 警告信息 | `255,170,0` |
| `LOG_INFO` | 亮蓝 | 一般信息 | `60,160,255` |
| `LOG_DEBUG` | 灰色 | 调试信息 | `160,160,160` |
| `LOG_TRACE` | 蓝紫 | 追踪信息 | `100,100,180` |
| `LOG_FATAL` | 红 | 致命错误 | `255,30,30` |
| `LOG_SKIP` | 黄绿 | 跳过信息 | `180,180,100` |
| `LOG_WAIT` | 蓝绿 | 等待信息 | `80,180,200` |

**使用方式：**

```python
print(c.LOG_SUCCESS + "✅ 任务完成" + c.RESET)
print(c.LOG_ERROR + "❌ 操作失败" + c.RESET)
```

---

### 二、样式控制常量

| 常量 | 效果 | 说明 |
|---|---|---|
| `BOLD` | **粗体** | 开启粗体 |
| `DIM` | 暗淡 | 暗淡效果 |
| `ITALIC` | *斜体* | 开启斜体 |
| `UNDERLINE` | <u>下划线</u> | 开启下划线 |
| `BLINK_SLOW` | 闪烁（慢） | 慢速闪烁 |
| `BLINK_FAST` | 闪烁（快） | 快速闪烁 |
| `REVERSE` | 反显 | 前景背景互换 |
| `HIDE` | 隐藏 | 隐藏文字 |
| `STRIKE` | ~~删除线~~ | 删除线 |
| `DOUBLE_UNDER` | 双下划线 | 双重下划线 |

**重置常量：**

| 常量 | 作用 |
|---|---|
| `RESET` | 重置所有样式和颜色 |
| `RESET_BOLD` | 仅重置粗体 |
| `RESET_ITALIC` | 仅重置斜体 |
| `RESET_UNDER` | 仅重置下划线 |
| `RESET_BLINK` | 仅重置闪烁 |
| `RESET_REVERSE` | 仅重置反显 |
| `RESET_HIDE` | 仅重置隐藏 |
| `RESET_STRIKE` | 仅重置删除线 |

**使用方式：**

```python
print(c.BOLD + "粗体文字" + c.RESET_BOLD + "恢复正常")
print(c.ITALIC + "斜体文字" + c.RESET_ITALIC + "恢复正常")
# 精细控制：只关斜体，粗体保留
print(c.BOLD + c.ITALIC + "粗斜体" + c.RESET_ITALIC + "只有粗体了" + c.RESET)
```


### 三、底层RGB工具函数

---

#### `fg_256(color_code: int) -> str`

生成256色前景色转义序列。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `color_code` | `int` | 0~255 之间的色号 |

**返回值：** `str` —— ANSI 转义序列

**使用方式：**

```python
print(c.fg_256(196) + "亮红色文字" + c.RESET)
```

**色号说明：**
- `0-15`：系统基础色
- `16-231`：6×6×6 颜色立方体（216色）
- `232-255`：灰度渐变（24级）

---

#### `bg_256(color_code: int) -> str`

生成256色背景色转义序列。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `color_code` | `int` | 0~255 之间的色号 |

**返回值：** `str` —— ANSI 转义序列

**使用方式：**

```python
print(c.bg_256(196) + "亮红色背景" + c.RESET)
```

---

#### `fg_rgb(r: int, g: int, b: int) -> str`

生成24位真彩色前景色转义序列。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `r` | `int` | 红色通道 0~255 |
| `g` | `int` | 绿色通道 0~255 |
| `b` | `int` | 蓝色通道 0~255 |

**返回值：** `str` —— ANSI 转义序列

**使用方式：**

```python
custom_color = c.fg_rgb(255, 128, 64)
print(custom_color + "自定义橙色文字" + c.RESET)
```

---

#### `bg_rgb(r: int, g: int, b: int) -> str`

生成24位真彩色背景色转义序列。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `r` | `int` | 红色通道 0~255 |
| `g` | `int` | 绿色通道 0~255 |
| `b` | `int` | 蓝色通道 0~255 |

**返回值：** `str` —— ANSI 转义序列

**使用方式：**

```python
custom_bg = c.bg_rgb(255, 128, 64)
print(custom_bg + "自定义橙色背景" + c.RESET)
```


### 四、颜色预览函数

---

#### `new_info(color, *prompt)`

查看颜色的详细信息：十六进制值、生活化文案预览、颜色效果。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `color` | `str` | 颜色转义序列（如 `c.RED`） |
| `*prompt` | `str` | 可选，自定义预览文本（不传则使用生活化文案或默认狐狸句） |

**使用方式：**

```python
c.new_info(c.COFFEE)
# 输出：
# #A84628
# 前往瑞幸咖啡喝一杯生椰拿铁
# go to luckin coffee for a coconut latte

c.new_info(c.ORANGE, "自定义预览文字")
# 输出：
# #FF8000
# 自定义预览文字
```

---

#### `classic_info(color_const)`

快速预览颜色，输出十六进制值 + 经典狐狸句。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `color_const` | `str` | 颜色转义序列 |

**使用方式：**

```python
c.classic_info(c.RED)
# 输出： #FF0000 [红色预览] the quick brown fox jumps over a lazy dog
```

**与 `new_info` 的区别：**

| 特性 | `new_info` | `classic_info` |
|---|---|---|
| 十六进制值 | ✅ | ✅ |
| 生活化文案 | ✅ | ❌ |
| 自定义预览文本 | ✅（传 `*prompt`） | ❌ |
| 适用场景 | 展示、教学、详细查看 | 快速看一眼颜色 |

---

#### `new_rgb(r: int, g: int, b: int, *prompt)`

直接预览RGB颜色，不需要先定义常量。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `r` | `int` | 红色通道 0~255 |
| `g` | `int` | 绿色通道 0~255 |
| `b` | `int` | 蓝色通道 0~255 |
| `*prompt` | `str` | 可选，自定义预览文本 |

**使用方式：**

```python
c.new_rgb(255, 128, 0, "橙色预览")
# 输出：
# #FF8000
# 橙色预览
```


### 五、颜色存储与管理函数

> color033 的存储架构是开放的——所有底层字典都可以直接访问，你永远有控制权。

**存储架构：**

| 存储层 | 用途 | 底层变量 |
|---|---|---|
| 原生内置全局色 | 无限制自由修改 | （直接使用常量） |
| 高频常用色 | 速查表，最常用的颜色 | `_often` |
| 全局自定义色 | 单变量零散配色 | `_user_color_vars` |
| 二维色彩表格 | 网格矩阵批量收纳 | `_color_table_storage` |
| 虚拟环境 | 多套独立主题 | `_env_storage` |
| 回收站 | 软删除备份 | `_recycle_bin` |

---

#### `hex_rgb(r_str: str, g_str: str, b_str: str, var_name: str) -> str`

将十六进制颜色值转换为ANSI转义序列，并存入全局自定义颜色字典。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `r_str` | `str` | 十六进制红色（两位，如 `"FF"`） |
| `g_str` | `str` | 十六进制绿色（两位，如 `"00"`） |
| `b_str` | `str` | 十六进制蓝色（两位，如 `"00"`） |
| `var_name` | `str` | 变量名，用于后续引用 |

**返回值：** `str` —— ANSI 转义序列

**使用方式：**

```python
c.hex_rgb("FF", "00", "00", "my_red")
print(c._user_color_vars["my_red"] + "红色文字" + c.RESET)
```

---

#### `del_color(var_name: str)`

从全局自定义颜色字典中永久删除一个颜色。

> ⚠️ **警告：** 删除操作不可逆，且不会进入回收站。如需安全删除，请使用 `recycle`。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `var_name` | `str` | 要删除的变量名 |

**使用方式：**

```python
c.hex_rgb("FF", "00", "00", "temp_color")
c.del_color("temp_color")  # 永久删除
```

**与 `f_color` 的关系：** 如果变量被 `f_color` 锁定，直接调用 `del_color` 会报错。

---

#### `r_color(var_name: str)`

将全局自定义颜色重置为空字符串（保留变量名）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `var_name` | `str` | 要重置的变量名 |

**使用方式：**

```python
c.hex_rgb("FF", "00", "00", "my_color")
c.r_color("my_color")  # my_color 的值变为空字符串
print(c._user_color_vars["my_color"])  # 输出空
```

---

#### `f_color(var_name: str)`

将全局自定义颜色设置为只读锁定。

> 锁定后，该颜色不能被 `del_color` 或 `r_color` 修改/删除。适用于保护核心配色。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `var_name` | `str` | 要锁定的变量名 |

**使用方式：**

```python
c.hex_rgb("FF", "00", "00", "primary_color")
c.f_color("primary_color")
c.del_color("primary_color")  # ❌ 报错：被锁定了
```

---

#### `passTo(old_var: str, new_var: str)`

将颜色从一个变量转移到另一个变量，原变量置空。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `old_var` | `str` | 源变量名 |
| `new_var` | `str` | 目标变量名 |

**使用方式：**

```python
c.hex_rgb("FF", "00", "00", "temp")
c.passTo("temp", "final")
# temp 变为空字符串，final 获得该颜色
```


### 六、颜色锁定与注释函数（`f_*` 系列）

> 这是 color033 的独家功能——你可以给颜色加锁、加注释、加预览，形成完整的配色文档。

---

#### `f_lock(fcolor: str, lock: bool, act: str, log=True)`

为自定义颜色设置密钥锁。锁定后，修改/删除需要提供正确密钥。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `fcolor` | `str` | 要锁定的变量名 |
| `lock` | `bool` | `True`=锁定，`False`=解锁 |
| `act` | `str` | 密钥（锁定/解锁需要同一密钥） |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.hex_rgb("FF", "00", "00", "my_red")
c.f_lock("my_red", lock=True, act="123")  # 锁定，密钥为123
c.f_lock("my_red", lock=False, act="123") # 解锁，需要同一密钥
```

---

#### `f_info(fcolor: str, prompt="Preview text in this color", *info)`

为锁定变量添加注释和预览文本。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `fcolor` | `str` | 变量名 |
| `prompt` | `str` | 预览文本（默认 `"Preview text in this color"`） |
| `*info` | `str` | 注释内容（多行自动换行） |

**使用方式：**

```python
c.f_info("my_red", "这是主色调红色", "用于错误提示", "RGB: 255,0,0")
```

---

#### `f_read(fcolor: str)`

查看锁定变量的完整信息：锁定状态、预览样例、注释内容。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `fcolor` | `str` | 变量名 |

**使用方式：**

```python
c.f_read("my_red")
# 输出：
# ===== 锁定变量 my_red 信息 =====
# 锁定状态：🔒 上锁
# 预览样例：这是主色调红色
# 完整注释：
# 用于错误提示
# RGB: 255,0,0
```

---

#### `f_edit(fcolor: str, *info, log=True)`

修改锁定变量的注释（需要先解锁）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `fcolor` | `str` | 变量名 |
| `*info` | `str` | 新的注释内容 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.f_lock("my_red", lock=False, act="123")  # 先解锁
c.f_edit("my_red", "新的注释内容")
c.f_lock("my_red", lock=True, act="123")   # 重新锁定
```

---

#### `f_cedit(oldf: str, newf: str, log=True)`

修改锁定变量的色彩值（需要先解锁）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `oldf` | `str` | 变量名 |
| `newf` | `str` | 新的颜色值（ANSI转义序列） |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.f_lock("my_red", lock=False, act="123")  # 先解锁
c.f_cedit("my_red", c.BLUE)                # 改为蓝色
c.f_lock("my_red", lock=True, act="123")   # 重新锁定
```

---

#### `f_del(fcolor: str, log=True)`

彻底删除锁定变量及其注释（需要先解锁）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `fcolor` | `str` | 变量名 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.f_lock("my_red", lock=False, act="123")  # 先解锁
c.f_del("my_red")                          # 彻底删除
```

---

### 七、临时颜色函数（`TEMP` / `BG_TEMP`）

> 会话级临时色，反复使用，不想用就清掉。

---

#### `temp_color(r: int, g: int, b: int, type: str)`

将RGB颜色存入临时变量 `TEMP`（前景）或 `BG_TEMP`（背景）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `r` | `int` | 红色通道 0~255 |
| `g` | `int` | 绿色通道 0~255 |
| `b` | `int` | 蓝色通道 0~255 |
| `type` | `str` | `"fg"` 存入 `TEMP`，`"bg"` 存入 `BG_TEMP` |

**使用方式：**

```python
c.temp_color(255, 128, 0, "fg")
print(c.TEMP + "橙色文字" + c.RESET)
print(c.TEMP + "还是橙色" + c.RESET)
c.reset_temp()  # 清空临时色
```

---

#### `reset_temp()`

清空 `TEMP` 和 `BG_TEMP`。

**使用方式：**

```python
c.reset_temp()
```

---

### 八、虚拟环境函数（`env`）

> 多套配色隔离，互不干扰，可导出导入持久化。适合团队协作、多主题切换。

---

#### `env_color(name=None, *color, log=True)`

创建或更新虚拟环境。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 环境名称（不传自动生成 `env1`, `env2`...） |
| `*color` | `tuple` | 颜色项，格式 `(颜色名, 颜色值)` |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.env_color("work", ("primary", c.BLUE), ("danger", c.DANGER_RED))
c.env_color("play", ("primary", c.PINK), ("danger", c.ORANGE))
```

---

#### `envs() -> EnvNamespace`

返回全部虚拟环境的命名空间容器，支持 `envs().环境名.颜色名` 调用。

**返回值：** `EnvNamespace` —— 可通过点号访问的环境对象

**使用方式：**

```python
print(c.envs().work.primary + "工作模式" + c.RESET)
print(c.envs().play.primary + "娱乐模式" + c.RESET)
```

---

#### `env_del(name, log=True)`

删除虚拟环境（需要二次确认）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 环境名称 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.env_del("work")  # 输入 y 确认删除
```

---

#### `env_cdel(name, *color, log=True)`

删除指定环境内的若干色彩变量。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 环境名称 |
| `*color` | `str` | 要删除的颜色名 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.env_cdel("work", "primary", "danger")
```

---

#### `env_ls()`

列出当前全部虚拟环境及其包含的颜色。

**使用方式：**

```python
c.env_ls()
# 输出：
# ===== 现有全部色彩虚拟环境 =====
# 环境名：work | 内含色彩：['primary', 'danger']
# 环境名：play | 内含色彩：['primary', 'danger']
```

---

#### `env_ren(old, new, log=True)`

重命名虚拟环境。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `old` | `str` | 旧环境名 |
| `new` | `str` | 新环境名 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.env_ren("work", "prod")
```

---

#### `env_save(name, path: str, log=True)`

导出虚拟环境到本地 JSON 文件。

> 这是团队协作的核心功能——配色方案可以导出成文件，提交到 Git，团队成员导入后使用完全一致的配色。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 环境名称 |
| `path` | `str` | 导出路径（如 `"./theme.json"`） |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.env_save("work", "./work_theme.json")
```

---

#### `env_open(name, path: str, log=True)`

从本地 JSON 文件导入配色方案，生成新环境。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 新环境名称 |
| `path` | `str` | 导入路径 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.env_open("work_imported", "./work_theme.json")
```


### 九、回收站函数（`recycle`）

> 软删除备份，防止误删永久丢失配色。

---

#### `recycle(*object, oper=True, rec="default_rec", promode="uncover", log=True)`

将颜色存入回收站或从回收站恢复。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `*object` | `tuple` | 回收对象，格式 `(变量名, 颜色值)` |
| `oper` | `bool` | `True`=存入回收站，`False`=恢复 |
| `rec` | `str` | 回收站分区名（默认 `"default_rec"`） |
| `promode` | `str` | `"uncover"`=不覆盖（重名转列表），`"cover"`=直接覆盖 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
# 存入回收站
c.recycle(("my_color", c.RED), rec="default_rec")

# 查看回收站
c.recyls("default_rec")

# 恢复
recovered = c.recycle(("my_color", c.RED), oper=False, rec="default_rec")
my_color = recovered["my_color"]
```

---

#### `frecycle(log=True)`

清空全部回收站所有分区。

**使用方式：**

```python
c.frecycle()
```

---

#### `recycir(name, log=True)`

新建独立回收站分区。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 分区名称 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.recycir("project_backup")
```

---

#### `recyls(name=None)`

查看回收站内容。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 分区名（不传默认 `"default_rec"`） |

**使用方式：**

```python
c.recyls("default_rec")
# 输出： my_color : \033[31m
```

---

#### `rPass(old_rec: str, new_rec: str, log=True)`

将一个回收站分区的全部内容转移到另一个分区。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `old_rec` | `str` | 源分区名 |
| `new_rec` | `str` | 目标分区名 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.rPass("default_rec", "archive_rec")
```

---

#### `rcontent(cont, newcont, log=True)`

将字典内容无损转移至另一个字典，不覆盖原有键值。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `cont` | `dict` | 源字典 |
| `newcont` | `dict` | 目标字典 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
source = {"color1": c.RED, "color2": c.BLUE}
target = {"color3": c.GREEN}
c.rcontent(source, target)
# target 现在包含 color1, color2, color3
```


### 十、二维色彩表格函数（`color_table`）

> 像 Excel 一样按坐标存取颜色，可跳着存，可无限扩展。

---

#### `color_addt(name, log=True)`

创建空白色彩表格。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 表格名称 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.color_addt("my_palette")
```

---

#### `color_addc(name, x: int, y: int, color, log=True)`

在指定表格的 `(x, y)` 单元格写入颜色。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 表格名称 |
| `x` | `int` | X坐标 |
| `y` | `int` | Y坐标 |
| `color` | `str` | 颜色转义序列 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.color_addc("my_palette", 0, 0, c.RED)
c.color_addc("my_palette", 0, 1, c.BLUE)
c.color_addc("my_palette", 5, 5, c.GREEN)  # 跳着存
```

---

#### `color_table(tname, x: int, y: int) -> str`

从表格中提取指定坐标的颜色值。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `tname` | `str` | 表格名称 |
| `x` | `int` | X坐标 |
| `y` | `int` | Y坐标 |

**返回值：** `str` —— ANSI 转义序列

**使用方式：**

```python
my_color = c.color_table("my_palette", 0, 0)
print(my_color + "红色文字" + c.RESET)
```

---

#### `color_tdel(name, log=True)`

永久删除整张色彩表格（推荐先使用 `recycle` 备份）。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 表格名称 |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.color_tdel("my_palette")  # 需要输入 y 确认
```

---

#### `color_tls()`

列出当前全部已创建的色彩表格名称及单元格数量。

**使用方式：**

```python
c.color_tls()
# 输出：
# ===== 现有全部色彩表格列表 =====
# 表格名称：my_palette | 存储单元格数量：3
```

---

#### `colort_all(name)`

遍历指定表格全部单元格，格式化打印坐标、十六进制色值、预览色。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 表格名称 |

**使用方式：**

```python
c.colort_all("my_palette")
# 输出：
# ===== 色彩表格 [my_palette] 全部单元格明细 =====
# x: 0  y: 0   color: #FF0000, your table color 样例文本
# x: 0  y: 1   color: #0000FF, your table color 样例文本
```

---

#### `color_tread(name, x: int, y: int)`

查看单元格完整信息。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `name` | `str` | 表格名称 |
| `x` | `int` | X坐标 |
| `y` | `int` | Y坐标 |

**使用方式：**

```python
c.color_tread("my_palette", 0, 0)
# 输出：
# 🦊单元格详情 | 表格:my_palette 坐标(0,0) | 色值:#FF0000 | ANSI序列:\033[31m
# 预览效果：示例文字 | abcdefghijklmnopqrstuvwxyz0123456789 | This is a paragraph with color.
```


### 十一、高频常用色函数（`often_color`）

> 最常用的颜色存起来，随取随用，独立于 `env` 虚拟环境。

---

#### `often_color(str_name: str, color: str, log=True)`

将色彩存入常用色字典，禁止重名。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `str_name` | `str` | 自定义标识名称 |
| `color` | `str` | 颜色值（支持 `#RRGGBB` 十六进制字符串或ANSI转义序列） |
| `log` | `bool` | 是否打印状态信息（默认 `True`） |

**使用方式：**

```python
c.often_color("primary", "#FF0000")
c.often_color("bg", c.BLUE)
print(c._often["primary"] + "重要文本" + c.RESET)
```


### 十二、`print_color` —— 简单颜色输出

---

#### `print_color(text, *styles, end="\n")`

快速打印带颜色的文本，自动重置。

**参数：**

| 参数 | 类型 | 说明 |
|---|---|---|
| `text` | `str` | 要输出的文本 |
| `*styles` | `str` | 样式/颜色常量（如 `c.RED`, `c.BOLD`） |
| `end` | `str` | 结尾字符（默认 `"\n"`） |

> ⚠️ `print_color` 只能传一个字符串和一组样式。如果你需要不同片段不同颜色，推荐使用 f-strings 或 `color_fill`。

**使用方式：**

```python
c.print_color("红色文本", c.RED)
c.print_color("粗体红色文本", c.RED, c.BOLD)
c.print_color("不换行", c.GREEN, end="")
```


### 十三、`color_fill` —— 批量平均填充

> 将颜色/样式/任意前缀平均分配给文本，自动计算分割方案。

---

#### `color_fill(colors: tuple, text: str, prt_lst=False, reseted=False, ender='\n', seper='')`

**参数：**

| 参数 | 类型 | 说明 | 默认值 |
|---|---|---|---|
| `colors` | `tuple` | 前缀元组（颜色/样式/任意可打印对象） | 必传 |
| `text` | `str` | 要装饰的文本（自动转字符串） | 必传 |
| `prt_lst` | `bool` | 是否打印内部切分方案（调试用） | `False` |
| `reseted` | `bool` | 每个分段后是否独立重置 | `False` |
| `ender` | `str` | 最终输出结尾字符 | `'\n'` |
| `seper` | `str` | 前缀与文本之间的分隔符 | `''` |

**使用方式：**

```python
# 颜色平均分配
c.color_fill((c.RED, c.GREEN, c.BLUE), "你好世界！", reseted=True)

# 样式平均分配
c.color_fill((c.BOLD, c.ITALIC), "12345", reseted=True)

# 复合样式打包
c.color_fill((c.RED, c.COFFEE, f"{c.BOLD}{c.ITALIC}{c.UNDERLINE}{c.RED}{c.BG_YELLOW}"), "12345", reseted=True)

# 任意前缀（不只是颜色）
c.color_fill(('>', '<'), "12345", reseted=True)  # 输出：>12<345

# 控制分隔符和结尾
c.color_fill((c.RED, c.BLUE), "1234", seper=' ', ender='')
# 输出：RED 12 BLUE 34（无换行）

# 调试模式
c.color_fill((c.RED, c.BLUE), "12345", prt_lst=True)
# 输出：[2, 3] 然后才是颜色输出
```

**`reseted` 参数说明：**

| `reseted` | 效果 |
|---|---|
| `False`（默认） | 样式累积叠加，后一段继承前一段的样式 |
| `True` | 每个分段独立重置，互不干扰 |


### 十四、终端控制常量

| 常量 | 效果 |
|---|---|
| `CLEAR_LINE` | 清除当前行 |
| `CLEAR_LINE_LEFT` | 清除当前行左侧 |
| `CLEAR_LINE_RIGHT` | 清除当前行右侧 |
| `CLEAR_SCREEN` | 清屏 |
| `CURSOR_HIDE` | 隐藏光标 |
| `CURSOR_SHOW` | 显示光标 |
| `CURSOR_SAVE` | 保存光标位置 |
| `CURSOR_LOAD` | 恢复光标位置 |

**使用方式：**

```python
print(c.CLEAR_SCREEN + "屏幕已清空")
```


## 💡 使用建议

### 颜色输出方式的选择

| 需求 | 推荐方案 |
|---|---|
| 单色/单样式输出 | 直接用 `print(c.RED + "text" + c.RESET)` |
| 自由控制每个片段 | 用 f-strings：`print(f"{c.RED}12{c.BLUE}345{c.RESET}")` |
| 多色平均分配 | 用 `color_fill((c.RED, c.BLUE), "12345")` |

### 颜色管理工具的选择

| 需求 | 推荐方案 |
|---|---|
| 不确定是否需要删除 | 用 `recycle` 进回收站，随时可恢复 |
| 确定不需要了 | 用 `del_color` 最终删除 |
| 配色存储 | 用 `env`，有导出导入，适合长期保存 |
| 高频配色 | 用 `_often`，速查表，随取随用 |
| 网格收纳 | 用 `color_table`，按坐标存取 |
| 临时配色 | 用 `TEMP`，会话级，用完即焚 |
| 忘记密钥 | 直接查看 `_key_lock_color[fcolor]["key"]` |


## 📄 许可证

MIT License


## ⭐ 最后

> **Rich 让你学一套新语法，color033 让你接着用 Python。**
>
> **Rich 让你算颜色，color033 让你选颜色。**
>
> **Rich 给你功能，color033 给你自由。**

**color033 做的只有一件事——让终端颜色变得简单、自由、有趣。**

如果这个项目对你有帮助，请给一个 Star！⭐

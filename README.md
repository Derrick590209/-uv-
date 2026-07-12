# -uv-
用uv建立虛擬環境
# Python、uv、虛擬環境之間的關係

假設你的電腦剛買來，裡面可能長這樣：

```text
你的電腦
│
├── Python 3.11
├── Python 3.12
└── Python 3.13
```

可以安裝很多個 Python，它們互不影響。

---

# uv 在哪裡？

`uv` 也是安裝在你的電腦裡的一個工具。

```text
你的電腦
│
├── uv
├── Python 3.11
├── Python 3.12
└── Python 3.13
```

可以把它想成：

> **uv = Python 專案管理員**

它負責：

- 建立專案
- 建立虛擬環境
- 安裝套件
- 管理 Python 版本

它**不是 Python**。

---

# 建立第一個專案

例如：

```text
C:\Users\USER
│
└── my_project
```

目前裡面什麼都沒有。

---

# 執行

```bash
uv init
```

變成：

```text
my_project
│
├── pyproject.toml
├── README.md
└── .python-version
```

> **注意！**
>
> 目前還沒有 Python。

很多初學者會誤以為 `uv init` 已經建立好 Python，其實沒有。

---

# 建立虛擬環境

假設你輸入：

```bash
uv venv --python 3.13
```

這時會發生一件事：

```text
                   電腦

        Python 3.13
             │
             │ 複製一份
             ▼
```

放到專案裡：

```text
my_project
│
├── .venv
│      │
│      ├── python.exe
│      ├── Scripts
│      └── Lib
│
├── pyproject.toml
├── README.md
└── .python-version
```

> **注意！**
>
> 真正執行程式的是 `.venv` 裡面的 Python，
> 不是外面的 Python。

---

# 啟動虛擬環境

```bash
.venv\Scripts\activate
```

CMD 就會變成：

```text
(.venv)
C:\Users\USER\my_project>
```

意思就是：

```text
以後輸入

python

其實就是

↓

.venv 裡面的 python
```

而不是：

```text
C:\Python313\python.exe
```

---

# 安裝 requests

例如：

```bash
uv add requests
```

不是裝到整台電腦。

而是裝到：

```text
my_project
│
├── .venv
│      │
│      ├── Python
│      ├── requests
│      ├── urllib3
│      └── ...
```

所以：

另一個專案完全不知道你安裝了 requests。

---

# 再建立另一個專案

例如：

```text
C:\Users\USER
│
├── AI_Project
└── Website
```

AI_Project：

```text
AI_Project
│
└── .venv
       │
       ├── Python 3.13
       ├── numpy
       └── pandas
```

Website：

```text
Website
│
└── .venv
       │
       ├── Python 3.12
       ├── Django
       └── Pillow
```

兩個完全分開，互不影響。

---

# 全部畫在一起（最重要）

```text
                    你的電腦
────────────────────────────────────────────

               uv（專案管理工具）
                     │
                     │
      ┌──────────────┼──────────────┐
      │              │              │
      ▼              ▼              ▼

 Python 3.11     Python 3.12    Python 3.13
      │              │              │
      └──────────────┴──────────────┘
                     │
                     │ 建立虛擬環境
                     ▼

────────────────────────────────────────────

my_project
│
├── pyproject.toml
├── README.md
├── .python-version
└── .venv
      │
      ├── python.exe   ← 這個專案真正使用的 Python
      ├── requests
      ├── numpy
      └── 其他套件
```

---

# 最後，你只要記住四句話

## 1. Python

真正執行程式的程式語言。

---

## 2. uv

幫你管理 Python 專案、虛擬環境和套件的工具。

---

## 3. `.venv`

每個專案自己的獨立 Python 環境。

---

## 4. `pyproject.toml`

記錄專案資訊、Python 需求版本和相依套件。

---

# 一句話總結

```text
Python 負責執行程式
        ▲
        │
     .venv 使用某個 Python 建立
        ▲
        │
       uv 負責建立與管理 .venv
        ▲
        │
pyproject.toml 記錄整個專案的設定
```

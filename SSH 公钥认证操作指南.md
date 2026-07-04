# SSH 公钥认证操作指南
## 环境信息
| 系统 | IP 地址 | 角色 | 安装命令 |
| --- | --- | --- | --- |
| RHEL 10 | 192.168.135.141 | 客户端/服务端 | `sudo dnf install openssh-server` |
| Ubuntu | 192.168.135.138 | 客户端/服务端 | `sudo apt update && sudo apt install openssh-server` |


> #### 🐧 Linux 各发行版
> 大部分Linux系统通过其包管理器就能直接安装OpenSSH。
>
> #### 🍎 macOS
> macOS 系统预装了 SSH 客户端，无需额外安装。如果需要开启**远程登录**（即SSH服务端）功能，让其他电脑连接到你的 Mac，请按以下步骤操作：
>
> 1. 打开“**系统设置**” (System Settings)。
> 2. 点击“**通用**” (General) 选项。
> 3. 选择“**共享**” (Sharing)。
> 4. 开启“**远程登录**” (Remote Login) 开关。
>
> 开启服务后，你也可以在终端中查看或管理SSH服务：
>
> #### 🪟 Windows
> Windows 10 及以上版本默认已安装 OpenSSH 客户端，可以通过 PowerShell 或命令提示符直接使用。若未安装，可手动添加：
>
> + **图形界面安装**：
>     1. 打开“**设置**” (Settings)。
>     2. 进入“**应用**” (Apps) > “**可选功能**” (Optional features)。
>     3. 点击“**添加功能**” (Add a feature)，在列表中找到 `OpenSSH 客户端` 或 `OpenSSH 服务器`，点击“安装”即可。
> + **命令行安装（以管理员身份运行PowerShell）**：
>
> **小提示**：在Windows中，SSH服务器的服务名称是`sshd`。安装后可使用以下命令管理：
>
> #### 🔧 验证安装
> 无论使用哪种操作系统，安装或配置完成后，你都可以在终端（或PowerShell）中运行以下命令来验证是否成功：
>
> 如果命令返回类似 `OpenSSH_9.Xp1 ...` 的版本信息，就说明SSH已经准备就绪了。
>
> #### 💡 补充说明：客户端 vs. 服务端
> 你可能已经注意到，安装命令有时会区分客户端 (`openssh-client`) 和服务端 (`openssh-server`)。
>
> + **SSH 客户端 (**`ssh`**)**：是你用于**连接其他**安装了SSH服务的设备的工具。
> + **SSH 服务端 (**`sshd`**)**：是运行在目标设备上**接受连接**的服务。
>
> 简单来说，如果你想远程连接到设备A，那么你的设备需要一个客户端，而设备A需要启动服务端。许多系统的包管理器会同时提供这两个组件，或者将它们打包在同一个核心包（如`openssh`）中。
>

| 操作系统 | 安装服务端命令 | 安装客户端命令 |
| :--- | :--- | :--- |
| **Debian / Ubuntu / Linux Mint** | `sudo apt install openssh-server` | `sudo apt install openssh-client` (通常预装) |
| **CentOS / RHEL (较旧版本)** | `sudo yum install openssh-server` | `sudo yum install openssh-clients` |
| **RHEL / Fedora (较新版本)** | `sudo dnf install openssh-server` | `sudo dnf install openssh-clients` |
| **Fedora** | `sudo dnf install openssh-server` | `sudo dnf install openssh-clients` |
| **openSUSE** | `sudo zypper install openssh` | `sudo zypper install openssh` |
| **Arch Linux / Manjaro** | `sudo pacman -S openssh` | `sudo pacman -S openssh` |
| **Gentoo** | `sudo emerge -av net-misc/openssh` | `sudo emerge -av net-misc/openssh` |
| **Alpine Linux** | `sudo apk add openssh` | `sudo apk add openssh` |
| **NixOS** | 在 `/etc/nixos/configuration.nix` 中启用 `services.openssh.enable = true;` 后重建系统 | 通常预装 |


> **基本使用建议**：  
安装服务端后，通常需要用以下命令来**启动服务**并设置**开机自启**：
>
> 对于使用 OpenRC 的系统（如 Alpine, Gentoo），命令略有不同，建议参考对应发行版文档。
>

```bash
# 适用于大部分使用 systemd 的发行版 (如 Debian, Ubuntu, Fedora, Arch)
sudo systemctl start sshd   # 启动服务
sudo systemctl enable sshd  # 设置开机自启
```

```bash
# 查看 SSH 服务状态
sudo systemsetup -getremotelogin

# 开启或关闭 SSH 服务 (On/Off)
sudo systemsetup -setremotelogin on
```

```powershell
# 安装 SSH 客户端
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# 安装 SSH 服务器
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

```powershell
# 启动服务
Start-Service sshd
# 设置为自动启动
Set-Service -Name sshd -StartupType 'Automatic'
```

```bash
ssh -V
```

---

## 操作流程
### 1. 检查 SSH 服务
```bash
# RHEL
sudo systemctl status sshd

# Ubuntu
sudo systemctl status ssh
```

---

### 2. 生成密钥对（RHEL → Ubuntu）
```bash
ssh-keygen -t ed25519 -C "rhel-to-ubuntu"
```

> `-C` 添加注释，便于标识用途
>

**设置权限（关键！）**

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
```

---

### 3. 检查服务端配置（在 Ubuntu 上执行）
```bash
# 检查关键配置项
grep -E '^PubkeyAuthentication|^AuthorizedKeysFile' /etc/ssh/sshd_config
```

应看到 `PubkeyAuthentication yes`，如为 `no` 需修改并重启：

```bash
sudo systemctl restart ssh
```

---

### 4. 复制公钥到 Ubuntu
**方法1：自动复制（推荐）**

```bash
ssh-copy-id 你的用户名@192.168.135.138
```

**方法2：手动复制**

```bash
ssh 你的用户名@192.168.135.138
mkdir -p ~/.ssh && chmod 700 ~/.ssh
echo "你的公钥内容" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
exit
```

---

### 5. 测试免密登录
```bash
ssh 你的用户名@192.168.135.138
```

---

### 6. 反向认证（Ubuntu → RHEL）
在 Ubuntu 上执行：

```bash
ssh-keygen -t ed25519 -C "ubuntu-to-rhel"
chmod 700 ~/.ssh && chmod 600 ~/.ssh/id_ed25519
ssh-copy-id 你的用户名@192.168.135.141
ssh 你的用户名@192.168.135.141
```

---

## 故障排查
| 现象 | 排查命令 | 解决 |
| --- | --- | --- |
| 仍要求密码 | `ssh -vvv 用户名@IP` | 查看详细日志 |
| 权限拒绝 | `sudo tail -f /var/log/secure` (RHEL)   `sudo tail -f /var/log/auth.log` (Ubuntu) | 检查服务端日志 |
| 权限错误 | `chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys` | 修复服务端权限 |


**权限速查**

| 文件 | 权限 |
| --- | --- |
| `~/.ssh` | 700 |
| `~/.ssh/id_ed25519` | 600 |
| `~/.ssh/authorized_keys` | 600 |


---

## 常用命令
### 客户端命令（发起连接方）
```bash
# 生成密钥对
ssh-keygen -t ed25519 -C "注释"

# 复制公钥到服务端
ssh-copy-id 用户名@服务端IP

# 连接服务端
ssh 用户名@服务端IP

# 调试连接（查看详细过程）
ssh -vvv 用户名@服务端IP

# 查看本地密钥
ls -la ~/.ssh/
cat ~/.ssh/id_ed25519.pub
```

### 服务端命令（接收连接方）
```bash
# 检查 SSH 服务状态
sudo systemctl status sshd        # RHEL
sudo systemctl status ssh         # Ubuntu

# 重启 SSH 服务
sudo systemctl restart sshd       # RHEL
sudo systemctl restart ssh        # Ubuntu

# 检查服务端配置
grep -E '^PubkeyAuthentication|^AuthorizedKeysFile' /etc/ssh/sshd_config

# 查看认证日志
sudo tail -f /var/log/secure      # RHEL
sudo tail -f /var/log/auth.log    # Ubuntu

# 设置公钥权限
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## 公钥认证流程详解
### 基本概念
+ **私钥**：保存在客户端，相当于"钥匙"，必须保密
+ **公钥**：保存在服务端，相当于"锁"，可以公开

### 认证流程图
```plain
客户端                                    服务端
   │                                        │
   │  1. 发起连接请求                        │
   │ ─────────────────────────────────────>│
   │                                        │
   │  2. 服务端发送随机挑战                  │
   │ <─────────────────────────────────────│
   │                                        │
   │  3. 客户端用私钥签名挑战                │
   │ ─────────────────────────────────────>│
   │                                        │
   │  4. 服务端用公钥验证签名                │
   │     成功 → 允许登录                    │
   │     失败 → 拒绝连接                    │
   │                                        │
   │  5. 建立加密通道                        │
   │ <────────────────────────────────────>│
```

### 具体例子：Alice 连接 Bob
```plain
Alice（客户端）                            Bob（服务端）
     │                                          │
     │  1. 生成密钥对                           │
     │     ssh-keygen -t ed25519                │
     │                                          │
     │  2. 将公钥复制给 Bob                     │
     │     ssh-copy-id bob@192.168.135.138 ────>│
     │                                          │
     │  3. 连接时：                             │
     │     - Bob 发送挑战 "8f3a9c..."           │
     │     - Alice 用私钥签名 ─────────────────>│
     │     - Bob 用公钥验证 ✓                   │
     │                                          │
     │  4. 登录成功                             │
     │     ssh bob@192.168.135.138 ───────────>│
```



---

## 公钥密码学数学原理
### 核心概念：单向函数
**比喻理解**：把两瓶墨水（红+蓝）倒在一起，很容易得到紫色；但给你一瓶紫色墨水，让你准确还原出原来的红和蓝，几乎不可能。

**数字世界**：

```plain
正向（容易）：61 × 53 = 3233  （计算器秒算）
反向（极难）：3233 = ? × ?   （真实质数几百位，超计算机也算不出）
```

这个"**乘起来容易，拆回去极难**"的特性，就是公钥密码的安全根基。

### RSA 算法示例
**造锁和钥匙的过程**：

```plain
1. 选两个小质数：p=61, q=53（真实RSA用几百位数字）
2. 造锁芯 n：n = 61 × 53 = 3233（公开）
3. 选公钥指数 e = 17（公开）
4. 算私钥指数 d = 2753（保密）

最终：
  公钥（锁）= (n, e) = (3233, 17)  → 可以公开给任何人
  私钥（钥匙）= (n, d) = (3233, 2753)  → 绝对不能给别人

数学魔术：知道 n 和 e，算不出 d（除非能分解出 p 和 q）
```

**签名与验证过程**：

```plain
场景：服务器要验证你是不是私钥持有者

① 挑战：服务器发随机数 s=123
        "来，用你的私钥给我签个名看看"

② 签名：你用私钥 d=2753 计算
        签名 sq = 123^2753 mod 3233 = 855
        把 855 发给服务器

③ 验证：服务器用公钥 e=17 计算
        855^17 mod 3233 = 123 ✓
        还原出原数，证明你持有私钥！

核心逻辑：只有手持私钥 d 的人，才能生成能用公钥 e 还原的签名
```

### Ed25519 vs RSA
| 对比项 | RSA | Ed25519 |
| --- | --- | --- |
| 比喻 | 大号机械密码锁 | 现代电子指纹锁 |
| 基础 | 大数分解困难 | 椭圆曲线离散对数困难 |
| 密钥长度 | 2048-4096 位 | 256 位 |
| 速度 | 较慢 | 非常快 |
| 安全性 | 高 | 更高（更抗量子攻击） |


**为什么选 Ed25519？** 椭圆曲线用更短的钥匙提供同等级别保护，所以 `ssh-keygen -t ed25519` 是更优选择。

### 跟 SSH 登录的关系
```plain
1. 生成密钥对（步骤二）
   ssh-keygen -t ed25519
   → 用椭圆曲线数学生成一对"逆运算"数字
   → id_ed25519 是私钥（你的指纹）
   → id_ed25519.pub 是公钥（服务器留存的指纹模）

2. 上传公钥（步骤四）
   ssh-copy-id 把 .pub 存到服务器的 authorized_keys

3. 免密登录（步骤五）
   ssh 用户名@IP
   → 服务器发挑战码
   → 你的电脑用私钥签名
   → 服务器用公钥验证
   → 验证通过，直接放行

整个过程中，私钥从未离开过你的电脑！
```

### 一句话总结
> **公钥和私钥互为"逆运算"——用私钥"锁"上的数据，只有对应公钥能"开"。验证者通过"能不能打开"来判断你是不是持有那把对的私钥。这背后的一切，都建立在"正向好算，反向极难"的数学难题上。**
>



### 简单总结过程
```plain
# 选择俩个质数
p = 61, q = 53

# 计算模数 n
n = p x q = 3233

# 计算欧拉函数 φ(n)  对于俩个质数，φ(n) = (p-1) x (q-1)
φ(n) = (61-1) x (53-1) = 3120

# 选择公钥指数 e     e 需要满足：① 1 < e < φ(n) ② 与 φ(n) 互质。通常选 e = 17（或 65537）
e = 17
gcd(17, 3120)=1

# 计算私钥指数 d     d 是 e 关于模 φ(n) 的乘法逆元
d x e ≡ 1(mod φ(n))
即 d x 17 ≡ 1(mod 3120)
d = 2753
验证：2753 x 17 = 46801
     46801 ÷ 3120 = 15···1

# 产生密钥对：
- 公钥 = (n=3233, e=17)
- 私钥 = (n=3233, d=2753)



# 签名与验证
挑战：服务器发来随机数 s = 123。

签名（用私钥 d 计算）：
签名 sq = s^d mod n
       = 123^2753 mod 3233
       
这个数字巨大，用计算机进行模幂运算后得到：
sq = 855

验证（用公钥 e 计算）：
还原值 s' = sq^e mod n
          = 855^17 mod 3233
          
计算结果：
s' = 123

与挑战值 s=123 完全一致 ✅

数学原理一句话：
(s^d)^e ≡ s^(d×e) ≡ s^1 ≡ s (mod n)
因为 d×e 在模 φ(n) 下等于 1，指数部分的计算遵循欧拉定理。
```



### 用极小数字完整演算
现在用 `p=11, q=13` 重新走一遍，保证每一步都能手算。

#### ① 密钥生成
```plain
p = 11, q = 13
n = 11 × 13 = 143
φ(n) = (11‑1)×(13‑1) = 10×12 = 120

选 e = 7   （与 120 互质，且 1<7<120）
求 d，使得 7×d ≡ 1 (mod 120)
```

求解过程（尝试或扩展欧几里得）：

```plain
7 × 103 = 721
721 ÷ 120 = 6 余 1   ➜ d = 103 ✅
```

密钥对：

+ **公钥**：`(n=143, e=7)`
+ **私钥**：`(n=143, d=103)`

---

#### ② 签名与验证（挑战 s=5）
**签名**：用私钥 `d=103` 计算 `5^103 mod 143`。  
我们一步步做模幂（平方‑乘算法）：

_预备：先把 5 的各次幂模 143 算出来备用_

```plain
5^1 mod 143 = 5
5^2 = 25                → 25
5^4 = (5^2)^2 = 25^2 = 625 → 625 - 143×4 = 625-572 = 53
5^8 = 53^2 = 2809 → 2809 - 143×19 = 2809-2717 = 92
5^16 = 92^2 = 8464 → 8464 - 143×59 = 8464-8437 = 27
5^32 = 27^2 = 729 → 729-143×5 = 729-715 = 14
5^64 = 14^2 = 196 → 196-143 = 53
```

指数 `103` 拆成二进制：103 = 64 + 32 + 4 + 2 + 1  
现在把对应的幂乘起来，边乘边模 143：

```plain
先取 5^64 mod 143 = 53
乘 5^32：53 × 14 = 742 → 742 - 143×5 = 742-715 = 27
乘 5^4：27 × 53 = 1431 → 1431 - 143×10 = 1431-1430 = 1
乘 5^2：1 × 25 = 25
乘 5^1：25 × 5 = 125
```



**最终签名值**：125 📝

**验证**：用公钥 `e=7` 计算 `125^7 mod 143`。  
同样逐步：

```plain
125^1 = 125
125^2 = 15625 → 15625 mod 143:
  143×109 = 15587, 15625-15587 = 38
125^4 = 38^2 = 1444 → 1444 - 143×10 = 1444-1430 = 14
125^7 = 125^4 × 125^2 × 125^1
     = 14 × 38 × 125
     = 14×38 = 532 → 532 - 143×3 = 532-429 = 103
     = 103 × 125 = 12875
     = 12875 mod 143 → 143×90 = 12870, 余 5
```



**还原结果**：`5`，与挑战值完全一致 ✅


# tg-jav-bot

**一个基于 Javbus，Sukebei，Avgle, Dmm 并集成 Pikpak 的 TG 番号查询机器人。**

## 功能简介

**主要功能：**

发送给机器人一条含有番号的消息，机器人会匹配并搜索消息中所有符合 **“字母-数字”** 格式的番号（其它格式的番号可通过 **/av** 命令查找）。如果搜索到结果，将返回番号对应 AV 的 **封面，标题，日期，演员，磁链** 等。

**附加功能：**

- 支持**过滤**磁链（过滤顺序：**高清，有字幕**）
- 支持让机器人自动将**最优磁链**发送到 **pikpak**（随机获取时不会自动发送）
- 支持通过 Dmm 获取**预览视频**功能 （由于 DMM 限制，只支持日本 IP）
- 支持通过 Avgle 获取**完整视频**功能
- 支持获取**截图**功能
- 支持**代理**功能
- 支持**收藏演员和番号**功能
- 支持**随机获取**影片功能
- 支持**日志记录**功能
- 支持**搜索演员**功能

注：记录和日志等文件生成位置在 `~/.tg_jav_bot` 目录下。

## 使用教程

### 一、下载代码

```
git clone https://github.com/akynazh/tg-jav-bot.git
cd tg-jav-bot
```

### 二、安装依赖

如果使用 docker 部署，可以跳过该步骤。

前提：系统已经安装 Python3（>=3.7）

```
pip install -r requirements.txt
```

注：`requirements.txt` 配置使用了国内镜像源，如需取消该设定，可以删除 `requirements.txt` 中的第一行内容：

```
-i https://pypi.tuna.tsinghua.edu.cn/simple
```

### 三、配置机器人

将 `cfg.pub.py` 重命名为 `cfg.py` 并根据提示编辑:

```
# 必填字段

# your telegram chat id
TG_CHAT_ID = ''
 # your telegram bot token
TG_BOT_TOKEN = ''

# 可选字段：关于代理的配置

# 是否使用代理 1 是 | 0 否
USE_PROXY = 1
 # 访问 DMM 是否使用代理 1 是 | 0 否 （该字段的值由自己决定，与 USE_PROXY 无关）
USE_PROXY_DMM = 1
# 如果不使用代理，以下三个字段不用管
# 代理类型 http | socks5 | socks4
PROXY_SCHEME = ''
# IP 地址
PROXY_ADDR_HOST = ''
# 端口地址
PROXY_ADDR_PORT = ''
# 不用编辑该字段
PROXY_ADDR = f'{PROXY_SCHEME}://{PROXY_ADDR_HOST}:{PROXY_ADDR_PORT}'

# 可选字段：关于自动发送磁链到 Pikpak 的配置

# 是否使用 Pikpak 自动发送功能 1 是 | 0 否
USE_PIKPAK = 0
# 如果不使用 pikpak 自动发送功能，以下三个字段不用管
# 默认使用官方机器人：https://t.me/PikPak6_Bot
PIKPAK_BOT_NAME = 'PikPak6_Bot'
# 在这里申请 api：https://my.telegram.org/apps
# telegram api id
TG_API_ID = ''
# telegram api hash
TG_API_HASH = ''
```

如需使用 Pikpak 自动发送功能，需要先生成 `my_account.session` 文件，运行如下命令：

```
python3 util_pikpak.py
```

接着需要在控制台中完成登录操作，登录成功即可生成 `my_account.session` 文件。

### 四、运行机器人

如果不是通过 docker 部署，运行如下命令：

```
nohup python3 bot.py >/dev/null 2>&1 &
```

如果通过 docker 部署，运行如下命令：（前提：安装了 docker 和 docker-compose ）

```
docker-compose up -d
```

# 其他问题
### 密钥
公钥：常用于SSH远程连接
`cat /etc/ssh/key.pub`查看公钥
1. 按下 `Win + R`，输入 `%USERPROFILE%\.ssh`
2. 按下 `Win + X`，选择「Windows 终端」或「命令提示符」，`type %USERPROFILE%\.ssh\id_rsa.pub`
3. 生成密钥对`ssh-keygen -t rsa`

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/u2itf1X7p0ln9Wu7.png)

passphrase是私钥保护密码，可不设置
### 跳板机密码登录
`ssh 用户名@跳板机IP -p 端口号`
1. 属性-用户身份验证-方法（public key）-上传密钥
2. xshell中生成密钥：工具 (Tools) → 用户密钥管理 (User Key Manager)→ 生成 (Generate)/属性 (Properties)查看公钥

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/bb3bRtJzNcLfmNsR.png)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/8Btp7hiBwG9a7zZm.png)

### 项目学习流程
#### 下载项目
`git clone`
#### 创建虚拟环境
1. 激活项目自带的虚拟环境
`source venv/bin/activate`
sh环境：
`. venv/bin/activate`
conda：
创建`conda create -n qa-query-intent python=3.10`
激活`conda activate qa-query-intent`
2. 查看
`which python`
`conda -version`
3. 退出虚拟环境
`deactivate`
#### 项目补装依赖
`pip install -r requirements.txt`
### 其他
1. 主机名称：
`hostname`
2. IP地址：
`windows+R+cmd+ipconfig+IPV4`
3. 张量

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/jJhxeqkbHelZUw8z.jpeg)

5. pycharm远程开发/JetBrains Gateway
6. 
- .sh文件是shell脚本文件；
- bash命令执行脚本；
- deployment.xml记录项目配置，保存本地文件和远程服务器文件的映射关系；
6. 强制删除 JetBrains 系列软件（如 IDEA、PyCharm、WebStorm 等）的本地缓存文件:
`rm -rf ~/.cache/JetBrains/*`
7. powershell进入192.168.3.2：
`ssh cuiwenyue@192.168.3..2 -p 22`
8. `ps -ef|grep JetBrains|grep cui|awk '{print $2}'|xargs kill`
- `ps -ef`查看系统所有进程，f表示完整格式；
- `grep`文本过滤命令；
- `awk`按空格/制表符分隔每行内容；
- `'{print $2}'`只输出第2列，并转化为纯PID数字；
- `xargs kill`将前一个命令的输出作为kill终止进程的输入；
9. crul命令：传输数据，支持多种协议。
`crul [options] [URL]`
# 法律条文向量化项目
## 出现并解决的问题
1. torch安装：`nvidia-smi`查看cuda版本并选择官网对应命令
2.  `nvidia-smi` 显示的是驱动支持的最高 CUDA 版本
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/5hsHdkBm11yWal1r.png)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/T3CVvvBP95I1QcBK.png)

pytorch官网稳定版只发行到13.0，13.0可以向下兼容。
4. 针对 Flask 等 Web 框架提供的框架专属导航 / 快捷操作功能

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/JspEG2mUsMOB1i4M.png)

5. 该结果表示执行脚本时必须传入一个端口号（PORT）作为参数，例如`bash startup.sh 8080`

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/jcZRkXFI4k8tdvn8.png)

这个代码里标定的端口13020只在直接运行 `python server.py` 时生效

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/eiWGQ9TIRvj4Cu1U.png)

而项目里的 `startup.sh` 启动脚本，是用 `gunicorn` 来启动服务的，它会覆盖这个端口设置，使用执行脚本时传入的端口参数。
7. 运行`server.py`的工作目录不对。在终端里先 `cd` 到项目的真实 `src/law_vector/server` 目录，再执行 `python server.py`

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/vVJKmEeES2Leq2E2.png)

问题出在Python 解释器找不到 `law_vector` 这个模块的路径，项目的上层根目录未被添加到搜索路径中，解决方法是人为添加，例如：`export PYTHONPATH=/home/cuiwenyue/law_text_vectorization/src`

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/I9Yh1UavKTWN2ISi.png)

8. 列出系统中所有进程的完整信息，从进程列表中过滤出包含 `278570` 关键字的进程行

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/t28PUg15vtwC1OYj.png)

进程所属用户，目标进程PID，父进程PID，CPU占用率，进程启动时间，关联终端，累计占用CPU时间，启动进程的完整命令。
11. 运行调试配置
- 用 `module` 模式运行，相当于在终端执行 `python -m law_vector.server.server`，它把 `law_vector/server/` 这个目录当作一个 Python 模块来启动

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/03SRZpqU2MDNOiYd.png)

- 用 `script` 模式运行，相当于在终端执行 `python src/law_vector/server/server.py`，它直接把 `server.py` 作为一个独立脚本运行

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/6lMOM9jDFiCi6SlG.png)

9. `server.py` 里的路由定义为`@app.post()` 括号里的路径，这是需要用的真实接口地址

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/8JlOpPGeF7xu1mZH.png)

例如：接口地址：`/law_query_vector_base`crul命令代码为：
`curl -X POST http://localhost:13020/law_query_vector_base \
-H "Content-Type: application/json" \
-d '["宠物狗咬伤人主人要承担什么责任", "离婚时夫妻共同财产如何分割"]'`
## 函数学习
`from...import...`是 Python 的导入语法，表示「从某个模块中，只导入指定的子模块 / 类 / 函数

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/4E8pY1TnUMWIqGB0.jpeg)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/3PoBuxo4bWsKr0Vz.jpeg)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/85jKU9v30F6gfkS6.jpeg)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/bkASsAl9xhfTlfhz.jpeg)

把需要启用的模块enable=True，启用相对应的模型，模型路径在根目录找。
# 意图识别项目
## 出现并解决的问题
1. 权限不足

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/uuepxyLWPTrWH8bW.png)

3. log_dir和data_dir自己定义，预训练模型在huggingface中现存，下载的目录即为配置文件中的路径

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/2mlYHxyjrBUFyJnC.png)

4. 尝试导入的 `_distutils_hack` 模块缺失，通常是因为 `setuptools` 包安装不完整、版本冲突。
- 先激活虚拟环境`conda activate qa-query-intent`
- 强制重新安装 setuptools`pip install --force-reinstall setuptools`

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/1mPfVigFgWfkvIMn.png)

- `_distutils_hack` 不是一个可以直接用 `pip` 安装的独立包

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/C6Lu9RWNMqeqmRSU.png)

4. 环境里缺少了 `accelerate` 库，或者版本低于 `transformers` 库的要求。激活虚拟环境之后，`pip install transformers[torch]`。

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/tKEE7yttfyMloneb.png)

5. `train_file_path = DATA_ROOT + "train.csv" # 训练数据文件地址 
eval_file_path = DATA_ROOT + "eval.csv" # 验证数据文件地址`
在配置文件中定义的`log_dir=/tmp/data`之后没有跟/，导致拼接之后生成并不存在的datatrain.csv，正确格式应该是`log_dir=/tmp/data/`

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/xEiApENPSHTF2tnI.png)

6. 代码里执行了 `evaluate.load("accuracy.py")`，但 `evaluate` 库在它自己的内置指标目录和项目根目录下都没找到这个文件。它的查找路径是 `/home/cuiwenyue/qa-query-intent/accuracy.py`，而 `accuracy.py` 实际在 `src/query_intent/serve/` 目录里。

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/zKvLebDh8nCMIU7X.png)

使用绝对路径:
`# 获取当前文件所在目录 current_dir = os.path.dirname(os.path.abspath(__file__)) `
`# 拼接得到 accuracy.py 的绝对路径 accuracy_path = os.path.join(current_dir, "accuracy.py")`
修改代码如下：

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/GUtnfWzgyXkgoA9a.png)

7. CSV 文件里的列名和 `load_dataset()` 期望加载的列名不匹配。要注意csv文件是否放在配置文件定义的`log_dir=/tmp/data/`下，这个路径中的训练集和测试集是否更新。

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/w8acXlyoNpUZZtQZ.png)

8. 跟训练数据集匹配只需修改数字ID对应的训练标签内容，训练的只是数字，与中英文不匹配无关：

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/JNCUKAaGZDmnY6zM.png)

9. 修改表头标签内容在这里：例如表头为question和intent：

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/Yt9AeVaxcYPfJ1vc.png)

10. 如果是有空行的数据集，不拆分为train.csv和eval.csv：

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/Ck954JdUV2XKb4G8.png)

11. 混用了数据集变量，数据集拆分之后仍使用了原数据集的名称导致报错

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/A34zSrRStjtKX9x6.png)

12. 模型训练过程本身是成功的（16 个 epoch 跑完了），但训练结束保存模型权重时失败了。报错根源是模型的部分张量（tensor）不是「连续内存存储」的（non contiguous），而 `safetensors`（Hugging Face 默认的权重保存库）要求保存的张量必须是连续的，因此触发`ValueError`中断。

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/14ecluV8O2G94wAJ.png)

解决：

![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-04/jNgok6xU6EzHXzjK.png)

## 函数学习
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/pBf18sz16pH75J7G.jpeg)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/ZAFMnlOsaaU51lW0.jpeg)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/Ij1BoCZnXZYR4KSk.jpeg)
![输入图片说明](https://raw.githubusercontent.com/wenyuecui/sum/main/imgs/2026-02-03/k11b7N1gOyquT6gh.jpeg)

# 虚拟环境建立与jupyter notebook安装

## 1. 部署虚拟环境

1. 创建虚拟环境

   ```shell
   conda create -n name python=3.6
   ```

2. 进入虚拟环境

   ```shell
   conda activate name
   ```

   第一次只能使用

   ```
   source activate name
   ```

   不知为何

3. 离开虚拟环境

   ```shell
   conda deactivate
   ```

## 2. 配置jupyter notebook

安装jupyter notebook与ipython（进入虚拟环境前）

```shell
pip install jupyter notebook
pip install ipython
```

为了远程使用jupyter notebook，需要配置jupyter notebook，先生成配置文件

```shell
jupyter notebook --generate-config
```

远程使用jupyter notebook要求配置密码，先进入ipython，然后输入

```python
from IPython.lib import passwd
passwd()
```

输入两次密码（密码输入时不可见）

保存输出的密钥

配置服务器文件

```shell
$ vim ~/.jupyter/jupyter_notebook_config.py
```

在末尾添加信息

```shell
c.NotebookApp.ip = '*' #所有绑定服务器的IP都能访问
c.NotebookApp.port = 9876 #请勿设置为8888，与电脑端访问冲突，9001我占用了
c.NotebookApp.password = u'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed' #''内为ipython输出的密钥
c.NotebookApp.open_browser = False #服务器gpu服务器直接打开会卡死，禁止自动打开
c.NotebookApp.notebook_dir = '/public/liushuo' #这里是设置Jupyter的根目录
```

vim搜索是否有remote（老版本jupyter会有远程访问限制），如有远程访问后改为true

```
/remote
```

启动：命令行输入

```
jupyter notebook
```

![image-20211011170003550](C:\Users\shor\AppData\Roaming\Typora\typora-user-images\image-20211011170003550.png)

http://172.16.132.237:9001/即为我的jupyter访问地址

只要保持shell运行，即可在校园网内其他设备访问

## 3. 虚拟环境激活jupyter

进入虚拟环境，下载ipykernel

```shell
conda install ipykernel
```

输入

```shell
python -m ipykernel install --name yourname
```

将yourname改成你想要的kernel名字

进入jupyter notebook

![image-20211011170502525](C:\Users\shor\AppData\Roaming\Typora\typora-user-images\image-20211011170502525.png)

选择你的kernel，即可运行


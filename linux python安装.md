#### linux python安装



- 现在官网下载需要的python安装包并传输到服务器指定目录（目录位置自定义）

  也可直接通过wget https://www.python.org/ftp/python/3.10.14/Python-3.10.14.tar.xz 在服务器路径下进行下载，wget后的网址是想要下载安装的tar.gz包的地址，在官网中选择自己想要下载的包右键复制即可

- 解压压缩包

  ```python
  tar -Jxvf Python-3.9.0.tar.xz
  ```

- 进入文件夹

  ```python
  cd Python-3.9.0
  ```

- 配置安装位置

  ```pytho
  ./configure prefix=/usr/local/python3
  ```

- 安装

  ```
  make && make install
  ```

  安装成功后，在/usr/local/目录下会有python3目录

- 添加软连接

  ```
  # 添加python3软连接
  ln -s /usr/local/python3/bin/python3 /usr/local/bin/python3
  
  # 添加pip3软连接
  ln -s /usr/local/python3/bin/pip3 /usr/local/bin/pip3
  ```

配置成功后，在任意目录输入python3 -V可以查看python版本





#### 创建虚拟环境



- 安装virtualenv和virtualenvwrapper

  ```
  pip3 install virtualenv
  pip3 install virtualenvwrapper
  ```

- 配置环境变量，编辑bashrc文件

  ```
  vim /root/.bashrc  // root是用户名，根据实际情况填写
  ```

- 添加如下内容

  ```
  export WORKON_HOME=/root/python_even   // 虚拟环境文件夹
  export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3   //python路径
  source /usr/local/python3/bin/virtualenvwrapper.sh  // virtualenvwrapper.sh路径
  ```

  

- 使环境变量生效

  ```
  source /root/.bashrc
  ```

  

- 创建虚拟环境

  ```
  mkvirtualenv env1
  ```

- 当看到命令行前方显示(env1)表示已经激活虚拟环境，若未激活，执行woerkon env1命令即可

- 查看虚拟环境列表

  ```
  workon
  ```

  

- 选择虚拟环境

  ```
  woerkon gjdatac_env
  ```

  


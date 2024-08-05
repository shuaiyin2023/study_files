#### linux anaconda安装





- 下载需要的包

- 赋权

  ```
  chmod +x Anaconda3-2024.02-1-Linux-x86_64.sh
  ```

- 执行安装程序

  ```
  ./Anaconda3-2024.02-1-Linux-x86_64.sh
  ```

- 一直按Enter，有yes的地方输入yes

- 如果没有设置环境变量，需要设置环境变量

  - 一般anaconda安装路径在用户目录的anaconda3

  - 进入安装目录，执行vi  ~/.bashrc打开配置文件

  - 编辑~/.bashrc文件，将anaconda的安装路径添加到文件中

    ```
    export PATH=/root/anaconda3/bin:$PATH
    ```

  - 运行命令，使环境变量生效

    ```
    source ~/.bashrc
    ```

- 检查是否安装成功

  ```
  conda -V
  ```

  
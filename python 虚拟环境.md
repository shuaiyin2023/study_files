# python 虚拟环境

- python -m venv env1    系统环境创建
- 进入虚拟环境的Scripts文件夹，运行 .\activate，激活虚拟环境
- 再虚拟环境中安装相关项目所需第三方包





#### 问题总结

在linux中遇到如下问题时：

在普通用户中创建不了虚拟环境，只能在root用户中创建

- 问题原因：普通用户权限不够

  - 切换到root用户，为普通用户添加权限

    ```
    visudo
    ```

  - 使用上述命令，在sudoers文件中，找到类似于`root ALL=(ALL:ALL) ALL`的行，然后在下面添加以下行以为用户shuaiyin添加sudo权限：

    ```
    bash
    
    shuaiyin    ALL=(ALL:ALL) ALL
    ```

  - 返回已设置权限的用户，再次执行创建虚拟环境的命令

    ```
    sudo python3 -m venv env1
    ```

  - 即可创建环境






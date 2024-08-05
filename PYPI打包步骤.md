# python代码打包发布到PYPI

需要在虚拟环境中安装如下包：

```python
pip install setuptools wheel
pip install twine
```



- 构建文件目录

  - 创建一个文件名mypackage(名称可自定义)
  - 在mypackage目录下创建一个setup.py文件（此文件名必须固定）
  - 在mypackage目录下再创建一个文件夹inner_package(和mypackage一样，名称可以自定义)，用于存放代码文件，以及代码中所需要的其他文件，例如封装的函数、数据字典等信息
  - 再inner_package目录下创建__init__.py（前后双下划线）文件，用于表示这是一个包

  目录结构如下图：
  ![image-20240729153218502](C:\Users\shuaiyin\AppData\Roaming\Typora\typora-user-images\image-20240729153218502.png)

  

- 各文件用途

  - 根目录：用于存放子目录和setup.py文件，以及其他的一些说明文档等

  - setup.py文件：用于存放包相关的信息说明

    ```python
    from setuptools import setup, find_packages
    
    with open('description_info.md', 'r', encoding='utf-8') as f:
        long_description = f.read()
    
    setup(
        name='my-test-gj-package',  # 你的包名
        version='0.0.3',  # 版本号
        description='测试包1',  # 包的简要描述
        long_description=long_description,  # 包的详细描述
        long_description_content_type='text/markdown',  # 描述文件的类型
        include_package_data=True,  # 包含包数据
        package_data={'my-test-gj-package': ['*.py', 'dict_data.py', 'dolphin_db_info.py']},  # 指定数据文件
        author='yin',  # 作者姓名
        author_email='2018209921@qq.com',  # 作者邮箱
        packages=find_packages(),  # 自动查找包目录
        python_requires='>3.6',  # python版本要求
        install_requires=[
            'dolphindb==3.0.1.0',
            'holidays==0.53',
            'numpy==1.26.3',
            'pandas==2.2.0'
        ],  # 依赖库列表 (除开python自带的包外的其他依赖库(代码中如果缺少了对应的库会导致无法运行的包))
    )
    
    ```

  - 子目录：用于存放代码文件及__init__.py文件

  - __init__.py文件：用于导入需要展示给用户的信息，接口等

    ```python
    from .data_api_class import GJDataC
    
    __all__ = ['GJDataC']
    
    ```

    

- 按照上面的方法构造好文件目录及文件内容后，切换到外层目录路径下（mypackage目录下）

  - 执行命令

  ```
  python setup.py sdist bdist_wheel
  ```

  执行成功后，会在根目录下生成一下文件：

  ![image-20240729160309450](C:\Users\shuaiyin\AppData\Roaming\Typora\typora-user-images\image-20240729160309450.png)
  - 上一步执行成功后，在继续在同样目录位置执行以下命令

    ```
    twine upload dist/* 
    ```

    > 会提示需要输入pypi的token，注册账号后，网上搜索教程生成即可

- 





- 检查目录结构

  ```
  gjdatac_project/
      setup.py
      gjdatac_project/
          __init__.py
          ...其他文件...
  ```

  





## 注意

![image-20240729164336239](C:\Users\shuaiyin\AppData\Roaming\Typora\typora-user-images\image-20240729164336239.png)

打包好后，在代码中使用包时，包名是左边红色方框中的包名，而不是右边setup.py文件中设置的名称，

在setup文件中设置包名称时，建议和文件目录的包名保持一致


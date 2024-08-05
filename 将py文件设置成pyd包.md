在linux环境中，生成的包后缀为.so，windows环境下后缀为pyd（下面是linux环境）

- 编写setup.py文件方式:

  ```python
  from distutils.core import setup
  from Cython.Build import cythonize
  import sys,os,traceback
  
  setup(name='TargetCompute', ext_modules=cythonize('target_compute.py'))
  
  ```

  name: 想要保存的包名

  target_compute.py: 想要保存成pyd包的py文件

- 命令行方式：

  将需要打包的.py文件和setup.py文件放在同一文件夹，打开终端，使用命令:

  ```python
  python create.py build_ext --inplace
  # ~/.conda/envs/test/bin/python create.py build_ext --inplace
  ```
  
>注意：需要进入该目录，再执行命令
  
执行后，会在文件夹中生成以下文件：
  
![image-20240129162146174](C:\Users\shuaiyin\AppData\Roaming\Typora\typora-user-images\image-20240129162146174.png)
  
target_compute.so本来叫target_compute.cpython-39-x86_64-linux-gnu.so，将中间的删掉，只保留文件名和后缀名即可
  
- 调用封装好的包

  ```python
  # 导入刚才封装好的包
  from target_compute import TargetCompute
  
  final_result = TargetCompute()
  start_date = "20210901"  # 开始时间 
  end_date = "20231002"  # 结束时间
  breed_list = ["IF", "IC"]  # 品种列表
  n = 2  # 间隔天数，不传递默认为1
  
  # 调用方法计算所有指标（返回的结果是一个字典，根据相应的key获取相应指标的值即可）
  previous_result = final_result.compute_result_by_breed(start_date, end_date, breed_list, n)
  previous_result["revisionary_right_data"].dropna(subset=['price'], inplace=True)
  
  # 前复权的数据
  revisionary_right_data = previous_result["revisionary_right_data"].loc[:, ["underlying_symbol", "date", "dominant_id", "close", "prev_close", "yield", "price"]]
  revisionary_right_data.to_csv("revisionary_right_data.csv", index=True)
  
  ```

  


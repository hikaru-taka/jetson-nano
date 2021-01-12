# JetPack4.4.1 関連


## TensorFlow インストール

### 依存パッケージのインストール
```bash
$ sudo apt-get update
$ sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
$ sudo apt-get install python3-pip
$ sudo pip3 install -U pip testresources setuptools==49.6.0
$ sudo pip3 install cython
$ sudo pip3 install -U numpy==1.16.1 future==0.18.2 mock==3.0.5 h5py==2.10.0 keras_preprocessing==1.1.1 keras_applications==1.0.8 gast==0.2.2 futures protobuf pybind11
```
h5pyのコンパイル時に下記のエラーが出る場合があるので、あらかじめcythonをインストールしている。
```
    h5py/h5a.pyx:184:36: Cannot convert 'void *' to Python object
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-bn0pp4ok/h5py/setup.py", line 159, in <module>
        cmdclass = CMDCLASS,
      File "/usr/lib/python3/dist-packages/setuptools/__init__.py", line 129, in setup
        return distutils.core.setup(**attrs)
      File "/usr/lib/python3.6/distutils/core.py", line 148, in setup
        dist.run_commands()
      File "/usr/lib/python3.6/distutils/dist.py", line 955, in run_commands
        self.run_command(cmd)
      File "/usr/lib/python3.6/distutils/dist.py", line 974, in run_command
        cmd_obj.run()
      File "/usr/lib/python3/dist-packages/setuptools/command/install.py", line 61, in run
        return orig.install.run(self)
      File "/usr/lib/python3.6/distutils/command/install.py", line 589, in run
        self.run_command('build')
      File "/usr/lib/python3.6/distutils/cmd.py", line 313, in run_command
        self.distribution.run_command(command)
      File "/usr/lib/python3.6/distutils/dist.py", line 974, in run_command
        cmd_obj.run()
      File "/usr/lib/python3.6/distutils/command/build.py", line 135, in run
        self.run_command(cmd_name)
      File "/usr/lib/python3.6/distutils/cmd.py", line 313, in run_command
        self.distribution.run_command(command)
      File "/usr/lib/python3.6/distutils/dist.py", line 974, in run_command
        cmd_obj.run()
      File "/tmp/pip-build-bn0pp4ok/h5py/setup_build.py", line 209, in run
        language_level=2)
      File "/tmp/pip-build-bn0pp4ok/h5py/.eggs/Cython-3.0a6-py3.6.egg/Cython/Build/Dependencies.py", line 1110, in cythonize
        cythonize_one(*args)
      File "/tmp/pip-build-bn0pp4ok/h5py/.eggs/Cython-3.0a6-py3.6.egg/Cython/Build/Dependencies.py", line 1277, in cythonize_one
        raise CompileError(None, pyx_file)
    Cython.Compiler.Errors.CompileError: /tmp/pip-build-bn0pp4ok/h5py/h5py/h5a.pyx
```

### インストール
Version 2系をインストール
```bash
$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 tensorflow
```

Version 1系をインストール
```bash
$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 'tensorflow<2'
```

インストール時に、下記のようなエラーが出る場合は、`--no-cache-dir`オプションを追加して実行する。
```
requests.exceptions.HTTPError: 404 Client Error: Not Found for url: https://developer.download.nvidia.com/compute/redist/jp/v44/google-pasta/
```

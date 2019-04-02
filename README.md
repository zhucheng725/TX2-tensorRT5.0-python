# TX2-tensorRT5.0-python

1.Install JetPack4.2(including tensorrt5.0)

2.You can see the example:
/usr/src/tensorrt/samples/python/end_to_end_tensorflow_mnist

3.Install pycuda
```
$ sudo pip3 install pycuda
```
<br>
4.convert pb to uff<br>

```
import uff
print(uff.__path__)
```
<br>
['/usr/lib/python3.6/dist-packages/uff']<br>

```
python3 /usr/lib/python3.6/dist-packages/uff/bin/convert_to_uff.py --input_file = 'your_xxx.pb_path'
```
<br>

Change from .pb to .uff successfully.

5.create the .engine
```
with open(“sample.engine”, “wb”) as f:
    f.write(engine.serialize())
```
<br>

6.use the .engine
```
with open(“sample.engine”, “rb”) as f, trt.Runtime(TRT_LOGGER) as runtime:
    engine = runtime.deserialize_cuda_engine(f.read())
```
<br>

7.See the difference of calculating time between sample.py and use_engine.py
```
$ python3 sample.py
$ python3 use_engine.py
```

![image](https://github.com/zhucheng725/TX2-tensorRT5.0-python/blob/master/difference_calculating_time.png)

Creating .engine can save lots of calculating time.

# TensorFlow
> https://www.tensorflow.org/

## install
```
# Requires the latest pip
pip install --upgrade pip

# Current stable release for CPU and GPU
pip install tensorflow

# Or try the preview build (unstable)
pip install tf-nightly

```


## Python 虛擬環境來獨立安裝套件，與系統區隔開來

```
1. create virtual environment
$ python3 -m venv --system-site-packages ./venv

2. using the environment
$ source ./venv/bin/activate

3. upgrate pip in venv
$ pip install --upgrade pip
$ pip list

4. if you would exit venv(option)
$ deactivate
```

## 安裝 TensorFlow pip 套件
> https://stackoverflow.com/questions/47068709/your-cpu-supports-instructions-that-this-tensorflow-binary-was-not-compiled-to-u

```
$ pip install --upgrade tensorflow

validate installed status:
$ python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"

$ python -c "import tensorflow as tf;import os;os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2';print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

# TensorFlow

https://hub.docker.com/r/tensorflow/tensorflow

## 启动一个带 TensorFlow 环境的 Jupyter Notebook

```bash
docker run -d \
  --rm \
  --name tf \
  -p 8888:8888 \
  -v /docker-data/tf/notebooks:/tf/notebooks \
  tensorflow/tensorflow:latest-py3-jupyter
```

## 测试

```bash
docker run -it --rm \
  tensorflow/tensorflow:latest-py3-jupyter \
  python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

## 进入容器控制台

```bash
docker run -it tensorflow/tensorflow:latest-py3-jupyter bash
```

## 使用一个临时的 TensorFlow 容器运行当前目录下的 scirpt.py 脚本

运行结束之后容器自动删除

```bash
docker run -it --rm \
  -v $PWD:/tmp \
  -w /tmp \
  tensorflow/tensorflow:latest-py3-jupyter \
  python3 model_train.py 64 100 1>log 2>&1
```

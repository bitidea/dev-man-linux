# TensorFlow

[https://hub.docker.com/r/tensorflow/tensorflow](https://hub.docker.com/r/tensorflow/tensorflow)

## 启动一个带 TensorFlow 环境的 Jupyter Notebook

```bash
docker run -d --rm --name tf \
  -p 8888:8888 \
  -v /docker-data/tf/notebooks:/tf/notebooks \
  tensorflow/tensorflow:latest-py3-jupyter
```

## 测试

```bash
docker run -it --rm \
  tensorflow/tensorflow \
  python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

## 使用一个临时的 TensorFlow 容器运行当前目录下的 model_train.py 脚本

运行结束之后容器自动删除

```bash
docker run -d --rm --name tf \
  -v $PWD:/data \
  -w /data \
  tensorflow/tensorflow:latest \
  bash -c ' pip3 install -U pip -i https://pypi.douban.com/simple && \
  pip3 config set global.index-url https://pypi.douban.com/simple && \
  pip3 install -U tensorflow keras pandas numpy jieba gensim fastapi uvicorn && \
  python3 model_train.py 64 100 false 1>log 2>&1 '
```

## TensorBoard

```bash
docker run -d --rm --name tf-board \
  -p 6006:6006 \
  -v $PWD:/data \
  -w /data \
  tensorflow/tensorflow:latest \
  tensorboard --logdir logs/fit --host 0.0.0.0 --port 6006
```

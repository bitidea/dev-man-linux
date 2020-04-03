# 树莓派编译 Hadoop 2.7.7 Native Library

## JDK 8

如果已经装了可以跳过

```bash
sudo apt -y install openjdk-8-jdk
```

要设置 `JAVA_HOME` 环境变量

## 依赖库

```bash
sudo apt -y install maven
sudo apt -y install build-essential autoconf automake libtool cmake zlib1g-dev pkg-config libssl1.0-dev
sudo apt -y install snappy libsnappy-dev
sudo apt -y install bzip2 libbz2-dev
sudo apt -y install libjansson-dev
sudo apt -y install fuse libfuse-dev
```

注意 `libssl` 的版本必须是 `1.0`

## 解压源码

```bash
tar xvf hadoop-2.7.7-src.tar.gz
```

## 给源码打补丁

```bash
cd hadoop-2.7.7-src/hadoop-common-project/hadoop-common/src/
wget https://issues.apache.org/jira/secure/attachment/12570212/HADOOP-9320.patch
patch < HADOOP-9320.patch
cd ..
```

## 开始编译

```bash
mvn compile -Pnative -T4
```

## 检查结果

```bash
ls target/native/target/usr/local/lib/
# libhadoop.a  libhadoop.so  libhadoop.so.1.0.0
```

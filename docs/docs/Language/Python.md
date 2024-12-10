# 虚拟环境
## 安装虚拟环境库
```bash
pip install install virtualenv
```

## 创建虚拟环境
`exampleEnv`为虚拟环境名

```bash
virtualenv exampleEnv
```

## 使用虚拟环境
```bash
source exampleEnv/bin/activate
```

## 退出虚拟环境
windows可能需要在后面加上.bat

```bash
deactive
```

## 删除虚拟环境，也就是删除这个虚拟环境目录
```bash
rm -rf ./exampleEnv
```

## 创建制定版本的虚拟环境
```bash
virtualenv -p python2.7 exampleEnv
```



# PIP
安装requirements.txt中的依赖

```bash
pip install -r requirements.txt
```



# 配置国内镜像源
## 本次安装使用
```bash
pip install -i http://mirrors.aliyun.com/pypi/simple Pillow
```

## 全局
```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```



# 语法相关
如果你想在python中向下取整应当使用`a//b`取整的除法，而不是`int(a/b)`

当`a`非常大的时候，这个除法的精度会不够，再转成int后，是不对的结果


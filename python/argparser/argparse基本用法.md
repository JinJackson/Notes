# argparse基本用法

argparse 是python自带的命令行参数解析包，可以用来方便地读取命令行参数。它的使用也比较简单。

#### >1.从命令行获取用户名

>```python
>parser.add_argument('--name', default='Great')
>$ python print_name.py --name Wang
>args = parser.parser_args()
>arg.name  #Wang
>```

#### 2.action参数

> 用argparse模块让python脚本接收参数时，对于**True/False**类型的参数，向add_argument方法中加入参数action=‘store_true’/‘store_false’。

```python
parser = argparse.ArgumentParser()
parser.add_argument('--foo', action='store_true')  #传参则为true，默认false
parser.add_argument('--bar', action='store_false') #传参则为false，默认true
parser.add_argument('--baz', action='store_false') #传参则为false，默认true

#如果默认不传参，
Namespace(Namespace(bar=True, baz=True, foo=False))
```



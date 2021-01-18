# argparse模块

开始写稍微大一点的项目的时候就发现人家都是用argparse的，在命令行跑代码，很酷（

以下都是抄的[知乎原文](https://zhuanlan.zhihu.com/p/56922793)，写得非常清晰！

## 传入一个参数

```
import argparse

parser = argparse.ArgumentParser(description='命令行中传入一个数字')
#type是要传入的参数的数据类型  help是该参数的提示信息
parser.add_argument('integers', type=str, help='传入的数字')

args = parser.parse_args()

#获得传入的参数
print(args)
```

## 操作args字典

```
print(args.integers)
```

## 传入多个参数

```
parser.add_argument('integers', type=str, nargs='+',help='传入的数字')
```

**nargs**是用来说明传入的参数个数，'+' 表示传入至少一个参数。

## 改变数据类型

```
parser.add_argument('integers', type=int, nargs='+',help='传入的数字')
```

直接改type参数即可

## 位置参数

在命令行中传入参数时候，传入的参数的先后顺序不同，运行结果往往会不同，这是因为采用了位置参数，例如

```text
import argparse

parser = argparse.ArgumentParser(description='姓名')
parser.add_argument('param1', type=str, help='姓')
parser.add_argument('param2', type=str, help='名')
args = parser.parse_args()

#打印姓名
print(args.param1+args.param2)
```

如果我们将代码`parser.add_argument('param1', type=str,help='姓')`和`parser.add_argument('param2', type=str,help='名')`互换位置，即第4行和第五行代码，再重新运行，打印出来的姓名是反的。

## 可选参数

```
parser.add_argument('--family', type=str,help='姓')
parser.add_argument('--name', type=str,help='名')
```

在关键词前面加上--

在命令行中输入（输入变麻烦了，但是增加了命令行中的可读性，不容易因为参数传入顺序导致数据错乱。）

```text
python demo.py --family=张 --name=三
```

运行结果

```text
张三
```

## 默认值

add_argument的default参数

```text
import argparse

parser = argparse.ArgumentParser(description='姓名')
parser.add_argument('--family', type=str, default='张',help='姓')
parser.add_argument('--name', type=str, default='三', help='名')
args = parser.parse_args()

#打印姓名
print(args.family+args.name)
```

在命令行中分别输入 `python demo.py` 、 `python demo.py --family=李`

运行结果分别为

```text
张三
```

和

```text
李三
```

## 必需参数

add_argument的required参数

```text
parser.add_argument('--family', type=str, help='姓')
parser.add_argument('--name', type=str, required=True, default='', help='名')
```

## Reference:

argparse模块用法实例详解 https://zhuanlan.zhihu.com/p/56922793
+++
title = "符合python风格的对象"
date = "2019-05-22T10:23:52+08:00"
toc = true
tags = ["流畅的python", "learning"]
categories = ["Python", "流畅的python", "第九章"]
#mathjax = null  # To use: uncomment and replace null with value
description = ""
+++


得益于 Python 数据模型，自定义类型的行为可以像内置类型那样自然。实现如自然的行为，靠的不是继承，而是鸭子类型（duck typing）：我们只需按照预定行为实对象所需的方法即可。

<!--more-->

# 1.特殊方法

repr()
　　以便于开发者理解的方式返回对象的字符串表示形式。
str()
　　以便于用户理解的方式返回对象的字符串表示形式。

bytes()
　　调用它获取对象的字节序列表示形式

\__format__ 方法会被内置的 format() 函数和 str.format() 方法调用
　　使用特殊的格式代码显示对象的字符串表示形式

 print 函数会调用 str 函数

 bytes 函数会调用 \__bytes__ 方法，生成实例的二进制表示形式。

 abs 函数会调用 \__abs__ 方法，返回实例的模。

 bool 函数会调用 \__bool__ 方法，如果实例的模为零，返回 False，否则返回 True。

```python
from array import array
import math
class Vector2d:
    typecode = 'd'  #  typecode 是类属性，在 Vector2d 实例和字节序列之间转换时使用。
    def __init__(self, x, y):
        self.x = float(x)   # 在 __init__ 方法中把 x 和 y 转换成浮点数，尽早捕获错误，以防调用 Vector2d 函数时传入不当参数。
        self.y = float(y)
    def __iter__(self):
        return (i for i in (self.x, self.y))  # 定义 __iter__ 方法，把 Vector2d 实例变成可迭代的对象，这样才能拆包（例如，x, y = my_vector）。这个方法的实现方式很简单，直接调用生成器表达式一个接一个产出分量。
    def __repr__(self):
        class_name = type(self).__name__
        return '{}({!r}, {!r})'.format(class_name, *self)  #__repr__ 方法使用 {!r} 获取各个分量的表示形式，然后插值，构成一个字符串；因为 Vector2d 实例是可迭代的对象，所以 *self 会把 x 和 y 分量提供给 format 函数。
    def __str__(self):
        return str(tuple(self))  # 从可迭代的 Vector2d 实例中可以轻松地得到一个元组，显示为一个有序对。
    def __bytes__(self):
        return (bytes([ord(self.typecode)]) +  # 为了生成字节序列，我们把 typecode 转换成字节序列，然后……
                bytes(array(self.typecode, self)))  # ……迭代 Vector2d 实例，得到一个数组，再把数组转换成字节序列。
    def __eq__(self, other):
        return tuple(self) == tuple(other)  # 为了快速比较所有分量，在操作数中构建元组。对 Vector2d 实例来说，可以这样做，不过仍有问题。参见下面的警告。
    def __abs__(self):
        return math.hypot(self.x, self.y)  #模是 x 和 y 分量构成的直角三角形的斜边长。
    def __bool__(self):
        return bool(abs(self))  # __bool__ 方法使用 abs(self) 计算模，然后把结果转换成布尔值，因此，0.0 是False，非零值是 True。
```

# 2.格式化显示

内置的 format() 函数和 str.format() 方法把各个类型的格式化方式委托给相应的.\__format__(format_spec) 方法。format_spec 是格式说明符，他是：

+ format(my_obj, format_spec) 的第二个参数，或者
+ str.format() 方法的格式字符串，{} 里代换字段中冒号后面的部分

```python
>>> brl = 1/2.43  # BRL到USD的货币兑换比价
>>> brl
0.4115226337448559
>>> format(brl, '0.4f')  #  格式说明符是 '0.4f'。
'0.4115'
>>> '1 BRL = {rate:0.2f} USD'.format(rate=brl)  #  格式说明符是 '0.2f'。代换字段中的 'rate' 子串是字段名称，与格式说明符无关，但是它决定把 .format() 的哪个参数传给代换字段。
'1 BRL = 0.41 USD'
```

'{0.mass:5.3e}' 这样的格式字符串其实包含两部分，冒号左边的 '0.mass' 在代换字段句法中是字段名，冒号后面的 '5.3e' 是格式说明符

格式说明符使用的表示法叫格式规范微语言

## 格式描述

```python
fill 
可以是任意字符，默认为空格。

align 
仅当指定最小宽度时有效。

< 左对齐（默认选项）
> 右对齐
= 仅对数字有效；将填充字符放到符号与数字间，例如 +0001234
^ 居中对齐
sign 
仅对数字有效

+ 所有数字均带有符号
- 仅负数带有符号（默认选项）
 即空格；正数前面带空格，负数前面带符号
'#' 
只对整数有效

自动在二进制、八进制、十六进制数值前添加对应的 0b、0o、 0x。

',' 
自动在每三个数字之间添加 , 分隔符。

width 
十进制数字，定义最小宽度。如果未指定，则由内容的宽度来决定。

如果没有指定对齐方式（align），那么可以在 width 前面添加一个0来实现自动填充0，等价于 fill 设为 0 并且 align 设为 =。

precision 
用于确定浮点数的精度，或字符串的最大长度。不可用于整型数值。

type 
确定参数类型，默认为 s ，即字符串。

整数输出类型：

b：以二进制格式输出
c：将整数转换成对应的 unicode 字符
d：以十进制输出（默认选项）
o：以八进制输出
x：以十六进制小写输出
X：以十六进制大写输出
n：与 d 相同，但使用当前环境的分隔符来分隔每3位数字
十进制浮点数输出类型：

e：指数标记；使用科学计数法输出，用e来表示指数部分，默认 precision 为6
E：与 e 相同，但使用大写 E 来表示指数部分
f：以定点形式输出数值，默认 precision 为6
F：与 f 相同
g：通用格式；对于给定的 precision p >= 1，取数值的p位有效数字，并以定点或科学计数法输出（默认选项）
G：通用格式；与 g 相同，当数值过大时使用 E 来表示指数部分
n：与 g 相同，但使用当前环境的分隔符来分隔每3位数字
%：百分比标记；使用百分比的形式输出数值，同时设定 f 标记

```

格式规范微语言是可扩展的，因为各个类可以自行决定如何解释 format_spec 参数

如果类没有定义 __format__ 方法，从 object 继承的方法会返回 str(my_object)。

然而，如果传入格式说明符，object.__format__ 方法会抛出 TypeError：

示例 Vector2d.__format__ 方法，第 1 版

 ```python
    # 在Vector2d类中定义
    def __format__(self, fmt_spec=''):
        components = (format(c, fmt_spec) for c in self)  # 使用内置的 format 函数把 fmt_spec 应用到向量的各个分量上，构建一个可迭代的格式化字符串。
        return '({}, {})'.format(*components)  # 把格式化字符串代入公式 '(x, y)' 中
 ```

# 3.可散列的Vector2d

目前 Vector2d 实例是不可散列的，因此不能放入集合（set）中

为了把 Vector2d 实例变成可散列的，必须使用 __hash__ 方法（还需要 \__eq__ 方法，前面已经实现了）此外，还要让向量不可变

```python
class Vector2d:
    typecode = 'd'
    def __init__(self, x, y):
        self.__x = float(x)  #使用两个前导下划线（尾部没有下划线，或者有一个下划线），把属性标记为私有
        self.__y = float(y)
    @property  # @property 装饰器把读值方法标记为特性。
    def x(self):  #读值方法与公开属性同名，都是 x
        return self.__x  #直接返回 self.__x
    @property # 以同样的方式处理 y 特性
    def y(self):
        return self.__y
    def __iter__(self):
        return (i for i in (self.x, self.y)) # 需要读取 x 和 y 分量的方法可以保持不变，通过 self.x 和 self.y 读取公开特性，而不必读取私有属性，因此上述代码清单省略了这个类的其他代码。
    def __hash__(self):
    	return hash(self.x) ^ hash(self.y)
    def __eq__(self, other):
        return tuple(self) == tuple(other) 
```

**要想创建可散列的类型，不一定要实现特性，也不一定要保护实例属性。只需正确地实现 hash 和 eq 方法即可。但是，实例的散列值绝不应该变化，因此我们借机提到了只读特性。**

# 4.Python的私有属性和“受保护的”属性

现在，你创建了 Dog 类的子类：Beagle。，如果以  \_\_mood 的形式（两个前导下划线，尾部没有或最多有一个下划线）命名实例属性，Python 会把属性名存入实例的  \_\_dict\_\_ 属性中，而且会在前面加上一个下划线和类名。因此，对 Dog 类来说，\__mood 会变成 _Dog__mood；这个语言特性叫名称改写



但是，只要知道改写私有属性名的机制，任何人都能直接读取私有属性——这对调试和序列化倒是有用。此外，只要编写 v1._Vector__x = 7 这样的代码，就能轻松地为 Vector2d 实例的私有分量直接赋值。

Python 解释器不会对使用单个下划线（如self._x)的属性名做特殊处理，不过这是很多 Python 程序员严格遵守的约定，他们不会在类外部访问这种属性。

（注：像遵守使用全大写字母编写常量）

Python 文档的某些角落把使用一个下划线前缀标记的属性称为“受保护的”属性。  使用self._x 这种形式保护属性的做法很常见，但是很少有人把这种属性叫作“受保护的”属性。有些人甚至将其称为“私有”属性。

# 5.使用 \_\_slots\_\_ 类属性节省空间

默认情况下，Python 在各个实例中名为 __dict__ 的字典里存储实例属性。为了使用底层的散列表提升访问速度，字典会消耗大量内存。如果要处理数百万个属性不多的实例，通过 \_\_slots\_\_ 类属性，能节省大量内存，方法是让解释器在元组中存储实例属性，而不用字典。

```python
class Vector2d:
    __slots__ = ('__x', '__y')
    typecode = 'd'
```

在类中定义 \_\_slots\_\_ 属性的目的是告诉解释器：“这个类中的所有实例属性都在这儿了！”这样，Python 会在各个实例中使用类似元组的结构存储实例变量，从而避免使用消耗内存的 \_\_dict\_\_ 属性。如果有数百万个实例同时活动，这样做能节省大量内存。

如果要处理数百万个数值对象，应该使用 NumPy 数组（参见 2.9.3 节）。NumPy 数组能高效使用内存，而且提供了高度优化的数值处理函数，其中很多都一次操作整个数组。

如果把 '\_\_dict\_\_' 这个名称添加到\_\_slots\_\_ 中，实例会在元组中保存各个实例的属性，此外还支持动态创建属性，这些属性存储在常规的 \_\_dict__ 中。当然，把 '\_\_dict\_\_' 添加到 \_\_slots\_\_ 中可能完全违背了初衷，这取决于各个实例的静态属性和动态属性的数量及其用法。

在类中定义 \__slots_\_ 属性之后，实例不能再有 \__slots__ 中所列名称之外的其他属性。这只是一个副作用，不是 \_\_slots\_\_ 存在的真正原因。不要使用\_\_slots\_\_ 属性禁止类的用户新增实例属性。

**\_\_slots\_\_ 是用于优化的，不是为了约束程序员**



为了让对象支持弱引用（参见 8.6 节），必须有这个属性。用户定义的类中默认就有 \_\_weakref\_\_ 属性。可是，如果类中定义了 \_\_slots\_\_ 属性，而且想把实例作为弱引用的目标，那么要把'\_\_weakref\_\_' 添加到 \_\_slots\_\_ 中

如果使用得当，\_\_slots\_\_ 能显著节省内存，不过有几点要注意。
+ 每个子类都要定义 \_\_slots\_\_ 属性，因为解释器会忽略继承的 \_\_slots\_\_ 属性。
+ 实例只能拥有 \_\_slots\_\_ 中列出的属性，除非把 '\_\_slots\_\_' 加入 \_\_slots\_\_ 中（这样做就失去了节省内存的功效）。
+ 如果不把 '\_\_weakref\_\_' 加入 __slots__，实例就不能作为弱引用的目标。
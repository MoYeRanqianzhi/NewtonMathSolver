# NewtonMathSolver

> 使用牛顿法无限迭代求任意方程近似解

## 基础调用

```python
from NewtonMathSolver import Tolerance, NewtonMathSolver

n = NewtonMathSolver('x - 1 = 10', 'x', 2, Tolerance(level=6))
print(n.iterate(10))
print(n.result)

```

与之等效的是

```python
from NewtonMathSolver import Tolerance, NewtonMathSolver

n = NewtonMathSolver('x - 1 = 10', 'x', 2, 1e-6)
print(n.iterate(10))
print(n.result)

```

## 进一步探究

这样可以看到计算步骤

```python
from NewtonMathSolver import Tolerance, NewtonMathSolver

n = NewtonMathSolver('x - 1 = 10', 'x', 2, Tolerance(level=6))

while 1 + 1 == 2:
    n.iterate()
    print(n.result)
    if n.result.result:
        break

```

### 容忍与误差

使用牛顿法通常会有误差，于是我们会将误差与设定的容忍度进行对比，容忍度即误差允许的最大值

这样可以设定一个可操作的误差

```python
from NewtonMathSolver import Tolerance

t = Tolerance(1e-6)

```

与之等价的是

```python
from NewtonMathSolver import Tolerance

t = Tolerance(level=6)

```

以及

```python
from NewtonMathSolver import Tolerance

t = Tolerance(1e-6, 666)
# 若是同时存在两个参数，则tolerance优先

```

其可以进行多种操作

### 自增

```python
from NewtonMathSolver import Tolerance

t = Tolerance(level=6)
```

以下操作均允许

```python
t + 1
print('t + 1', t)
```

t + 1 1.000001

```python
t - 1
print('t - 1', t)
```

t - 1 9.999999999177334e-07

```python
t * 2
print('t * 2', t)
```

t * 2 1.9999999998354667e-06

```python
t / 2
print('t / 2', t)
```

t / 2 9.999999999177334e-07

```python
t ** 2
print('t ** 2', t)
```

t ** 2 9.999999998354668e-13

```python
t ** (1 / 2)
print('t ** (1 / 2)', t)
```

t ** (1 / 2) 9.999999999177334e-07

```python
t.more()
print('more', t)
```

more 9.999999999177333e-08

```python
t.less()
print('less', t)
```

less 9.999999999177334e-07

### 逻辑运算

```python
print(t == 0)
print(t > 0)
print(t >= 0)
print(t < 1)
print(t <= 1e-7)
```

False
True
True
True
False

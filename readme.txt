learngit# 先定义一个装饰函数（帽子）
# 再定义你的业务函数（人）
# 最后把这顶帽子带在这个人头上

#日志打印器
def logger(func):
	def wrapper(*args,**kw):
		print("开始计算{}函数".format(func.__name__))
		#真的执行的函数
		func(*args,**kw)
		print("执行完毕")

	return wrapper

@logger
def add(x,y):
	print("{}+{}={}".format(x,y,x+y))

# add(10,20)

#. 入门用法：时间计时器

import time
def timer(func):
	def wrapper(*args,**kw):
		t1=time.time()
		func(*args,**kw)
		t2=time.time()
		print("花费时间{}".format(t2-t1))

	return wrapper
@timer
def  xumian():
	time.sleep(1)
# xumian()

# . 进阶用法：带参数的函数装饰器
# 那么装饰器如何实现传参呢，会比较复杂，需要两层嵌套。

def say_hello(contry):
	def wrapper(func):
		def deco(*args,**kw):
			if contry=="china":
				print("你好")
			elif contry=="america":
				print("hello")
			else:
				return
			func(*args,**kw)
		return deco
	return wrapper

@say_hello("america")				
def america():
	print("i like junk food")
@say_hello("china")
def china():
	print("我喜欢好吃的")

# america()
# china()

# 高阶用法：不带参数的类装饰器
# 基于类装饰器的实现，必须实现 __call__ 和 __init__两个内置函数。
# __init__ ：接收被装饰函数
# __call__ ：实现装饰逻辑。

class logger():
	def __init__(self,func):
		self.func=func
	def __call__(self,*args,**kw):
		print("正在运行{func}()函数".format(func=self.func.__name__))
		return self.func(*args,**kw)

@logger
def say(something):
	print("say {}".format(something))
# say("hello")
# 高阶用法：带参数的类装饰器
# __init__ ：不再接收被装饰函数，而是接收传入参数。
# __call__ ：接收被装饰函数，实现装饰逻辑。



class logger1():
    def __init__(self, level='INFO'):
        self.level = level
    def __call__(self, func): # 接受函数
        def wrapper(*args, **kw):
            print("[{level}]: the function {func}() is running..."\
                .format(level=self.level, func=func.__name__))
            func(*args, **kw)
        return wrapper  #返回函数

@logger1(level="warning")
def say(something):
    print("say {}!".format(something))

Git is a distributed version control system.
Git is free software.

# say("hello")


class hh():
	def __init__(self,level="info"):
		self.level=level


	def __call__(self,func):
		def wrapper(*args,**kw):
			print("[{level}正在运行{func}]".format(level=self.level,func=func.__name__))
			func(*args,**kw)
		return wrapper

@hh(level="wraning")
def sya(something):
	print("hahh{}".format(something))
sya("hello")

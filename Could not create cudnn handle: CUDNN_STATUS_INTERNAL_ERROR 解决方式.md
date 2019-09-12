rom tensorflow.compat.v1 import ConfigProto  
from tensorflow.compat.v1 import InteractiveSession  

config = ConfigProto()  
config.gpu_options.allow_growth = True  
session = InteractiveSession(config=config)  

原文链接：https://blog.csdn.net/pkuyjxu/article/details/89402298  

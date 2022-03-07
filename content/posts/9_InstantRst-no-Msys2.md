---
title: 9. InstantRst no Msys2
date: 2017-05-02 11:45:03
tags:
---
### InstantRst on Msys2(发现了更好的替代软件markdown composer）

按照 [riv.vm官网](https://github.com/Rykka/riv.vim)
按照 [InstantRst官网](https://github.com/Rykka/InstantRst)
按照 [instant-rst.py官网](https://github.com/rykka/instant-rst.py)

先在Msys2上用pacman安装好pip，然后用pip按照官网的地址安装InstantRst
vim里用插件工具安装好riv和instantRst.但是这时候vim里:InstantRst只能开服务
不能自动打开浏览器.之前查到问题出在脚本instantRst上.

### HOST问题
cd到/mingw/bin,打开instantRst,找到def browse(b,......)函数,添加bhost参数
``` python
def browse(b, port, filename, bhost):
    time.sleep(1)
    url =  'http://' + bhost + ':'+ port
```

后面调用也要添加bhost参数
``` python
if ag.localhost_only:
    HOST = "localhost"
else:
    # get hostname of local LAN IP
    HOST = socket.gethostbyname(socket.gethostname())

p = Process(target=browse, args=(ag.browser, ag.port, ag.filename, HOST))
```

### 多线程返回问题

instantRst这个脚本开了线程运行服务后,应该返回到原脚本上,但是在Msys2下其返回到
instantRst.py这个文件上,注意啦是多了".py",然后我就复制多一份原来的instantRst并
改为instantRst.py,但因为python的一些问题,要添加freeze_support和rstmain

``` python
from multiprocessing import Process,freeze_support
```
``` python
    
def rstmain():
	ag = args.parse()

	if ag.localhost_only:
	    HOST = "localhost"
	else:
	    # get hostname of local LAN IP
	    HOST = socket.gethostbyname(socket.gethostname())

	p = Process(target=browse, args=(ag.browser, ag.port, ag.filename, HOST))
	p.start()

	try:
	    run(host=HOST, port=int(ag.port),
		template_dir=ag.template_dir,
		static_dir=ag.static_dir,
		additional_dirs=ag.additional_dirs)
	except:
	    print '\nSome error/exception occurred.'
	    print sys.exc_info()
	    p.terminate()
	    sys.exit()

if __name__ == '__main__':
	freeze_support()
	rstmain()

```
简单说就是要将执行的代码放到rstmain里,再在下面调用,这样就可以调出浏览器了啊.
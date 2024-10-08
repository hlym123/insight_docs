显示屏 
======================================================

API: class Display
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    ''' 
     导入模块
    '''
    from maix import display

    '''
     创建显示屏对象(显示屏初始化)
    '''
    dis = display.Display()

    '''
     显示图像 
    '''
    dis.show(self, img: maix.image.Image) 

    '''
     设置背光亮度
     value: 0~100 
    '''
    dis.set_backlight(self, value: float)

    '''
     获取背光亮度
    '''
    dis.get_backlight(self) 

    '''
     设置镜像显示
    '''
    dis.set_hmirror(self, en: bool)

    '''
     设置垂直翻转
    '''
    dis.set_vflip(self, en: bool) 


Example: 绘图显示
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    from maix import image, display, app, time

    # 显示屏初始化
    dis = display.Display()
    dis.set_backlight(60)

    # 加载设置字体
    image.load_font("sourcehansans", "/maixapp/share/font/SourceHanSansCN-Regular.otf", size = 28)
    image.set_default_font("sourcehansans")

    img = image.Image(640, 480) # 创建 640x480 的空白图像
    img.draw_rect(0, 0, dis.width(), dis.height(), color=image.Color.from_rgb(0, 0, 0), thickness=-1) # 画黑色实心矩形
    img.draw_string(10, 10, "Hello World!", color=image.Color.from_rgb(255, 255, 255)) # 画字符串
    dis.show(img) # 显示图像 

    # 保持程序不退出
    while not app.need_exit():
        time.sleep(1)




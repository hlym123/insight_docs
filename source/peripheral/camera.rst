摄像头 
======================================================


API: class camera
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     导入模块
    '''
    from maix import camera

    '''
     创建摄像头对象(摄像头初始化)
     @width 水平分辨率
     @height 垂直分辨率
    '''
    cam = camera.Camera(width, height)

    '''
     读取图像
    '''
    img = cam.read() 

    '''
     设置水平镜像
    '''
    cam.hmirror(mirror) 

    '''
     设置垂直翻转
    '''
    cam.vflip(flip)

    '''
     设置分辨率
     @width 水平分辨率
     @height 垂直分辨率
    '''
    cam.set_resolution(width, height) 

Example: 拍摄显示
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    from maix import camera, display, app

    dis = display.Display()       # 显示屏初始化
    cam = camera.Camera(640, 480) # 摄像头初始化，分辨率设为 640x480

    while not app.need_exit():
        img = cam.read() # 从摄像头读取图像
        dis.show(img)    # 显示拍摄的图像



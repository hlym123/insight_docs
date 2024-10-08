二维码识别
====================================================== 

二维码是一种可以存储大量信息的矩阵条码，最常见的是QR码（Quick Response Code）。它可以存储文字、网址、联系人信息等。



二维码生成
++++++++++++++++++++++++++++++++++++++++++++++++++++++

点击 `二维码生成 <https://cli.im/>`_ 进入二维码生成网站，按下图所示生成自定义的二维码

.. figure:: ./qrcode_create.png
   :width: 800
   :align: center

生成的二维码

.. figure:: ./qrcode_hello.png
   :width: 200
   :align: center


Example: 二维码识别
++++++++++++++++++++++++++++++++++++++++++++++++++++++

运行下面的程序，将摄像头对准二维码可查看二维码信息。

::

    from maix import image, camera, display

    # 加载设置字体
    image.load_font("sourcehansans", "/maixapp/share/font/SourceHanSansCN-Regular.otf", size = 20)
    image.set_default_font("sourcehansans")

    cam = camera.Camera(640, 480) # 摄像头测试化
    disp = display.Display()      # 显示屏初始化

    while 1:
        img = cam.read() # 获取图像
        qrcodes = img.find_qrcodes() # 二维码识别
        for qr in qrcodes: # （可能存在多个二维码）逐个显示二维码信息
            corners = qr.corners() # 获取二维码角点坐标
            for i in range(4):
                img.draw_line(corners[i][0], corners[i][1], corners[(i + 1) % 4][0], corners[(i + 1) % 4][1], image.COLOR_BLUE, thickness=3)
            img.draw_string(qr.x(), qr.y() - 25, qr.payload(), image.COLOR_BLUE) # 绘制二维码信息
        disp.show(img) # 显示图像

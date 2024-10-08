条形码识别
====================================================== 

 

条形码生成
++++++++++++++++++++++++++++++++++++++++++++++++++++++

点击 `二维码生成 <https://cli.im/>`_ 进入二维码生成网站，按下图所示生成自定义的二维码

.. figure:: ./qrcode_create.png
   :width: 800
   :align: center

生成的二维码

.. figure:: ./qrcode_hello.png
   :width: 200
   :align: center


TODO: 案例程序：条形码识别
++++++++++++++++++++++++++++++++++++++++++++++++++++++

运行下面的程序，将摄像头对准条形码识别可查看条形码识别信息。

::

    from maix import image, camera, display

    # 加载设置字体
    image.load_font("sourcehansans", "/maixapp/share/font/SourceHanSansCN-Regular.otf", size = 20)
    image.set_default_font("sourcehansans")

    cam = camera.Camera(320, 240) # 摄像头测试化
    disp = display.Display()      # 显示屏初始化

    while 1:
        img = cam.read()
        barcodes = img.find_barcodes()
        for barcode in barcodes:
            corners = barcode.corners()
            for i in range(4):
                img.draw_line(corners[i][0], corners[i][1], corners[(i + 1) % 4][0], corners[(i + 1) % 4][1], image.COLOR_BLUE, thickness=3)
            img.draw_string(barcode.x(), barcode.y() - 25, barcode.payload(), image.COLOR_BLUE)
        disp.show(img)

AprilTag 识别
====================================================== 

`AprilTag <https://april.eecs.umich.edu/software/apriltag.html>`_ 是一种专门用于机器人视觉中的二进制方形标记。它的设计目标是精确且快速地在复杂环境中进行位置跟踪和姿态估计。

* 每个 AprilTag 标记由一个黑白相间的方形图案组成，内部包含一个唯一的二进制ID。

可点击 `AprilTag <https://pan.baidu.com/s/1CG9cQ27SJ1ec5DFaOl1a4w?pwd=6666>`_ (提取码：6666) 下载。 


.. figure:: ./tag36h11_0.png
   :width: 200
   :align: center

Example: AprilTag 识别
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    from maix import image, camera, display
    import math

    # 加载设置字体
    image.load_font("sourcehansans", "/maixapp/share/font/SourceHanSansCN-Regular.otf", size = 20)
    image.set_default_font("sourcehansans")

    cam = camera.Camera(640, 480) # 摄像头测试化
    dis = display.Display()       # 显示屏初始化

    families = image.ApriltagFamilies.TAG36H11
    x_scale = cam.width() / 160
    y_scale = cam.height() / 120

    while 1:
        img = cam.read() # 获取图像
        new_img = img.resize(160, 120) # 图像缩放到 160x120 便于加快识别速度
        apriltags = new_img.find_apriltags(families = families)
        for a in apriltags: # 逐个 apriltags 显示 
            corners = a.corners() # 获取角点坐标
            for i in range(4):
                corners[i][0] = int(corners[i][0] * x_scale) # 缩放后的图像坐标还原为显示图像坐标
                corners[i][1] = int(corners[i][1] * y_scale)
            x = int(a.x() * x_scale)
            y = int(a.y() * y_scale)
            w = int(a.w() * x_scale)
            h = int(a.h() * y_scale)
            for i in range(4):
                img.draw_line(corners[i][0], corners[i][1], corners[(i + 1) % 4][0], corners[(i + 1) % 4][1], image.COLOR_BLUE, thickness=3)
            tag_info = "id: %d, rotation %d°" %  (a.id(), (180 * a.rotation()) / math.pi)
            img.draw_string(x + w + 20, y, tag_info, image.COLOR_BLUE)
            img.draw_string(x + w + 20, y + 23, "family: " + str(a.family()), image.COLOR_BLUE)
        dis.show(img) # 显示图像






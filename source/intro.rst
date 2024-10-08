入门使用 
======================================================

资料下载 `链接 <https://pan.baidu.com/s/1CG9cQ27SJ1ec5DFaOl1a4w?pwd=6666>`_ (提取码：6666) 

 
驱动安装
++++++++++++++++++++++++++++++++++++++++++++++++++++++

通过 USB 连接设备到电脑，一般会自动安装驱动。查看驱动安装情况可用鼠标移动到我的电脑，点击右键，选择“属性”，在弹出的界面中点击“设备管理器”

.. figure:: ./media/driver1.png 
   :width: 800
   :align: center

点击“网络适配器”，看到 “远程 NDIS 兼容设备” 表明驱动安装成功

.. figure:: ./media/driver2.png 
   :width: 800
   :align: center


软件安装
++++++++++++++++++++++++++++++++++++++++++++++++++++++

打开资料链接中的软件文件夹，下载 MaixVision-1.1.0-setup.exe，双击按照提示安装软件。 


案例测试
++++++++++++++++++++++++++++++++++++++++++++++++++++++

打开 MaixVision，通过 USB 连接设备到电脑，等待设备开机完成（显示“欢迎使用通慧”）

按下图所示连接设备

.. figure:: ./media/connect1.png 
   :width: 800
   :align: center

.. figure:: ./media/connect2.png 
   :width: 800
   :align: center


显示 “connect successful” 表明连接成功

.. figure:: ./media/connect3.png 
   :width: 800
   :align: center


测试程序 

::

   from maix import camera, display, image, nn

   cam = camera.Camera(640, 480)
   dis = display.Display()

   while True:
       img = cam.read()
       img.draw_string(10, 10, "Hello World!", image.COLOR_RED)
       dis.show(img)

创建空白文件，复制上面的测试程序到文本区，点击运行程序

.. figure:: ./media/run.png 
   :width: 800
   :align: center

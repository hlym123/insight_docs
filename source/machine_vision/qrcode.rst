二维码识别
====================================================== 


::

    from maix import image, camera, display

    cam = camera.Camera(320, 240)
    disp = display.Display()

    while 1:
        img = cam.read()
        qrcodes = img.find_qrcodes()
        for qr in qrcodes:
            corners = qr.corners()
            for i in range(4):
                img.draw_line(corners[i][0], corners[i][1], corners[(i + 1) % 4][0], corners[(i + 1) % 4][1], image.COLOR_RED)
            img.draw_string(qr.x(), qr.y() - 15, qr.payload(), image.COLOR_RED)
        disp.show(img)
 
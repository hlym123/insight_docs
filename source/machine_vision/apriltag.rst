AprilTag 识别
====================================================== 

::

    from maix import image, camera, display

    cam = camera.Camera()
    disp = display.Display()

    families = image.ApriltagFamilies.TAG36H11
    x_scale = cam.width() / 160
    y_scale = cam.height() / 120

    while 1:
        img = cam.read()

        new_img = img.resize(160, 120)
        apriltags = new_img.find_apriltags(families = families)
        for a in apriltags:
            corners = a.corners()

            for i in range(4):
                corners[i][0] = int(corners[i][0] * x_scale)
                corners[i][1] = int(corners[i][1] * y_scale)
            x = int(a.x() * x_scale)
            y = int(a.y() * y_scale)
            w = int(a.w() * x_scale)
            h = int(a.h() * y_scale)

            for i in range(4):
                img.draw_line(corners[i][0], corners[i][1], corners[(i + 1) % 4][0], corners[(i + 1) % 4][1], image.COLOR_RED)
            img.draw_string(x + w, y, "id: " + str(a.id()), image.COLOR_RED)
            img.draw_string(x + w, y + 15, "family: " + str(a.family()), image.COLOR_RED)

        disp.show(img)





 
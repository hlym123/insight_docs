image 模块
====================================================== 
 

class QRcode
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     返回二维码信息
    '''
    qrcode.payload()

    '''
     返回二维码边界框参数
    '''
    qrcode.rect() # tuple (x, y, w, h)
    qrcode.x()    # 矩形框起点坐标x
    qrcode.y()    # 矩形框起点坐标y
    qrcode.w()    # 矩形框的宽度
    qrcode.h()    # 矩形框的高度


class AprilTag
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     Returns a list of 4 (x,y) tuples of the 4 corners of the object.
    '''
    apriltag.corners()

    '''
     返回矩形框参数
    '''
    apriltag.rect() # tuple (x, y, w, h)
    apriltag.x()    # 矩形框起点坐标x
    apriltag.y()    # 矩形框起点坐标y
    apriltag.w()    # 矩形框的宽度
    apriltag.h()    # 矩形框的高度
    apriltag.cx()   # 矩形框中心点坐标x
    apriltag.cy()   # 矩形框中心点坐标y

    '''
     返回标签ID
    '''
    apriltag.id()

    '''
     Returns the numeric family of the apriltag.
    '''
    apriltag.family()

    '''
     Returns the quality of the apriltag image (0.0 - 1.0) where 1.0 is the best.
    '''
    apriltag.goodness()


class Blob
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    '''
     Returns a list of 4 (x,y) tuples of the 4 corners of the object.
    '''
    blob.corners()

    '''
     返回矩形框参数
    '''
    blob.rect()     # tuple (x, y, w, h)
    blob.x()        # 矩形框起点坐标x
    blob.y()        # 矩形框起点坐标y
    blob.w()        # 矩形框的宽度
    blob.h()        # 矩形框的高度
    blob.cx()       # 矩形框中心点坐标x
    blob.cy()       # 矩形框中心点坐标y

    '''
     返回色块内像素点
    '''
    blob.pixels()

class Circle
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    class image.circle

    '''
     返回圆相关信息
    '''
    x()  # 圆心位置x
    y()  # 圆心位置y
    r()  # 圆的半径

    '''
     Returns the circle’s magnitude.
    '''
    magnitude()


class Rect
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    class image.rect

    '''
     返回矩形四个角的位置 (x,y) tuples of the 4 corners of the object.
    '''
    rect.corners() # list[tuple(int, int)]

    '''
     返回矩形相关信息
    '''
    rect.rect() # tuple (x, y, w, h)
    rect.x()    # 矩形框左上角坐标x
    rect.y()    # 矩形框左上角坐标y
    rect.w()    # 矩形框的宽度
    rect.h()    # 矩形框的高度

    '''
     Returns the rectangle’s magnitude.
    '''
    rect.magnitude()


class Image
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    class image.Image
图像分类  
======================================================

图像分类（Image Classification）是计算机视觉中的一个核心任务，指的是将输入图像分配到预定义的类别或标签中。图像分类通常通过卷积神经网络（CNN）等深度学习模型来实现，它的应用范围广泛，包括自动驾驶、医疗图像分析、人脸识别、安防监控等。

图像分类的基本流程：

* 数据收集：首先需要构建包含图像和相应标签的数据集。例如，ImageNet 数据集提供了大量已标注的图像，通常用于训练和验证模型。
* 数据预处理
* 数据增强：通过图像旋转、翻转、裁剪、缩放等操作，生成多样化的数据，从而提升模型的泛化能力。
* 模型选择与设计：
    * 卷积神经网络（CNN） 是图像分类的主流模型，能够自动学习图像的空间特征。典型网络包括 AlexNet、VGG、ResNet、MobileNet 等。
* 模型训练：
    * 前向传播：输入图像通过神经网络进行计算，输出预测的类别概率分布。
    * 损失函数：分类任务通常使用交叉熵损失函数来衡量预测的类别与真实标签的差异。
    * 反向传播与优化：通过反向传播算法更新模型参数，常用优化器如 SGD、Adam 等。
* 模型评估：
    * 准确率：分类任务中，最常见的评估指标是准确率（Accuracy），即模型预测正确的样本占总样本的比例。
* 模型部署：经过训练的图像分类模型可以部署到各种应用场景中，如实时检测系统、移动应用等。

ImageNet  
++++++++++++++++++++++++++++++++++++++++++++++++++++++

`ImageNet <https://image-net.org/index.php>`_ 是一个庞大的视觉数据库，常用于计算机视觉任务中的图像分类和对象检测。
相关测试图片和完整的分类名请查看资料下载 `链接 <https://pan.baidu.com/s/1CG9cQ27SJ1ec5DFaOl1a4w?pwd=6666>`_ (提取码：6666) ImageNet 文件夹

MobileNet 
++++++++++++++++++++++++++++++++++++++++++++++++++++++

MobileNet 是一系列轻量级卷积神经网络架构，专为在移动设备或嵌入式设备上运行的高效图像分类和目标检测而设计。它以较少的计算资源和存储空间，保持了良好的性能。

Example: MobileNet 图像分类
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

    from maix import camera, display, image, nn, app

    # 加载设置字体
    image.load_font("sourcehansans", "/maixapp/share/font/SourceHanSansCN-Regular.otf", size = 20)
    image.set_default_font("sourcehansans")

    # 创建图像分类对象，加载 mobilenetv2 模型
    classifier = nn.Classifier(model="/root/models/mobilenetv2.mud", dual_buff = True)

    # 加载 ImageNet 中文分类标签
    classes = []
    with open("/root/models/imagenet_classes_ch.txt", encoding='utf-8') as f:
        read = f.readlines()
        for l in read: 
            classes.append(l.strip('\n'))
        f.close()  

    # 摄像头，显示屏初始化
    cam = camera.Camera(classifier.input_width(), classifier.input_height(), classifier.input_format())
    dis = display.Display()

    while not app.need_exit():
        img = cam.read() # 读取图像
        res = classifier.classify(img) # 输入图像到分类器
        max_idx, max_prob = res[0] # 获取检测结果，res[0] 只最大概率的结果 
        #msg = f"{max_prob:5.2f}: {classifier.labels[max_idx]}" # 英文标签
        msg = f"{max_prob:5.2f}: {classes[max_idx]}" 
        img.draw_string(10, 10, msg, image.COLOR_BLUE) # 显示检测结果
        dis.show(img) # 显示图像

测试图片 

.. container:: image-container

    .. figure:: ./media/火烈鸟.jpg 
       :width: 400
       :align: center

    .. figure:: ./media/寄居蟹.jpg 
       :width: 400
       :align: center

    .. figure:: ./media/金刚鹦鹉.jpg 
       :width: 400
       :align: center

    .. figure:: ./media/天牛.jpg 
       :width: 400
       :align: center

 




 
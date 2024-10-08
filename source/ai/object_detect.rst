目标检测   
======================================================

目标检测（Object Detection）是计算机视觉中的一个重要任务，它不仅仅是要识别图像中的物体，还要在图像中定位这些物体。与图像分类不同，图像分类只需要给出图像所属的类别，而目标检测则需要提供每个物体的类别及其在图像中的位置（通常以边界框的形式表示）。

YOLO
++++++++++++++++++++++++++++++++++++++++++++++++++++++

YOLO（You Only Look Once）是一种用于目标检测的深度学习模型，因其高效的实时检测能力而受到广泛关注和应用。YOLO 将目标检测问题转化为回归问题，使得检测速度显著提高。

COCO 
++++++++++++++++++++++++++++++++++++++++++++++++++++++

`COCO数据集 <https://docs.ultralytics.com/zh/datasets/detect/coco/>`_ 是一个广泛使用的计算机视觉数据集，旨在推动物体检测、分割和图像理解等领域的研究。


Example: YOLO 目标检测 
++++++++++++++++++++++++++++++++++++++++++++++++++++++

::

	from maix import camera, display, image, nn, app

	# 加载设置字体
	image.load_font("sourcehansans", "/maixapp/share/font/SourceHanSansCN-Regular.otf", size = 20)
	image.set_default_font("sourcehansans")

	# 创建目标检测器，加载 YOLOv5 模型
	detector = nn.YOLOv5(model="/root/models/yolov5s.mud", dual_buff=True)
	# detector = nn.YOLOv8(model="/root/models/yolov8n.mud", dual_buff=True)

	# 摄像头，显示屏初始化
	cam = camera.Camera(detector.input_width(), detector.input_height(), detector.input_format())
	dis = display.Display()

	# COCO80 分类标签
	coco80_classes = (
	    "人", "自行车", "汽车", "摩托车", "飞机", "公共汽车", "火车", "卡车",
	    "船", "交通信号灯", "消防栓", "停车标志", "停车计时器", "长椅", "鸟", "猫",
	    "狗", "马", "羊", "牛", "大象", "熊", "斑马", "长颈鹿",
	    "背包", "伞", "手提包", "领带", "行李箱", "飞盘", "滑雪板", "单板滑雪",
	    "运动球", "风筝", "棒球棒", "棒球手套", "滑板", "冲浪板", "网球拍", "瓶子",
	    "酒杯", "杯子", "叉子", "刀", "勺子", "碗", "香蕉", "苹果",
	    "三明治", "橙子", "西兰花", "胡萝卜", "热狗", "比萨", "甜甜圈", "蛋糕",
	    "椅子", "沙发", "盆栽植物", "床", "餐桌", "厕所", "电视", "笔记本电脑",
	    "鼠标", "遥控器", "键盘", "手机", "微波炉", "烤箱", "烤面包机", "水槽",
	    "冰箱", "书", "时钟", "花瓶", "剪刀", "毛绒玩具", "吹风机", "牙刷"
	)

	while not app.need_exit():
	    img = cam.read() # 获取图像
	    objs = detector.detect(img, conf_th = 0.5, iou_th = 0.45) # # 输入图像到检测器
	    for obj in objs: # 逐个结果显示 
	        img.draw_rect(obj.x, obj.y, obj.w, obj.h, color = image.COLOR_BLUE)
	        #msg = f'{detector.labels[obj.class_id]}: {obj.score:.2f}' # 英文标签
	        msg = f'{coco80_classes[obj.class_id]}: {obj.score:.2f}' # 中文标签
	        img.draw_string(obj.x, obj.y, msg, color = image.COLOR_BLUE)
	    dis.show(img) # 显示图像


 
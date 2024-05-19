# NWPU-VHR-10-for-yolov8
将西北大学的NWPU VHR-10数据集用于yolov8和yolov5的脚本

yolov8需要的标签为类别 中心坐标 宽高（归一化）0 0.622651356993737 0.6503712871287128 0.06993736951983298 0.11757425742574257

NWPU VHR-10的标签为左上角坐标 右下角坐标 类别 (563,478),(630,573),1 

文件如下


    |-datasets

        |-NWPU VHR-10 不建议有空格和分隔符
            |-ground truth 储存数据集集的标签
    
                   |--001.txt (563,478),(630,573),1
    
    
            |-positive image set 储存图片
    
                   |--001.jpg
    
            |-negative image set 存放可能没有检测物品的图片
    
            |-images 存放划分训练集、测试集、验证集
    
                   |--train
    
                   |--val
    
                   |--test
    
            |-labels 转换标签格式，存放划分训练集、测试集、验证集
    
                   |--train
    
                   |--val
    
                   |--test
            
            |-train.txt     存放训练集图片的路径
    
            |-test.txt      存放测试集图片的路径
    
            |-val.txt       存放验证集图片的路径
    
            |-nwpu.py       脚本    运行前需要修改路径  用于转换标签格式
    
            |-testsplit.py  脚本    运行前需要修改路径  用于划分训练集、测试集、验证集，将图片和标签存放在images和labels文件夹下
    
            |-ll.py         脚本    运行前需要修改路径  用于统计训练集、验证集、测试集的路径，生成train.txt、test.txt、val.txt

            |-nwpu.yaml    配置文件


之后可以在yolov5或yolov8下运行程序，这是一个10分类的数据集，将yolo.yaml的nc改为10。

yolov8

    # 加载模型
    model = YOLO('yolov8.yaml').load('yolov8n.pt')  # 从YAML构建并转移权重
    # 训练模型
    results = model.train(data='./datasets/NWPUVHR/nwpu.yaml', epochs=10,  workers=0)
    # 如果数据集中存在大量小对象，增大输入图像的尺寸imgsz可以使得这些小对象从高分辨率中受益，更好的被检测出。
 
    metrics = model.val()


yolov5

    python.exe train.py --data ./datasets/NWPUVHR/nwpu.yaml --epochs 30 --weights 'yolov5n.pt' --cfg yolov5n.yaml  --batch-size 16 --device 0 --workers 0
    你的解释器路径        数据集参数

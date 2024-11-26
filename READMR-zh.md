代码实施步骤

Original TF implementation: https://github.com/chenhsuanlin/3D-point-cloud-generation

训练/评估网络             

必要条件             

此代码是用Python3（Python3）开发的。需要Pythorch 0.4+。             

数据集             

（在TF的repo中提供）可以通过运行命令下载数据集（8.8GB）

wget https://cmu.box.com/shared/static/s4lkm5ej7sh4px72vesr17b1gxam4hgy.gz

此文件包括：              

训练/测试分割文件（从透视变换网络）             

输入RGB图像（从透视变换网络）             

用于训练的预渲染深度图像             

测试分离的地面真值点云（密度为100K点）

下载后，在主目录下运行

run tar -zxf s4lkm5ej7sh4px72vesr17b1gxam4hgy.gz

文件将被提取到data目录。（使用此数据集包，可引用相关论文。）

运行代码             

以下脚本提供了运行代码的示例。             

网络预训练：scripts/train-stg1.sh             

进行二维优化微调：scripts/train-stg2.sh             

在测试集上求值：scripts/evaluate.sh             

计算错误度量：scripts/evaluate_dist.sh             

检查点存储在models/${experiments}中，摘要存储在runs/${experiments}中，计算的点云存储在results{GROUP}中。执行python3 train-stg1.py--help可以找到可选参数列表。

绘制真实深度图像             

（在TF的repo中提供）提供了用于呈现深度图像的代码以供监督。             

先决条件             

此代码要求以下内容：             

Blender作为渲染引擎。此代码是使用Blender 2.78开发的。安装后，请确保该命令blender是可调用的（用于which blender检查安装）。
用于将.exr转换为.mat文件的OpenEXR Python绑定。 
数据集             

原始ShapeNet数据集可以在这里下载。此呈现代码是为使用ShapeNetCore v2开发的。（提供的深度图像是从ShapeNetCore v1渲染的。）             

运行代码             

在渲染中，运行/运行.sh03001627 8为固定和任意视点渲染深度图像，并将其转换为.mat文件。这将转换ShapeNet椅子类别（03001627）中具有8个固定视点的所有对象。呈现的文件将存储在输出目录中。

评估CAD模型密集点云的生成             

（在TF的repo中提供）还提供了代码来将CAD模型的顶点加密到指定的数字。此代码可以独立运行；只需要ShapeNet数据集。重复将顶点添加到三角形网格最长边的中心，然后重新对网格进行三角剖分的过程。这将创建（通常）均匀致密的CAD模型。

运行代码

在致密下，运行

run  ./run.sh 03001627

进行加密，加密的CAD模型将存储在output目录中。

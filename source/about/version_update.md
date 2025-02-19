# 版本更新记录

## 1. 正式版

发布时间：2022年9月

### 开发计划

1.实现以pip方式安装。

2.分MMEdu、BaseML、BaseNN三个功能模块。

3.工具持续迭代，增加了模型部署库BaseDeploy和数据处理库BaseDT。

### 正式版更新记录

#### 1）MMEdu

##### V0.1.20 20230704

1. cls的sota()函数完善，无需声明。

##### V0.1.15 20230605

1. 对模型生成示例代码和载入onnx权重信息做了拓展和调整。

##### V0.1.14 20230517

1. 优化批量推理时show_result的判断逻辑，避免大量占用内存导致的内核中断。

##### V0.1.9 20230423

1. 合并git与飞书中的最新版本。
1. 更新cls和det转换生成内容以适配最新XEdu库。
1. 消除生成onnx权重大段warning。
1. 类别压入生成的权重。
1. train()函数返回log。
1. 权重文件中保存版本号。

##### V0.1.8 20230316

1. pth存储信息完善。
1. pth_info函数展示权重文件相关信息。

##### V0.1.7 20230313

1. 更新cls和det模型转换后生成的py文件内容。

##### V0.1.6 20230302

1. cls和det的推理和转化函数中去除了class_path这一参数，类别信息从pth中获得。
1. 修复SSD_Lite类名传递不正确的问题。

##### V0.1.5 20230203

1. det修正infer和convert中类别数量的问题。
1. det模型训练时会自动保存best_map的权重。
1. det 规范化数据集文件夹名称。
1. 修复SSD_Lite类名传递不正确的问题。

##### V0.1.4 20230106

1. cls+det同时增加可选batch_size功能。
1. det补充SSD和yolov3。
1. det输出格式由xywh修正为x1y1x2y2。

##### V0.1.3 20221222

1. det增加模型转化功能。
2. cls+det更新模型转化功能，参数调整，会额外输出config文件。

##### V0.1.2 20221215

cls：

1. cls检查数据集中图片shape，指出损坏图片。检查图片出现损坏时，抛出错误码`The image file xxx is damaged`。

2. 数据集如缺少txt，自动生成。

   case1：数据集缺少classes.txt, val.txt ，会自动生成并提示, eg，“生成val.txt”。

   case2：如缺少test_set，可正常训练，但不会生成test.txt 。（不影响正常功能）

   case3：如缺少val_set，可训练，但不能验证，即train函数中validate参数不能为True。（功能受损，看不到准确率，但还是可以训练出模型）。

   其他：

   允许数据集中出现其他类别的文件，eg,csv；

   数据集中test_set可以不按照类别存放。

3. 检查写权限，确定写到哪里

   innolab上数据集没有读写权限，则将txt生成至项目内，文件夹名为dataset_txt，内含classes.txt，val.txt。(若有读写权限则生成至数据集路径内）


​	4.加入模型转换convert()函数，pth转onnx。

det：

1. det增加支持PIL和np array 输入功能。图片形式可以通过PIL和np数组进行输入，PIL和数组列表也支持输入。
2. 参考cls，det增加相关错误码。

##### V0.1.1 20221118

​	支持读入pil，np格式数据。

##### V0.1.0 20221111

1. train和infer的`device=cuda`检查`torch.cuda.is_available()`，`device=cpu`当cuda可用时提示可以使用cuda加速。
2. 文件夹推理LeNet无误。
3. `fast_infer`支持LeNet。

##### V0.1.0rc2 20221111

​	同V0.0.9，少依赖版本。

##### V0.0.9 20221104

1. 检测模块训练函数支持device参数。
2. `load_checkpoint()`参数顺序更换。将checkpoint前置（第一个），`device`后置，可以只输入路径，而省略 "`checkpoint=`"。
3. fast_infer错误反馈，补充错误情况，当`fast_infer`之前未使用l`oad_checkpoint`载入`ckpt`时会提示错误码305。
4. `MMEdu.__ path __` 可正常返回环境中包所在地址。
5. 修复lenet 文件夹推理问题。

##### V0.0.1rc2 20221104

​	同V0.0.9，少依赖版本。

##### V0.0.8 20221102

1. 加入错误反馈机制。

2. 增加命令行字符画和简介。

3. 提示目前支持的主干网络。

4. 支持推理opencv、PIL读入的图片。

5. 模型声明时允许读入配置文件，而不仅是模型名。

##### V0.0.1rc1 20221102

​	同V0.0.8，少依赖版本。

#### 2）BaseML

##### V0.0.6 20230217

1. 与MMEdu的错误提示码风格进行了统一，并在此基础上进行了BaseML部分的补充。
2. 所有库类代码应用了PEP8代码规范，使得代码结构与语句更加美观。

##### V0.0.5 20230210

1. 完成模型可视化和评测指标可视化两个库。目前只有4种算法支持可视化，大部分模型支持评测指标可视化，少部分不支持。
2. 引入yellowbrick库，用于评测指标可视化。
3. 修改了load_dataset函数，cls和reg默认split=True, 即划分为训练和测试集， 聚类和降维默认不划分。
4. 加入了警告（蓝色字体）和报错（红色字体），但待与MMEdu的风格统一。

##### V0.0.4 20221121

​	按照cls中的分类算法，给reg中的算法名进行了更改与添加，目前的回归算法有：['LinearRegression', 'CART', 'RandomForest',       'Polynomial', 'Lasso', 'Ridge', 'SVM', 'AdaBoost', 'MLP']。

##### V0.0.3 20221115

​	把 `from BaseML import Classification`  调用为`Classification.cls`  改成了 `from BaseML import Classification as cls`  调用为 `cls(algorithm= ...)`。

##### V0.0.2 20221110

1.  给每个类增加了docstring类型的注释，可以使用`cls.__doc__`查看拥有的算法以及类注释。
2.  更改了`load_dataset`函数的初始默认值，默认shuffle, 不展示前5条数据，不划分数据集，不进行数据归一化。
3.  添加了反归一化函数，可以将归一化后的数据转换为原数据，在`base.reverse_scale`函数中。

##### V0.0.1 20221110

1. `load_dataset`中设置了X和y的默认列，如果没有标明`x_column`和`y_column`，默认采用输入的所有列。但输入的是**txt**或**csv**格式的话，一定要标注出列号，否则报错。
2. `inference()`中加了参数`verbose`，默认值为True，表示会输出训练过程中的过程数据，False则不会。

3. `train()`中设置了参数`validate`（默认为True），表示会将输入的训练集划分为训练集和验证集，并输出验证集下的模型准确率。

4. 添加了图片读取处理模块ImageLoader，具体使用方式查看文件中的注释以及demo实现。

5. 对于加载数据集，添加了几个bool标记：shuffle, show, split, scale，分别表示是否打乱数据集、是否展示5条数据、是否划分数据集、是否对训练数据进行归一化。

6. 每个模型的初始化增加了参数字典方法，便于更高级的模型调参。


#### 3）BaseNN

##### V0.1.6 20230531

1. 训练速度优化，dataloader多线程读取设置。

##### V0.1.5 20230529

1. basenn层名兼容大小写，推荐全部采用小写。
2. 图片文件夹、特征csv格式数据集设计并实现。

##### V0.0.7 20230322

1. 继续训练，特征可视化适配新的pth文件格式。

##### V0.0.6 20230317

1. 保存模型文件由pkl统一为pth，加入pth_info()。
2. 加入RNN部分。

##### V0.0.5 20221215

1. 可视化特征，只有传统意义上的层才计数，relu，reshape，softmax不计数;且当输入为二维图像时，展示可视化的图像，输入为一维数据时，生成txt保存每层之后的输出。
2. 加入随机数种子，确保当指定种子后，反复训练可以得到完全一致的结果。
3. 可选损失函数，可选评价指标。

##### V0.0.4 20221202

​	参数控制可视化，一整张图or一系列图。

##### V0.0.3 20221116

​	增加提取特征，可视化特征功能。

#### 4）BaseDT

##### V0.1.1 20230626

1. 修复BaseDT中plot模块在自定义载入时绘图通道顺序显示的错误。
2. 修改plot对分类问题显示时重复出现pred_label。

##### V0.1.0 20230621

1. 修复plot在绘图时信息未载入而引发报错的问题。

##### V0.0.9 20230620

1. 修复了plot使用show时函数冲突问题。
2. 增加了MMPose绘图所需的模块。
3. 修复了get_img时调用了show函数导致会使用plt进行绘制的问题。
4. util模块增加MMPose SIMCC格式推理前后处理的内容（之后得考虑将其迁移至data模块中）。

##### V0.0.8 20230616

1. 画图功能完善。

##### V0.0.7 20230609

1. 划分csv数据集加入归一化功能。

##### V0.0.6 20230607

1. 加入划分csv数据集功能。
2. 取消jieba安装依赖，仅在函数内部引用。
3. basedeploy相关的功能更新。

##### V0.0.4 20230426

1. log_plot接入train时日志导出。
2. 类名导出函数重命名为get_label。
3. 修复imshow_det_bboxes、map_orig_coords函数的一些漏洞。

##### V0.0.1 20230209

​	首次上源。

#### 5）XEdu一键安装包

##### V1.4.6 20230529

​	解决BaseNN推理缓慢的问题。

##### V1.4.5 20230529

​	升级BaseNN语法；

​	修复pip安装失败的问题；

​	优化easy系列功能。

##### V1.4 20230516

​	支持模块：MMEdu0.1.13（支持cls和det），BaseNN0.0.9，BaseML0.0.6（支持cls、reg和clt）、BaseDT0.0.5（支持通用数据处理）

​	内置编辑器：jupyter、pyzo、三个可视化工具（EasyTrain EasyInference EasyAPI）

​	升级支持模型转换onnx、推理和部署语法精简，不再需要class_path。BaseML支持绘图。

##### V1.3 20230416

​	支持模块：MMEdu0.1.8（支持cls和det），BaseNN0.0.9，BaseML0.0.6（支持cls、reg和clt）、**BaseDT0.0.2（支持通用数据处理）**

​	内置编辑器：jupyter、pyzo、三个可视化工具（EasyTrain EasyInference EasyAPI）

##### V1.2 20230110

​	支持模块：MMEdu0.1.4（支持 cls 和 det），BaseNN0.0.5，BaseML0.0.3（支持 cls、reg 和 clt） 

​	内置编辑器：jupyter、pyzo、三个可视化工具（EasyTrain EasyInference EasyAPI） 

##### V1.1 20221220

​	支持模块：MMEdu0.1.2（支持cls和det），BaseNN0.0.5，BaseML0.0.3（支持cls、reg和clt）

​	内置编辑器：jupyter、pyzo、三个可视化工具（EasyTrain、EasyInference和EasyAPI）

#### 6）BaseDeploy

##### V0.0.3 20230626

1. 新增demo实例文件夹，内置lenet的onnx模型。
2. 预测结果保留未润色后的形式，并可使用print_result对结果进行润色。

### XEdu 0.1.0版

发布时间：2022.11

版本说明：优化MMEdu、BaseML、BaseNN等模块，增加EasyAPI.bat、EasyInference.bat、EasyTrain.bat三个可视化工具，更新所有示例代码。

### MMEdu pip-0.0.1版

发布时间：2022.8

版本说明：发布内测版pip包。

### XEdu 0.0.1版

发布时间：2022.6

版本说明：重构目录结构，建立MMEdu和BaseML两大模块。

### 0.7版

发布时间：2022.6

版本说明：优化0.5版两个模块，新增自定义网络（BaseNN）模块。

### 0.5版

发布时间：2022.4

版本说明：整合图像分类（cls）、物体检测（det）两个核心模块，内置Pyzo、Jupyter，实现一键部署。


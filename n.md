### 一. 高性能计算技术

* *~~*并行计算：**~~

  ~~并行计算或称平行计算是相对于串行计算来说的。并行计算是指同时使用多种计算资源解决计算问题的过程【可以分为时间上的并行和空间上的并行】~~

* ~~**分布式计算**~~

  ~~分布式计算研究如何把一个需要非常巨大的计算能力才能解决的问题**分成许多小的部**分**，然后把这些部分**分配给许多计算机进行处理**，最后把这些**计算结果综合起来得到最终的结果~~

* ~~**如何区分并行计算和分布式计算？**~~

  ~~并行计算与分布式计算都是运用并行来获得更高性能，化大任务为小任务。简单说来，如果处理单元**共享内存**，就称为并行计算，反之就是分布式计算。~~

  ~~![image-20210624142902788](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624142902788.png)~~

* ~~分布式计算的优势~~

  * ~~稀有资源可以共享~~
  * ~~通过分布式计算可以在多台计算机上平衡计算负载~~
  * ~~可以把程序放在最合适运行它的计算机上~~

* **常见的并行计算框架**

  * MPI【message passing information】消息传递接口

    * 跨语言的并行计算接口，
    * 目标是高性能，大规模性，可移植性
    * 传统的高性能计算

  * **MapReduce**

    * google提出的软件架构，用于大规模数据集的并行计算

      * MapReduce概念：
        * 一个基于集群的高性能并行计算平台
        * 一个并行计算与运行软件框架
        * 一个并行计算程序设计模型与方法【也可以是一些方法，model，借助函数式【list语言？】来实现并行计算】【主要是map函数与reduce函数】
      * 提供的功能
        * 数据划分和计算任务调度
          * 前提本来就是分布式环境【数据/计算分布】
        * 数据/代码互定位
          * 不需要设计底层，只需要应用
        * 系统优化
        * 出错检测和恢复
      * MapReduce的特点
        * 向外横向扩展，而非向上纵向拓展
          * 集群的构建，选用的是便宜的，低端的设备，和mpi有本质的区别，对于大量数据的集群在这种情况下比较优越
        * 失效被认为是常态
          * 由于设备比较低端，短期内失效比较常态，节点和硬件和软件的失效比较常见，任何结点的失效不会导致整个系统的失效，会有容错，备份，无缝接管失效结点的工作
          * 使用多种错误检查和错误恢复机制来实现
        * 把处理向数据迁移
          * 数据在哪里，计算任务就分布在那里；传统的情况会有固定的计算结点
        * 顺序处理数据，避免随机访问数据
          * 顺序访问要比随机访问快，一般在外磁盘中
        * 为应用开发者隐藏系统层细节
          * 将编程工作交给底层框架，开发调试，差错工作，数据管理分发，通信同步等
        * 平滑无缝的可扩展性
      * map产生键值对，然后把键值对放到对应的reduce，reduce：将相同的key进行归类

      ![image-20210624153359444](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624153359444.png)

      * MapReduce步骤

        * Map：产生**<key,value>对**【键值对】
        * 在Map，Reduce之间系统把同一Key归类Reduce
        * Reduce操作对相同的Key进行归类处理

      * 例子：单词计数问题【可能参与编程】

        ![image-20210624153850258](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624153850258.png)

  * **Spark**

    * 专门为大规模数据处理而设计的快递通用的计算引擎，是一种包含流处理能力的下一代批处理框架

    * hive：数据仓库，storm数据流

    * 特点：

      * 高性能
        * 运行工作负载的速度提高了100倍
      * 易用
        * 使用java，scala，python，SQL等快速编写应用程序
      * 通用性
        * 结合使用SQL，流和复杂的分析
      * 高可扩展性【在hadoop等进行容器化的运行】
        * Spark可在Hadoop，Apache Mesos，Kubernetes，Standalone或云服务器中运行。它可以访问各种数据源。

    * RDD：弹性分布式数据集，是Spark中最基本的数据抽象。将数据项拆分为多个分区的集合,存储在集群的工作节点上的内存和磁盘中，并执行正确的操作

      * RDD特点
        * 不可变的【只能通过转换操作生成新的RDD】
        * 分区的【可以分布在多台机器上进行并行处理】
        * 弹性的【计算过程中内存不够时它会和磁盘进行数据交换】
        * 基于内存【可以全部或部分缓存与内存中，在多次计算间重用】
        
      * RDD算子类型

        * transformation算子
          * 延迟计算的特性（Lazy）, 记录读取和计算的方法，如flatMap, map，reduceByKey
        * action算子
          * 触发Transformation算子执行
        * 持久化算子
          * 将RDD从内存持久化到磁盘
  
        ![image-20210628112759488](C:\Users\all\AppData\Roaming\Typora\typora-user-images\image-20210628112759488.png)
  
    * 例子【单词计数】
  
      ![image-20210624155232077](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624155232077.png)

    * Spark和MapReduce的区别

      * MR的不足
  
        *  仅支持Map和Reduce两种操作
        * Map中间结果需要写磁盘
        * 任务调度和启动开销大
        * 无法充分利用内存
        * Map和Reduce都需要排序
        * 不适合迭代计算

      * Spark优势

        *  丰富的API（Java、Scala、Python、 R四种语言，sort、join等高效算子）
        * DAG执行引擎，中间结果保存在内存
        * 线程池模型减少task启动开销
        * 充分利用内存，减少磁盘IO
        * 避免不必要的排序操作
        * 适合迭代计算，比如机器学习算法
  
        
  
  * Geotrellis
  
    * 用于高性能应用程序的地理数据处理引擎
  
    * 特性
  
      * 使用Scala语言处理栅格的数据类型，对数据的操作灵活性高
      * 使用Spark作为计算框架，基于RDD的数据处理方式，使得IO和计算能力显著提高
      * 封装了操作栅格数据的功能，包括裁剪/变形，地图代数操作和渲染操作
  
    * 核心概念
  
      * Layer：由多个Tile构成的2D栅格数据图层，每个Tile拥有一个行列号
      * Tile：数据分块，为一系列像素的集合。
      * Cell或Pixel：表示Tile中的一个像素。
      * Metadata：栅格的存储元数据（空间范围、投影类型、像素类型等）。
      * KeyIndex: Tile之间的组织方式，即空间曲线。

      <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624160342716.png" alt="image-20210624160342716" style="zoom: 33%;" />

      ​	

    * 核心组件【数据管理组件】
  
      * AttributeStore: 管理图层的元数据信息
      * LayerReader：读取影像值
      * LayerWriter：将普通影像导入Geotrellis的数据源中
      * backend: 以接入第三方应用的方式来存储影像
  
      <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624160754794.png" alt="image-20210624160754794" style="zoom:50%;" />
  
    * 数据如何存储到Backend？----ETL工具
  
      * ETL(Extract-Transform-Load)是用来描述将数据从来源端经过**抽取（extract）、转换（transform）、加载（load）**至目的端的过程
      * ETL工具的质量问题具体体现在正确性，完整性，一致性，完备性，有效性，可获取性
  
      <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624161613695.png" alt="image-20210624161613695" style="zoom:33%;" />
  
    * ~~在工具包中封装了许多数据的功能 【如渲染，裁剪，】~~
    
    * ~~把实体的数据转化成geotrellis-layer【可以分层级的记录数据，把geotiff在数据共享的层面来】~~
    
    * ETL导入数据过程
    
      * ETL能将**大体量影像**数据切片成多层级瓦片，从而支持分布式计算和层级可视化。
    
        <img src="C:\Users\all\AppData\Roaming\Typora\typora-user-images\image-20210628113555945.png" alt="image-20210628113555945" style="zoom:50%;" />
    
      * Geotrellis Layer
    
      <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628113717710.png" alt="image-20210628113717710" style="zoom:50%;" />
    
    * 例子【伏羲平台基于Geotrellis实现叶绿素反演】
    
      ![image-20210628113121175](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628113121175.png)
    
      * 其中使用的是SeaWiFS传感器；SeaStar卫星（太阳同步轨道卫星）；美国国家航空航天局用于采集全球海洋生物光学特性的数据
      * Rrs490是SeaWiFS的蓝光波段；Rrs555是绿光波段

### 二. 遥感深度学习的方法

* 梯度下降【一种算法】：主要目的是**通过迭代**找到目标函数的最小值，或者收敛到最小值。而在深度学习中，训练神经网络的目的就是找到最低损失（Loss）的网络参数 θ

* 梯度下降的步骤：

  * 随机初始化参数 
  * 计算梯度<img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624162822002.png" alt="image-20210624162822002" style="zoom: 67%;" />
  * 沿梯度相反方向下降，更新参数【学习率】<img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624162904761.png" alt="image-20210624162904761" style="zoom:67%;" />
  * 重复以上步骤直到收敛

* 反向传播：利用链式法则计算得到神经网络的梯度的过程

  <img src="C:\Users\all\AppData\Roaming\Typora\typora-user-images\image-20210624163013586.png" alt="image-20210624163013586" style="zoom:67%;" />

* 梯度消失：求出的梯度更新信息将会以指数形式衰减

* 神经网络训练过程

  * 随机初始化参数，输入样本数据
  * 逐层前向传播计算输出值
  * 计算代价函数【输出值和真实值的损失】
  * 根据反向传播原理计算代价函数对每个神经元参数的偏导
  * 更新网络参数


<img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628113823445.png" alt="image-20210628113823445" style="zoom:50%;" />

* 神经网络需要注意避免过拟合【拟合越好，泛化越好】

  * 欠拟合：对训练数据的拟合情况不好
  * 过拟合：对训练数据的拟合较好，但对真实数据不好
  * 应对策略：
    * Dropout在训练过程中随机设置一部分神经元不激活
    * 提早停止训练

  

* 卷积神经网络的层次结构

  * 数据输入层【对原始图像进行预处理】input layer

    * 去均值

      * 把输入数据各个维度都中心化为0，其目的就是把样本的中心拉回到坐标系原点上

    * 归一化

      * 幅度归一化到同样的范围

        <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624164803013.png" alt="image-20210624164803013" style="zoom:33%;" />

    * PCA/白化：

      * 用PCA降维；白化是对数据各个特征轴上的幅度归一化

        <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210624164714630.png" alt="image-20210624164714630" style="zoom:33%;" />

  * 卷积计算层【最重要的一层】convolution layer

    * 卷积：一组固定的权重和不同窗口内数据做内积
    * 两个关键操作
      * 局部关联【每个神经元看成一个滤波器，进行滤波】
      * 窗口滑动【对局部数据进行计算】

    * 基本属性
      * 深度【表示有多少个神经元】
      * 步长【窗口滑动的长度】
      * 填充值

  * 激励层【梯度求解简单，收敛快，但脆弱】ReLU layer

    * 把卷积层输出结果做非线性映射。CNN采用的激励函数一般为ReLU(The Rectified Linear Unit/修正线性单元)，它的特点是收敛快，求梯度简单，但较脆弱，图像如下。

      <img src="C:\Users\all\AppData\Roaming\Typora\typora-user-images\image-20210628113959364.png" alt="image-20210628113959364" style="zoom: 33%;" />

  * 池化层  Pooling layer

    * **池化层夹在连续的卷积层中间， 用于压缩数据和参数的量，减小过拟合。**简而言之，如果输入是图像的话，那么池化层的最主要作用就是压缩图像。
    * 具体作用
      * 特征不变性【特征的尺度不变性，数据的压缩，把重要的尺度不变的信息进行保留；有损压缩下，保证重要信息不丢失】
      * 特征降维【把冗余信息去掉，把最重要的提取出来】
      * 防止过拟合
    * 常见方法：max pooling【取滑动窗口的最大值，并将其赋给中心像元】 与average pooling

  * 全连接层  FC layer

    * 两层之间所有神经元进行权重连接，通常在网络尾部【这和传统的神经网络神经元的连接方式是一样的】

* CNN求解步骤【卷积网络一般执行的是监督训练】

  * 参数初始化
    * 在开始之前，所有权都用不同的小随机数进行初始化。
      * 小：保证网络不会因为权值太大而进入饱和状态，导致训练失败
      * 不同：保证网络可以正常学习【如果一样，则无学习能力】

  训练

  * ~~第一阶段：前向传播阶段~~
    * ~~从样本集中选一个样本，输入网络。计算相应的实际输出【在这个阶段，信息从输入层经过逐级的变换，传送到输出层，这个过程网络在完成训练后正常执行时的执行过程】~~
  * ~~第二阶段：后向传播过程~~
    * ~~计算实际输出与相应的理想输出的差~~
    * ~~按照极小化误差的方式调整权值矩阵~~

* CNN具体步骤

  * 1. 选定训练组，从样本集中分别随机地寻求N个样本作为训练组；
  * 2. 将各权值、阈值，置成小的接近于0的随机值，并初始化精度控制参数和学习率；
  * 3. 从训练组中取一个输入模式加到网络，并给出它的目标输出向量；
  * 4. 计算出中间层输出向量，计算出网络的实际输出向量；
  * 5. 将输出向量中的元素与目标向量中的元素进行比较，计算出输出误差；
  * 6. 对于中间层的隐单元也需要计算出误差；
  * 7. 依次计算出各权值的调整量和阈值的调整量；
  * 8. 调整权值和调整阈值；
  * 9. 当经历M次后，判断指标是否满足精度要求，如果不满足，则返回(3)，继续迭代；
    10. 如果满足就进入下一步；
    11. 训练结束，将权值和阈值保存在文件中。这时可以认为各个权值已经达到稳定，分类器已经形成。再一次进行训练，直接从文件导出权值和阈值进行训练，不需要进行初始化。
  
  
  
  
  
* 遥感影像分类现状

  * 随着遥感技术和计算机技术的不断发展，遥感影像逐渐呈现出**<u>高光谱、高空间、高时间分辨率</u>**的特点，传统的遥感影像分类方法已不能满足如今遥感影像分类的需求

  * 统计模式识别方法：最大似然法、最小距离法、K-均值聚类法等。针对高分辨遥感影像中大量的细节信息和地物光谱的复杂化问题分类准确率下降。

  * 新的方法如支持向量机、遗传算法、面向对象等被用于遥感影像的解译中，

    虽然取得了很好的分类效果，但是自动化程度不高。

* 深度学习的遥感分类的一般流程

  * 数据输入
  * 深度神经网络特征提取【包括光谱特征，空间特征，光谱-空间特征】
  * 分类器分类【如SVM，logistic回归，softmax分类】

* 深度学习的遥感分类的优点和分类

  * 优点
    * 更好地提取遥感影像地**深层次**特征
    * 实现对高光谱遥感影像地**降维**
    * 在影像分类中分类**精度更高**
    * 遥感解译更**自动化和智能化**
  * 分类
    * 监督分类：卷积神经网络CNN
    * 非监督分类：深度信念网络DBN，自动编码器网络AE

  ![image-20210625151208377](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210625151208377.png)

* 常用的高光谱遥感数据集

  * INDIAN PINES数据集【145*145，200个光谱波段】
  * PAVIA大学数据集【610*340，104个光谱波段】

  

### 三. 共享服务技术

* 对象存储【是共享服务的基础】：
  也称为基于对象的存储，是一种扁平结构。其中地文件被拆分成多个部分并散布在多个硬件间。【在对象存储中，数据被分解为“对象”地离散单元，并保存在单个存储库中】

* object【由data，OID，metadata，attributes组成，是对象存储定义的最小数据存储单元】组成部分
  * data【用户要存储的数据】
  * meta data【元数据】
  * OID：数据对象的唯一标识
  * Attributes：数据属性

* 对象存储，块存储，文件存储的对比

  * 块存储读写快，但不利于共享
  * 文件存储利于共享，但读写慢
  * 对象存储兼具高速直接访问磁盘【读写快】，以及分布式【利于共享】

  ![image-20210625153307136](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210625153307136.png)

* 对象存储协议：Amazon S3协议

  * 由亚马逊提供的一套新兴的对象存储协议。本质上是通过基于 HTTP协议的 REST API访问【如通过 HTTP 发送命令到对象存储：PUT 用来建立一个对象，GET 用来读取一个对象，DELETE 用来删除对象等等】

  ![image-20210625153537465](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210625153537465.png)

* 对象存储的应用场景
  * 百度云存储BOS：是一个完整的从数据传输，数据存储，到数据处理，再到数据分发的生态
  
    <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628114551834.png" alt="image-20210628114551834" style="zoom:50%;" />
  
  * 企业云盘：
    * 华为云提出**基于对象存储服务 OBS 的企业云盘**（网盘）的解决方案，利用 OBS 存储静态数据【业务系统通过内网对静态数据进行处理，用户终端直接向OBS请求和取回静态数据】，借助 OBS 提供的生命周期功能，实现不同存储类别之间的自动转换，从而节省存储成本。 
    
    <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628114626962.png" alt="image-20210628114626962" style="zoom: 50%;" />
    
  * 视频直播
    * **阿里云**为了管理RTMP推流提出 **LiveChannel**（直播频道）的概念，用户可以通过创建LiveChannel 获得RTMP推流地址，随后通过RTMP协议**将音视频数据上传到阿里云的对象存**储服务 (OSS)，实现音视频的云存储。
    
    <img src="C:\Users\all\AppData\Roaming\Typora\typora-user-images\image-20210628114703360.png" alt="image-20210628114703360" style="zoom:50%;" />
  
* #### Ceph：

  **Ceph是一种为优秀的性能、可靠性和可扩展性而设计的统一的、分布式文件系统**。ceph的统一体现在可以**提供文件系统、块存储和对象存储**，分布式体现在可以动态扩展。

  

  * Ceph架构与核心组件

    * MON（monitor）监视器【集群中最重要的组件】

      * 在Ceph中相当于管理者，维护整个集群的状态。

      * Mon保证集群的相关组件在同一时刻能够达成一致，相

        当于集群的领导层，负责收集、更新和发布集群信息。

      * **为了规避单点故障，在实际的Ceph部署环境中会部署多**

        **个Mon**，同样会引来多个Mon之前如何协同工作的问题

      * 标准的Ceph环境下，功能分为管好自己，管好集群信息

        

    * OSD实际存储管理的进程

      * 通常一个OSD daemon绑定一个物理磁盘。Client write/read 数据最终都会走到OSD去执行write/read操作。

    * RGW【对象网关】

      * **提供了一个兼容S3和Swift的** **restful API接口。**RGW还支持多租户和Openstack的keyston身份验证服务。

  

* #### 微服务：

  使用一套小服务来开发单个应用的方式途径，每个服务运行在自己的进程中，并使用轻量级机制通信（如HTTP API），通过自动化部署机制来独立部署，服务之间的编程语言、数据存储等特点无需统一，保持着最低限度的集中式管理

  * 传统单体的局限

    * **代码臃肿**：应用启动时间长；
    * **测试耗时**：修复单一bug需要对所有业务进行回归测试；
    * **应用容错性差**：小功能错误可能导致整个系统宕机；
    * **伸缩局限**：扩大系统性能需要重新部署；
    * **开发协作困难**：上百开发人员需要同时去维护一套代码。

  * Docker【和微服务绑定】【针对传统单体应用的局限而提出的微服务】

    * 是一种开源容器(**Container**)技术，让开发者可以打包应用及其依赖到一个可移植容器**中，然后发布到**Linux机器**上或实现**虚拟化，完全使用沙箱机制，相互之间不会有任何接口。
    * 相比于虚拟机的有点
      * 启动更加快速；
      * 部署更加方便；
      * 体量更小；
      * 性能接近原生；
      * 功能隔离

  * K8s

    * **Kubernetes**，缩写为K8s，是Google内部容器编排管理平台Borg为原型的开源实现，也就是一个**开源的自动化大规模容器集群管理平台**，包括部署，调度和节点集群间扩展。Docker是Kubernetes内部使用的低级别组件。Kubernetes不仅仅支持Docker，还支持Rocket（另一种容器技术）。

    <img src="https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628115203997.png" alt="image-20210628115203997" style="zoom:50%;" />

    * 不仅仅是一个**容器编排系统**，而是**提供一个规范**，使开发者能描述和管理微服务集群的架构，定义其最终状态，帮助开发者将微服务系统自动达到和维持在这个最终状态。其核心特性如下

      * **自动化部署：** 部署后会根据应用程序计算资源需求，自动分配到每个node。 

      * **系统自愈：**如果某个节点宕机，会重新将其上的所有Pod调度到可用节点

      * **水平扩展：**周期调整每个工作负载的副本数量。

      * **服务发现和负载均衡：**内置服务发现功能，为每个容器分配内部ip，并用service代理。

      * **自动更新和回滚：**将当前工作负载的pod按照一定规则逐一升级或者回滚，而不会全部杀掉。

      * **弹性伸缩**：监控工作负载的CPU或者内存使用情况，对其增加或者减少运行的Pod数量

        

  

  * Kubernetes【K8s】：管理容器【操作管理调度容器的】，【docker比较初级】

    * 本来是一个用来管理无状态应用的容器平台，但是近两年有越来越多的公司用它来运行各种各样的工作负载，尤其是**TensorFlow**，**Caffe**，**MXNet**等等**分布式**机器学习的任务

    * K8s相对分布式AI的弊病
      * 配置难【不同分布式AI任务有不同配置要求；】
      * 调度难【默认的调度器对于机器学习任务的调度并不友好 】
      * 功能局限【能统筹到的模型训练只是AI中很小一部分，如Orale Graphpipe，Databricks MIflow，Google Kubeflow】

  * kubeflow

    * 特点
      * 是Google为了支持自家的**Tensorflow**的部署而开发出的开源平台，
      * 同时也支持Pytorch和SKlearn等**其它机器学习引擎**，
      * 是一个**为 Kubernetes 构建**的可组合，便携式，可扩展的机器学习技术栈。

    <img src="C:\Users\all\AppData\Roaming\Typora\typora-user-images\image-20210628123449458.png" alt="image-20210628123449458" style="zoom:33%;" />

    * pipeline
      * 是**Kubeflow**社区的开源项目，提供了一种<u>面向机器学习的工作流解决方案</u>，将机器学习中的应用代码按照**流水线（有向无环图，DAG）**的方式编排，形成可重复的**工作流**，并提供对这些工作流进行编排，部署，管理的平台。

    * pipeline【以中国开源项目】

    

* #### 三维可视化

  * cesium

    **Cesium**为**三维地理空间数据**的优化、可视化、分析提供了端到端的企业级开源解决方案，是当前主流的三维数据可视化框架，开源核心框架

    * 相关优势

      * 多维地图的展示

        * **Cesium**支持**2D**、**2.5D**、**3D**形式的地图展示。3D并不是2D+1D，Cesium还保留了3D的上下文，以提供空间数据的洞察力。

      * 多种数据可视化

        * **Cesium**可以绘制几何图形、高亮区域，地形、影像、矢量、3D模型、动态数据等多种数据可视化展示。

      * 高性能高可扩展性

        * **Cesium**结合云计算、并行计算和GPU技术，基于WebGL利用硬件渲染图形，提供良好的触摸支持，是基于Apache2.0的开源Javascript库，能支持绝大多数的浏览器和mobile

          

  

* ### COG

  * 遥感数据：

    * 作用：共享，科研

    * 遥感数据特点：大数据5V + 时空信息 + 波段信息 + 数以万计的瓦片小文件
    * 遥感数据存储方式：对象存储
    * 遥感数据共享方式：COG【Cloud Optimized GeoTIFF's，云端优化的GeoTIFF】

  * **存储在对象存储上的遥感数据在共享时会有哪些问题？**

    * 每次对文件进行处理都需要将其全部取回到本地，处理完成后再上传到云端COG：通过 S3协议进行**局部数据的读取**，即需要哪部分的数据就读取哪部分数据
    * 消耗大量的上传，下载网络资源被占用，所以出现了局部数据的读取，按需获取

  * COG相对于普通遥感影像怎么做到局部数据读取？

    ![image-20210628124240558](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628124240558.png)

* 案例：OBS【分布式环境下】+COG【瓦片是实体，所以可以进行多波段的展示，不需要重新切片】+Cesium实现遥感数据的共享

  tmf天然可以在球上进行可视化
  
  ![image-20210628124407985](https://raw.githubusercontent.com/shuixianhua-ai/demo/main/image/image-20210628124407985.png)




## 一．GIS History

 * GIS来源：制图的扩展（可视化，分析，问题和解释数据）--》改变人们对于位置的看法--》决策工具--》与生活接轨--》综合多学科（计算机，遥感，地理学，数学，制图学）

   #### 中国GIS发展

   * 陈述彭【地理信息与遥感奠基人】，1977，第一次提出中国应该发展GIS，78杭州遥感会议，提出发展GIS（系统），1980，Wang Zhizhuo（中国摄影测量之父，支持GIS事业），78-80，腾冲遥感实验成功，首次建立地理信息分析主题小组

     

     


   #### 世界GIS发展阶段

   * **before 1960** ：dark ages（without computing，mapping）

   * **1960-1975**：GIS Pioneering（to computer mapping，计算机技术发展，地图打印技术，数据存储，数据输出，显示）
     * 技术的优点：打印机把图片输出；大型数据存储；坐标可以用数据输入
     * GIS（system）的根源：CGIS，Roger Tomlinson（system，GIS之父）[最初用于加拿大土地作物决策]
     * 1968，Roger Tomlinson首次在“A Geographic Information System for Regional Planning”中提出“Geographic Information System”
     * 1970美国人口普查，GBF-DIME文件格式出现以支持地理数据【这是GIS发展的一大步】
     * 除此，英国地形测量局也开始常规地形图开发
     
   * **1975-1990**：GIS software commercialization
     * 哈佛实验室计算机图形学开发第一个矢量GIS，ODYSSRY GIS
     * ODYSSRY GIS导致software 商业化【由政府部门支持-》商业化】
     * 82，微型计算机ARC/INFO启动，1986年，PCARC/INFO随着Intel微计算机的生产而启动。
     * 软件工具：GIMMS（地理信息制作和管理系统），MAPICS，SURFACE，GRID，IMAGE，GEOMAP，MAP等出现
     * 1975 英国举行首次GIS会议（GIS Meeting），Esri会议（conference）1981

   * **1990-2010**（user proliferation– Location-based service）【用户提升-基于位置的服务】
     * 背景：
       * 计算机硬件发展迅速，
       * 多样软件选择和数据获取能力强，
       * 卫星遥感技术发展迅速

     * 发展特征
       * 成为决策的功能被发掘{尤其是交通与土地管理方面}
       * GIS进入教学领域
       * 公司软件兼具矢量和栅格处理
       * 遥感数据可以在GIS中使用
       * GPS引领了汽车导航系统和无人机等伟大的创新产品
   * **2010--**（open source explosion）【GIS与GPS发展使得开源数据剧增】
     * 发展特征
       * GIS数据可存储TB。PB。ZB等
       * 数据普遍，（如TIGER数据，LANDSAT影像）
       * 网上在线数据库存储大量空间数据
       * GIS软件开放的，协作的方式进行【开源的】

#####  	





Introduction（背景：简略；发现的问题，一定要是后文解决的）数据源：来源，范围，可靠程度 TGIS 

## 二．SYSTEM-->science

* Good Child 【GIS(Science)之父】，背景：当时关注点从处理数据到讨论普适性理论的问题【research on these fundamental issue is a better prospect for long-term survival and acceptance in the academy than the development of technical capabilities】
* GISystem——>GIScience的原因
  * 在一些像EGIS的会议上发表的一些研究论文讨论的是一系列的科学问题与知识，这超出了技术的范畴，所以主张转变成science
  * 空间数据处理可以表明我们在做什么，但不能知道为什么这么做
  * 虽然有的人认为GIS是技术驱动的（如CGIS），但实际上它的研究一般都远远超出可预见的范围

* GISystem--》GIScience变化过程
     * 思维的转变【从如何处理数据到为什么这样做】：
     * 从技术驱动（需求驱动，如CGIS）--》菜单驱动（与上面差不多，应用驱动【有模型等更加系统化的技术驱动】）--》‘S’驱动【如果把S看成科学，如何理解】
   * 如何看待GIScience
     * 科学在GIS的角色【GIS中间有些科学问题是普适的，GIS应该是由好奇心驱动的，考虑GIS 的子领域，规划，包含的科学问题
     * 原来认为GIS是科学的工具，将GIS从工具发展到科学，如何讨论其科学问题，如何证明其是科学
* 如何看待GIScience【为什么可以是science】
  * 空间
  * 数据{地理数据是独一无二的，所以相关问题不能纳入更大的范畴}
  * 普适性问题{存在一些问题对所有地理数据都是通用的}



*  空间数据的独特性

  * Anselin（1989）提出的空间依赖性【临近位置相互影响并有相似属性的倾向】

  * 坐标系与投影【椭球面】
  * spatial key可能是多维的
  * spatial key在sql语句方面不一样
  * 数据类型（地理流，tin，栅格，矢量）

  ​	

* GIScience内容：
  * 不平衡/不均衡的研究，存在多样性，动态的特征，研究常常被认为是纯粹的
  * 技术研究还是应用研究，GIS本身偏向应用（需求驱动，人类好奇心或日常需求驱动）
  * 主要是注重解决问题，【pure 当前看不到应用的，而applied是基于需求的】，但实际两者都需要



* 组织/期刊
  * 中国地理顶级期刊：地理学报，遥感学报
  * CSGPC：中国测绘地理信息学会网
  * CAGIS.org.cn：中国地理信息产业协会
  * CPGIS：华人GIS组织
  * {the US National Center for Geographical Information and Analysis}美国国家地理信息和分析中心
    * NCGIA研究的主题主要包括
      * Accuracy and uncertainty in spatial data. 【空间数据的准确性和不确定性】
      * Cognition（认知研究，人们如何思考和用地理概念来思考推理）
      * Modeling and representation（建模与标识，讨论数据建模以及相关分析和决策方法）

* GIScience的内容

  * data collection and measurement数据收集与测量

    * Scientific questions require a depth of understanding of the nature of spatial variation, and one person’s remote sensing may well be another’s geographical information science.
    * 离散化的过程（包括其隐含的泛化，抽象和近似）都被看成是收集，解释，编译的数据。在每个阶段的选择都会对最后的数据使用产生影响

  *  Data capture数据捕获

    * 系统能在解释扫描的地图文件时提供高水平的信息
    * 存在文件质量差或者地图设计存在歧义等问题
    * 现在manual digitizing（手工数字化）虽然成本高，显示效率没有提高，但还是广泛使用
    * 数据捕获的两大趋势
      * 数据汇编和输入过程中尽量避免地图文档
      * 地图设计中相对较小的变化可以使其更容易扫描和解释

  * Spatial statistics空间统计分析

    * 一般来说，空间数据是对现实数据的近似和扩展，不确定性和不准确性较多，所以要考虑精度。以Geostatistics【如kriging】作为统计基础
    * 关于不确定性，模糊算法，统计的概率演算等以及对于空间数据的不确定性，测量，建模和分析传播是地理信息科学的一部分

  * Data modeling and theories of spatial data数据建模和空间数据的理论

    * 数据模型：用来表示数字数据库中地理变化的逻辑框架
    * 空间数据理论早期可能涉及矢量栅格，现在扩展到对象，层复杂对象的层次模型
    * 需要开发一个全面的地理数据建模框架以及相关术语【提供标准】，以及一个可测量具体系统的理想框架【框架需要影响实践】

  * Data structures, algorithms and processes数据结构，算法与流程

    * 许多基础研究都涉及数据的内部表示以及算法
    * 现在这方面有许多挑战性问题：如设计最小花费的效率算法，制图设计，不同数据转换方式
    * 研究<u>有效存储和访问方式</u>

  * Display显示

    * 需要研究动画显示器，三维显示器，用户界面图标与隐喻的使用
    * 需要用电子媒体的思维来思考设计

  *  Analytical tools分析工具

    * GIS是一种支持广泛的空间分析技术的工具，包括创建新的空间对象类别、分析对象的位置和属性，以及使用多类对象和它们之间的关系进行建模的过程。
    * 具体涉及计算面的中心，建立缓冲区，网络最短路径等
    * 分析是GIS 的核心【但如果缺少GIS和空间分析的集成，许多分析会过于简单】
      * 注意：GIS marketplace信息管理而不是分析
      * 空间分析有相对模糊性

  *  Institutional, managerial and ethical issues制度，管理问题

    * 关于GIS管理的一些理论框架在相关的社会学科中已经有了，而现在主要是利用这些框架
    * 因为GIS的引入对于社会地理信息的管理产生重大影响
    * 人们关注GIS对监视和隐私的保护

    

​	

* 对于未来的建议			

  * 对于GIS在某一特定领域的应用的具体问题需要用领域的专业知识解决
  * 需要建立可以对新的研究并且可以建立新的概念体系的教育系统
  * 用地理信息系统技术处理空间信息提出一系列的知识和科学挑战，这表明GIS是科学
  * GIS在空间信息和空间分析两方面逐渐分裂
    * 空间信息强调大型数据库，并提供地理位置一种可访问机制
    * 空间分析强调丰富的功能和一系列数据模型
  * 注意science与system差别，确定GIS的关键科学问题认识到知识广度，实现GIS未来。GISystem是地理信息科学的一种工具，会对GIS有反作用力。

  ​	

​			














## BOM（Bill of Material）

> https://mp.weixin.qq.com/s/XZkR2GVhkxPAUhECcsKgUQ



1. **按照用途分类**

   **工程BOM——EBOM（Engineering BOM）**

   ​	产品工程设计管理中使用的数据结构，它通常精确地描述了产品的设计指标和零件与零件之间的设计关系。对应文件形式主要有产品明细表、图样目录、材料定额明细表、产品各种分类明细表等等。

   **计划BOM——PBOM（Plan BOM）**

   ​	是工艺工程师根据工厂的加工水平和能力，对EBOM再设计出来的。它用于工艺设计和生产制造管理，使用它可以明确地了解零件与零件之间的制造关系，跟踪零件是如何制造出来的，在哪里制造、由谁制造、用什么制造等信息。同时，PBOM也是 MRPⅡ/ERP生产管理的关键管理数据结构之一。

   **设计BOM——DBOM（Design BOM）**

   ​	设计部门的DBOM是产品的总体信息，对应常见文本格式表现形式包括产品明细表、图样目录、材料定额明细表等等。

   **制造BOM——MBOM（Manufacturing BOM）**

   ​	制造BOM信息来源一般工艺部门编制工艺卡片上内容，但是要以设计BOM作为基础数据内容。

   **客户BOM——CBOM（Customer BOM）**

   ​	客户BOM实际上有两个含义，一个指从所有产品机构中筛选出客户订购的产品目录。一个指用户订购的具体规格产品的明细表。这个主要是对有些按照客户管理和组织产品图纸的企业非常实用的种表现形式。这种情况在PDM系统中比较常见，到ERP系统中由于还考虑到不同的客户订购产品对生产计划的影响，情况更加复杂一些，可能还扩展到计划BOM的范畴。

   **销售BOM——SBOM（Sale BOM）**

   ​	销售BOM是按用户要求配置的产品结构部分。对应常见文本格式表现形式包括基本件明细表、通用件明细表、专用件明细表、选装件明细表、替换件明细表、特殊要求更改通知单等等。

   **维修BOM——WBOM**

   ​	维修服务部门的是按维修要求产生的，对应文本格式包括消耗件清单、备用件清单、易损易耗件清单等等。维修BOM信息来源一般从设计BOM对应记录属性中筛选获得消耗件、备用件、易损易耗件明细。

   **采购BOM**

   ​	是根据生产要求外购的原材料、标准件和成套部件等产生的，对应文本格式主要包括外购件明细表、外协件明细表、自制件明细表和材料明细汇总表。采购BOM信息来源一般来源于设计图纸和工艺卡片上信息汇总。由采购部门或生产准备部门根据其安排采购计划和生产计划。

   **成本BOM**

   ​	是由MRPⅡ系统产生出来的。当企业定义了零件的标准成本、建议成本、现行成本的管理标准后，系统通过对PBOM和加工中心的累加自动地生成CBOM。它用于制造成本控制和成本差异分析。其中集成关系最密切的是由PDM 控制的EBOM和MRPⅡ中的MBOM。

   

2. **按照设计软件划分**

   **CAD中的BOM（CAD计算机辅助设计）**

   设计部门既是BOM的设计者，又是BOM的使用者。在设计部门（CAD）中，BOM实际上是零件明细表，是一种技术文件，偏重于产品信息汇总。

   **CAPP中的BOM（CAPP计算机辅助工艺编制）**

   产品经过设计部门设计完毕后，部分电子数据转交工艺部门制订工艺路线（CAPP，Computer Aided Process Planning，计算机辅助工艺过程设计）,成为说明零部件加工或装配过程的文件。它不是技术文件，而是计划文件或指导生产文件。CAPP一般由工艺过程卡、加工工序卡、锻铸热处理卡、检测卡、工装材料工时等汇总信息组成；在一张加工工序卡中由工序（加工步骤）、工时定额（占用工作中心的负荷时间）、加工设备、检测设备、加工工具、工装夹具、材料等组成。

   

   **PDM中的BOM（PDM产品数据管理）**

   PDM（Product Data Management，产品数据管理）是连接CAD/CAPP与ERP的核心模块，避免大量重合数据的产生。现在通过PDM，为ERP系统自动传输BOM数据，只需要几分钟时间。在产品整个生命周期，PDM以数据仓库（所有系统可共用一个数据库）为底层支持，以材料清单（BOM）为其组织核心，把定义最终产品的所有工程数据和文档联系起来，实现产品数据的组织和管理，诸如产品配制管理、图文档管理、工作流程管理、设计变更管理、权限（角色）管理、版本管理、项目管理、维修记录以及日志管理等等。

   

   **ERP中的BOM（ERP企业资源计划）**

   物料需求计划(MRP)系统中BOM是MRP的主要输入信息之一，它利用BOM决定主生产计划项目时，动态确定物料净需求量，知道需要哪些自制件和外购件，需要多少，何时需要，标准用料与实际用料的差异分析。通过建立企业“信息（ERP）”管理和“过程（CAD/CAPP）”技术两条主线，以BOM为信息纽带，以PDM为核心，再结合CAD/CAPP和ERP系统，辅以Internet和EDI系统，就可以真正达到企业信息化建设的目标。



***



## 各阶段需要的汇总表

产品设计过程：合同决策——>总体设计——>工作图设计——>工艺路线分派——>工艺设计——>工装设计——>工时和材料定额汇总。

1. 完成全部设计工作后

   关于该项目的**《文件目录》**，编入文件目录的项目是为正式生产或试制及随机出厂的全部设计文件。

2. 产品图纸设计完成后

   **《图样目录》**：一般针对产品编制，为全部产品的工作图样，一般汇总字段有零部件代号、名称、图纸代号	（一般和零部件代号相同）、图幅、张数、底图总号、备注。

   **《产品零部件明细表》**：产品零部件按照一定序号规则生成。在分页上可能有一些要求。主要汇总字段有幅面、代号、名称和规格、材料、数量、单重、总重、备注（备注一般要填外购外协和借用哪个产品的信息）。

   **《产品分级零部件明细表》**：产品只汇总下属一级零部件明细，然后对下属一级部件另外出其下属一级零部件明细，由多个零部件明细表一起才能完整表达整个产品装配结构，类似PDM4中的零部件结构文卷打开后效果。

   **《系列产品明细表》：**用于反映本系列产品用到的全部零部件在不同规格中的装入关系，可以方便了解整个产品族之间零部件借用关系，在多品种小批量或者变型设计多企业中应用非常多，

   《自制件明细表》、《外购件表》、《外协件表》、《借用件表》、《图样目录》、《标准件表》、《装箱明细表》等

3. 编制产品工艺方案

   用PDM（Product Data Management，产品数据管理）项目管理中单独创建一个文档工作流进行管理。

4.  工艺路线设计，编工艺路线卡或车间分工明细表



***



## 常见的BOM形式

1. **单级展开BOM**

   单级展开格式显示某一装配件所使用的下级零部件。采用多个单级展开就能完整地表示产品的多级结构。对应很多企业(特别是产品零部件数量繁多的企业)的分组明细表即是单级BOM的具体形式。下表为所给的四级产品结构就得到四个单级展开的清单。

   ![image-20230310163628533](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310163628533.png)

2. **多级展开BOM**

   多级展开BOM显示某一装配件所使用的全部下级零部件。采用一个多级展开就能完整地表示产品的多级结构。对应很多企业(特别是产品零部件数量比较少的企业)的产品明细表即是多级BOM的具体形式。下表为所给的四级产品结构对应多级展开BOM表。

   ![image-20230310163727734](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310163727734.png)

3. **缩行展开**

   缩行展开格式是在每一上层物料下以缩行的形式列出它们的下属物料。同一层次的所有零件号都显示在同一列上。缩行展开的格式是以产品制造的方式来表示产品的。

   ![image-20230310163839477](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310163839477.png)

4. **汇总展开**

   汇总展开的格式列出了组成最终产品的所有物料的总数量。它反映的是一个最终产品所需的各种零件的总数。而不是每个上层物料所需的零件数。如某一零件用于多个装配件，汇总展开的清单就有助于确定合适的采购数量。这种格式并不表示产品生产的方式，但却有利于产品成本核算，采购和其他有关的活动。

   ![image-20230310163923299](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310163923299.png)

5. **单层跟踪**

   单层跟踪格式显示直接使用某物料的上层物料。这是一种物料被用在哪里的清单，它指出的是直接使用某物料的各上层物料。产品A的多层结构可用下表表示:

   ![image-20230310163957887](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310163957887.png)

6. **缩行跟踪**

   缩行跟踪的格式指出了某零件在所有高层物料中的使用情况。它可查找直接或间接地使用某零件的所有高层物料，采用这种格式很有价值。现以下表表示。

   ![image-20230310164037798](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310164037798.png)

7. **汇总跟踪**

   汇总跟踪的格式显示所有含有各零件的高层次物料以及每一物料所用零件的数量。这是一张扩展了的”用在哪里”的清单，它列出了所有含有零件的高层次物料。”所需数量”表示装配成该层次的物料所需的零件总数。见下表:

   ![image-20230310164109206](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310164109206.png)

8. **矩阵式的BOM**

   矩阵式的BOM是对具有大量通用零件的产品系列进行数据合并后得到的一种BOM。

   ![image-20230310164205119](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310164205119.png)

9. **加减BOM**

   以标准产品为基准，并规定还可以增加哪些零件或去掉哪些零件。一个特定的产品就被描述为标准产品加上或减去某些零件。下表说明专用产品A/1是在标准产品A上增加零件F和G,同时增加部件C数量到2个，并去掉零件1-1-1制成。这种方法能有效地描述不同产品之间的差异，但不能用于市场预测，也不太适用于MRP。

   ![image-20230310164239575](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230310164239575.png)

10. **模块化BOM**

    在实际应用中，由于产品规格是多变的，零件表按产品结构特点来划分的话，可以分为以下几种:

    * 产品单一，规格基本没有变化。
    * 产品规格多样，可以选择装配
    * 产品系列化，但同一系列中性能变化。
    * 不同产品系列，多种选择装配。




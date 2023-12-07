# **HIT-ICES知识服务构建平台说明文档**

[TOC]



## 1 功能简介

包括多源数据采集、语料库、AI开发辅助、数据资源、本体管理、模型中心、知识图谱模块。

**①多源数据采集**

​        采集非结构化、半结构化和结构化的数据，支持互联网数据的定时爬取。

**②语料库**

​        对现存可用于训练的数据集进行管理。

**③AI开发辅助**

​		支持在线开发、云配置等，通过编辑配置文件，针对不同的训练任务，进行多次训练。并支持训练可视化，根据训练的结果，选择效果较好的模型，进行打包和发布模型。

**④数据资源**

​		根据现有的MySQL数据库的表结构，通过映射规则，生成映射文件，并生成可用的本体。

**⑤Schema管理**

​		采用概念模式（schema）作为本体的载体，通过owl语言描述。包括版本管理，新增、编辑、删除、导入导出，版本融合。

**⑥本体管理**

​		 一部分是本体文件管理，主要针对上传的本体格式文件，完成本体的创建，另一部分是生成本体管理，主要是对根据映射规则生成的本体进行管理。

**⑦模型中心/算法中心**

 		通过AI开发辅助训练的模型，将模型通过镜像打包，集成至模型中心。

**⑧知识图谱**

​		知识图谱通过Docker技术，采用Neo4J容器的原生UI的节点和关系展示方式。

![image-20230330172912178](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230330172912178.png)

## 2 技术架构

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151533634.png" alt="image-20230222092244250" style="zoom:67%;" />



## 3 功能页面展示

### **3.1 登录页面**

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230315112215618.png" alt="登录页面" style="zoom: 33%;" />



### **3.2 系统主页**

![平台首页](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230315112428611.png)

### **3.3 多源数据采集**

【京东数据采集】和【采集数据概览】两部分功能。

**1）京东数据采集**

​        使用Web自动化工具selenium完成对数据来源页面的请求与页面获取，采用lxml的xpath解析器对HTML文档的数据解析，目标信息网站为京东购物平台。

**2）采集数据概览**

​        根据采集的数据，对数据规模、属性分析，生成数据分析结果。

![python数据采集Django](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230222171521407.png)

**Tips：此部分功能只针对京东单一数据源的数据进行爬取，通过关键字Key，模拟京东搜索框，检索商品列表。（需要对多源数据进行扩展，淘宝、拼多多、抖音等）**

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/Y7000P/image-20231126150349049.png" alt="image-20231126150349049" style="zoom:33%;" />

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/Y7000P/image-20231126150132929.png" alt="image-20231126150132929" style="zoom:50%;" />

### **3.4 语料库**

【新增数据集】和【数据集管理】两部分功能。

**1）新增数据集**

根据预先定义的任务要求格式，完善数据集的基础信息（名称、类型、文件等），上传数据集。

![新增数据集](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230223155328401.png)

**预先定义的格式：**

>- re
>
>  - standard
>
>    四个文件
>    relation.csv
>    test.csv
>    train.csv
>    valid.csv
>
>    - relation.csv![img](https://api2.mubu.com/v3/document_image/d4d57595-f244-420d-8041-155f9ced48de-1240121.jpg)
>      存放所有的头尾实体关系以及序号
>
>    - train/test/valid.csv![img](https://api2.mubu.com/v3/document_image/a29c6bab-9491-4b76-91ef-c3266a23f725-1240121.jpg)
>      训练集、测试集、验证集，自行划分；样例：
>      sentence,relation,head,head_offset,tail,tail_offset
>      明朝末年抗清英雄黄得功，本姓王，安徽合肥人后改姓黄,出生地,黄得功,8,安徽合肥,16
>
>  - fewshot
>
>    - rel2id.json![img](https://api2.mubu.com/v3/document_image/edc3a8a0-d29e-4b59-a41b-de3d45668956-1240121.jpg)
>
>    - temp.txt![img](https://api2.mubu.com/v3/document_image/219b075c-81b2-4374-bca7-c199ccdb2cac-1240121.jpg)
>      记录关系模板（由算法决定的数据格式） 样例：
>       0    Other    nothing    has    nothing    to    nothing
>       0    Member-Collection(e1,e2)    member    member    of    collection    collection
>
>    - train.txt/test.txt/val.txt
>      训练集、测试集、验证集 样例：
>      ​{"token": ["the", "crane", "arm", "raises", ",", "swivels", ",", "and", "extends", "to", "a", "maximum", "length", "of", "11", "''", "inches", ",", "just", "like", "our", "own", "poe", "ghostal", "."], "h": {"name": "crane", "pos": [1, 2]}, "t": {"name": "arm", "pos": [2, 3]}, "relation": "Component-Whole(e2,e1)"}
>
>- ner
>
>  由于服务器环境原因无法正常运行
>
>  - standard
>
>  - fewshot
>
>- ae
>
>  - standard
>
>    - attribute.csv
>      属性类别 样例：
>      attribute,index
>      None,0
>      民族,1
>      字,2
>
>    - train.csv/valid.csv/test.csv
>      训练、验证、测试集 样例：
>      sentence,attribute,entity,entity_offset,attribute_value,attribute_value_offset
>      张冬梅，女，汉族，1968年2月生，河南淇县人，1988年7月加入中国共产党，1989年9月参加工作，中央党校经济管理专业毕业，中央党校研究生学历,民族,张冬梅,0,汉族,6
>      相关文献明史岳正，字季方，漷县人,字,岳正,6,季方,10
>      邓卫中（1938-    ）男，汉族，四川宜宾人，四川大学毕业，编审,民族,邓卫中,0,汉族,16
>      王衮，明朝进士,朝代,王衮,0,明朝,3

**2）数据集管理**

查看数据集的详情、删除数据集等。

![数据集管理](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/image-20230223155319608.png)

### **3.5 AI开发辅助**

围绕属性抽取、关系抽取任务，基于已有数据资源和物理资源：1）在线训练；2）训练过程可视化 3）模型的发布。

>任务中心：新增AI训练的任务，例如关系抽取、属性抽取、KGC等
>
>训练管理：选择训练任务、数据集、训练
>
>训练可视化：查看训练任务和训练记录

**（1）任务中心**

![任务中心](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/Y7000P/image-20231126170625454.png)

**（2）训练管理**

![任务管理](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/Y7000P/image-20231126170612671.png)

**（3）训练可视化**

![AI开发辅助-训练可视化](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151442561.png)

### **3.6 数据资源**

从现有数据库，进行数据迁移与使用。目前实现MySQL的数据资源连接，后续考虑加入Neo4j、NoSQL、Hbase等数据库。

数据资源模块的MySQL数据库包括【连接管理】、【添加连接】和【映射文件生成】。

**1）连接管理**

对已经保存的MySQL数据库信息，进行连接选择。

![image-20231126175903434](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/Y7000P/image-20231126175903434.png)

**2）添加连接**

添加新的MySQL数据库连接。

>数据库名称：
>
>数据库类型：MySQL
>
>用户名：
>
>密码：
>
>描述：

![添加MySQL连接](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151443267.png)

**3）映射文件生成**

MySQL数据库和OWL文件之间的映射规则

![映射文件生成](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151443508.png)

### **3.7 本体管理**

本体是在特定领域之中某套概念及其相互之间关系的形式化表达，在知识工程中用本体建模指代知识建模，利用rdf、owl等规范的语言，定义严格完备的逻辑。

>不适合大数据时代知识的多样性、跨领域复杂性，无法满足数据的便捷迭代生产。

本体包括四部分：

1）在线编辑并创建的本体；

2）上传的本体；

3）数据资源转换的本体（MySQL—>OWL）

4）合成的本体（本体A.owl和B.owl融合成本体C.owl）

软件的本体管理包括【本体文件管理】和【本体生成】

**1）本体文件管理**

本体以OWL格式存储，包含本体的增、删、改、查等功能。

- 新增本体：导入本体文件，并补充本体名称、本体描述和相关联的知识图谱类型。

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151445434.png" alt="image-20230223160941793" style="zoom:67%;" />

- 使用WebVOWL对本体信息进行可视化

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151447434.png" alt="image-20230223161751896" style="zoom: 50%;" />

**2）本体生成**

根据已连接的MySQL数据库，根据映射规则，生成本体文件，并在【本体文件管理】中进行统一管理。

![image-20230223161714040](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151449079.png)

>1. 在线编辑并创建本体还未实现；
>2. 本体的融合还未实现（需要复现现有本体算法，复现即可，工程化工作）

### **3.8 模型中心**

考虑从**AI开发辅助**模块中训练出的模型，能够导入至模型中心，形成**模型/算法中心**，同时也可考虑形成算法/模型商城，用户可以上传模型（开发/私密）、知识图谱应用的算法等。

>目前算法/模型是镜像，通过Docker部署，要使用Kubernetes ，管理容器化的应用。

![模型中心首页](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151450539.png)

**（1）关系抽取**

复现或封装现有的算法/模型，以中间件的方式提供服务。

<img src="https://raw.githubusercontent.com/kaikaihit/kaiPic/main/Y7000P/image-20231126184329426.png" alt="image-20231126184329426" style="zoom: 50%;" />

### **3.9 知识图谱**

通过Docker虚拟化，以Neo4j容器进行呈现，原生的节点和关系展示方式。

![知识图谱管理](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151453985.png)

![原生的展示UI](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/202303151716770.png)

## 4 开发要求

### 4.1基于K8s容器资源管理

1. 与Docker虚拟化相关的功能（AI开发辅助，模型/算法商城，知识图谱）代码定位。

2. 学习K8S的资料。

3. 基于K8S完成容器资源管理。

4. 开放各个容器资源控制器的API接口，并形成接口文档。

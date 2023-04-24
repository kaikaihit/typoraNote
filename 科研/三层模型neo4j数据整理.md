# neo4j数据导入导出

## 1.数据导出

1. 停止neo4j数据所在的容器

2. 新建一个临时容器，该容器会在exit后自动删除（假设数据库所在目录/root/zhangkai/fish_threelayers/neo4j_data）

   ```
   docker run --rm -it -v /root/zhangkai/fish_threelayers/neo4j_data:/data neo4j:latest /bin/bash
   ```

3. 执行上述命令后会进入容器，执行导出命令（假设数据库名为neo4j，导出后文件在与数据库同级目录）

   ```
   neo4j-admin dump --database=neo4j --to data/name.dump
   ```

4. 退出临时容器

   ```
   exit
   ```


   **例如：**

```
docker run --rm -it -v /root/zhangkai/djc/data/:/data neo4j:3.5.35-community /bin/bash
```



## 2.数据导入

1. 停止neo4j数据所在的容器

2. 在合适位置新建一个文件夹，文件名为数据库名。

   ```
   mkdir databasename
   ```

3. 新建一个临时容器并进入（与之前的容易用同一个版本的neo4j，挂载同一个data）

   ```linux
   docker run --rm -it -v /root/zhangkai/fish_threelayers/neo4j_data:/data neo4j:latest /bin/bash
   ```

4. 导入数据

   ```linux
   neo4j-admin load --from=/data/dbname.dump --database=databasename --force
   ```

5. 退出

   ```
   exit
   ```

​    **例如：**

```
neo4j-admin load --from=\***.dump --database=*** --force
```





# 数据说明

> airConditional.dump  空调的数据
>
> fabrics.dump  面料、辅料的数据
>
> JDcomputer.dump  电脑数据（旧）
>
> computer_jdcomposition.dump 京东电脑组装方案数据（新）
>
> clothing.dump  服装的组装数据
>
> fishingRod.dump 渔具的图纸(drawing)和配件(part)数据
>
> fishingljl.dump 渔具的简单数据ljl



## 1.空调数据airConditional.dump

![空调的数据](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230405213142768.png)



## 2.服装的组装数据clothing.dump

![image-20230405213450116](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230405213450116.png)



## 3.京东的电脑数据JDcomputer.dump

![image-20230405213358986](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230405213358986.png)



## 4.面料、辅料数据fabrics.dump

![image-20230405213428355](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230405213428355.png)

### 实例：

1. **查询单个大类面料：**

```
MATCH (n:main_type)-[r]->(m:slave_type) where n.name='毛织物' with n,r,m match (m:slave_type)-[r2]->(nb:example) RETURN n, r, m,r2,nb;              
```

2. **查询抽象层与实例层：**

```
MATCH p=(n:begin)-[*]->(m:instance) RETURN p       
```

  

## 5.京东电脑组装方案数据（新）computer_jdcomposition.dump 

![image-20230406114309301](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230406114309301.png)



## 6.  渔具的图纸(drawing)和配件(part)数据 fishingRod.dump

![image-20230406150420244](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230406150420244.png)



## 7.渔具的简单数据 fishingljl.dump 

![image-20230407094039226](https://raw.githubusercontent.com/kaikaihit/kaiPic/main/x1Nano/image-20230407094039226.png)



# 待整理的数据

查看容器挂载目录

```linux
docker inspect  '容器id'  |  grep Mounts -A 20
```



b0b鲁么祺数据

![image-20230406110200792](C:\Users\18807\AppData\Roaming\Typora\typora-user-images\image-20230406110200792.png)



容器25b 中医数据 (47474:7474， 47687:7687)

![image-20230406110830238](C:\Users\18807\AppData\Roaming\Typora\typora-user-images\image-20230406110830238.png)



容器173 computerShow  (27474:7474，27687:7687)

![image-20230406111829687](C:\Users\18807\AppData\Roaming\Typora\typora-user-images\image-20230406111829687.png)







docker run --rm -it -v /root/zhangkai/djc/data/:/data neo4j:3.5.35-community /bin/bash








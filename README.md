# Live-streaming-e-commerce-user-churn-analysis
# 一、背景以及分析目的
>>在今天产品高度同质化的品牌营销阶段，企业与企业之间的竞争集中地体现在对客户的争夺上。“用户就是上帝”促使众多的企业不惜代价去争夺尽可能多的客户。但是企业在不惜代价发展新用户的过程中，往往会忽视或无暇顾及已有客户的流失情况，结果就导致出现这样一种窘况：一边是新客户在源源不断地增加，而另一方面是辛辛苦苦找来的客户却在悄然无声地流失。用户流失分析主要是通过分析用户特征，寻找对用户流失影响较大的用户特征，根据电商领域业务知识，提出产品/平台的运营建议，从而提高用户粘性，降低用户流失率。
# 二、分析思路及分析工具
## 2.1分析思路
![image](https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/ed7841ca-c8e9-4479-9cfb-788b09a47996)
## 2.2分析工具
可视化工具：Power BI  -- 一款微软旗下的免费可视化工具，有着强大的开发者社区，多元可视化工具<BR>
分析工具： Python,excel
# 三、数据预处理
绝大多数情况下，建立模型需要一个完整的数据集，包含空值的数据会使数据挖掘过程陷入混乱，导致不可靠的输出，我们处理缺失值是为了更好地进行建模，因此，在具体实现之前，此步骤也可以放到模型建立之前，先用原始数据进行特征分析。<br>
缺失值处理是对数据中的空值进行删除或者填充，简单的处理方法有直接删除、均值填充、中位数填充、众数填充和特殊值填充，更复杂的有插值填充、Knn均值填充等，这里不进行介绍。常用的缺失值处理方法如下：
    <div align=center><img src="https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/7e7a4333-67a0-4caf-8005-79e7217013c5" width="800" height="300" /></div><br>
   排序后，如有缺失值，会出现在预览区的第一条数据中。观察到需要进行缺失值填充的字段有：使用平台的时间、仓库到顾客地址的距离、使用APP时间、上月订单数量、订单数较去年增加、上月使用的优惠券数量、距上次下单天数。 具体的缺失值处理如下：
<div align=center><img src="https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/6159712b-2551-49bf-856d-b78d41a78f73" width="800" height="300" /></div>

# 四、用户维度特征分析
（1）城市等级分析
![image](https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/bb40a64f-6b95-4bb4-a503-e7b083f81074)
 读图：城市等级为3的流失用户占比为21.4%，城市等级为2的流失用户占比为19.8%,远高于城市等级为1的14.5%

       解图：建议运营团队在城市等级为2和3的城市适当开展运营活动，围绕2，3等级的城市受众设置会员产品，提高用户粘性
（2）性别分析
  <div align=center><img src="https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/59895cc3-40a7-48bd-b44d-5c1a493af517" width="900" height="550" /></div><br>
读图：女性用户是平台的主要用户，女性的流失用户占比为17.7%，男性的流失用户占比为15.5%，基本持平

       解图：建议运营团队根据男性与女性喜欢的直播风格，进行直播内容定向推送，尝试降低其流失率
（3）年龄分析
![image](https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/22ee70a8-f0b7-4fb0-94d8-6cf598e02374)
读图：年龄分组为6的流失用户占比最高，为34.6%，其次是年龄分组为5，流失用户占比为22.5%，另外年龄组别4是最大的受众群体，即使在流失用户占比中排第三位也依旧不能忽视

       解图：建议运营团队鼓励更多年龄分组4，5和6喜欢的直播内容和商品进驻，提高其留存率
 （4）婚姻状况分析
![image](https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/891cd227-ba0c-4315-ab3a-d124ac3fddf5)
    读图：已婚的总用户数最多，且流失用户占比最低，是产品的优质用户群，单身的流失用户占比较高，为26.7%，远高于离异和已婚的用户

       解图：建议运营团队在挖掘新用户时，更注意去吸引已婚的用户，对于现有的单身用户，采取积极留存措施

 （5）上月首选订单类型分析
 ![image](https://github.com/ykdlmu/Live-streaming-e-commerce-user-churn-analysis/assets/146841770/df0d4852-e716-4612-8f86-24ddd858120e)
读图：上月主要订单为Mobile Phone和Household的流失用户占比较多，均超过了25%，其次是上月订单为Fashion的用户

       解图：可能是由于Mobile Phone和Household的商品使用周期较长，用户购买该类商品后，很长一段时间不再有相同的购买意愿，从而造成用户流失
  # 五、利用python进行用户特征相关性分析
  ## 5.1生成哑变量

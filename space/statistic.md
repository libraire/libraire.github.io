# 第x章  统计分析

> 答题场使用基于事件日志机制的多维度数据分析方案

## 背景

在考试与练习的场景中，围绕题、人、场次会有一些杂乱的数据需求，但不外乎是这三个维度间的排列组合。

答题场作为考与练的通用模型，可以从底层出发，以作答明细和作答结果为数据源，为考试与练习的业务提供一些通用的数据分析能力。

而技术方案需要做到：

- **性能**：减少甚至避免`count(*)`的使用，这是计算统计数据常用的方式，但容易出现慢`sql`而影响性能；
- **数据一致性**：需要保证由同一数据源得到的多种统计分析数据的一致性；
- **解耦**：期望统计分析的任务与业务主流程解耦；
- **数据准确性**：期望统计分析的数据能够定期重算，无需人工参与即可防止暂时的程序`bug`对数据的永久性污染；
- **扩展性**：新的统计分析任务应该是易扩展的，期望历史数据被计算后作为新的统计分析任务的初始化数据。

## 具体实现

以作答明细作为数据源的四种统计分析任务为例

#### 作答明细事件日志结构

|  `id`  | `sessionId` | `userId` | `questionId` | `itemIds`  | `result` | `ctime`  |
| :----: | :---------: | :------: | :----------: | :--------: | :------: | :------: |
| 事件id |   会话id    |  用户id  |    题目id    | 选项id拼接 | 作答正误 | 作答时间 |

#### 基于kafka的统计数据分析方案

四种统计分析任务分别是：题目维度，人题维度，场题维度和人场题维度的，具体的内容在[答题场数据能力一览](https://wiki.lianjia.com/pages/viewpage.action?pageId=922282572)。

整套方案的主流程数据流向是：

- 用户作答产生作答明细数据，系统将其转换为事件日志的结构
- 事件日志首先追加到`mysql`数据库，获得事件`id`
- 将携带事件id的事件日志发布到`kafka`
- 统一的“作答明细事件消息消费者”接收该条消息，具体的消费行为分为两步：
  - 四个任务根据旧数据(`old data`)和消息(`delta`)，并行计算新数据(`new data`)；
  - 声明一个数据库事务，在一个事务中去更新四个统计分析任务的数据；

以上方案，利用`kafka`实现了**解耦**，多维度独立进行统计分析任务保证了读的**性能**，利用数据库事务保证了**数据一致性**，

新的统计分析任务只需加入到事件日志的消费行为中即可完成新任务的**扩展**。

#### 方案需要完善的部分

1.**数据准确性**：计算统计数据日表，作为统计数据重算的基准点。

2.**扩展性**：历史数据全量重算的方案，作为新扩展的统计分析任务的初始化数据
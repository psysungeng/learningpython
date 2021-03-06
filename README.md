# learningpython
for girlfriend
# 本程序是《返回抑制对时间知觉的影响》中实验一的展示。
# 实验流程
### 实验设计
#### 自变量为
线索位置（左、右）
目标位置（左、右）
目标之间的SOA（±120ms、±90ms、±60ms、±30ms）
*（备注：负值代表的是，线索目标不一致条件下，第一目标与线索指引的第二目标之间的时间差）*

#### 实验刺激构成
三个正方形（左、中、右），边长均为2.5cm×2.5cm，宽度为10像素；中央正方形呈现在屏幕正中央，左右两个正方形均离中间正方形7.5°视角，约为7.5cm距离。
注视点为“+”字形，长宽为1.5cm×1.5cm，宽度为10像素；呈现位置在中间正方形的正中心。
**线索**：线索呈现方式是将左或者右侧的正方形进行加粗处理，宽度为20像素；
**目标**：目标刺激分为两种形式，一种是垂直线段，一种是水平线段。
线段总长度均为1.5cm，中间部分间隙0.3cm，宽度为10像素。
**目标位置**，垂直线段呈现位置以（左/右）正方形中心**Y轴**垂直，水平线段呈现位置则在（左/右）正方形**X轴**水平

#### 实验刺激呈现顺序以及时间长度
1. FixationDisplay，由三个方形（后续所有中间方形中均存在注视点）组成，呈现时间**300ms**。
2. CueDisplay，左侧或者右侧方形变粗，呈现时间**50ms**。
3. FixationDisplayBack，再次呈现注视界面，呈现时间为**350ms**。
4. FixationCue，中央方形加粗，呈现时间为**250ms**。
5. FirstTarget，呈现第一个目标（可能为垂直线段，也可能为水平线段），呈现时间为(30ms、60ms、90ms或者120ms），并且不消失，一直保持呈现状态。
6. SecondTarget，呈现时间为1500ms。被试需要在该时间段内作出按键反应，否则该trial重新回到刺激集。

#### 实验过程中需要采集的数据
1. 线索出现的位置，数据值为**左**或者**右**；
2. 第一目标是垂直的线段，还是水平的线段，数据值为**水平**或者**垂直**；
3. 第一目标出现的位置，数据值为**左**或者**右**；
4. 若线索出现的位置和第一目标出现的位置一致，则有数据值**一致**，否则则为**不一致**；
5. 第一目标和第二目标之间的**SOA值**
6. 被试按**键的Key**，以及**正确**或者**错误**，被试的反应时也需要采集。


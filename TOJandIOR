#Block循环大法
from psychopy import visual, core, event, data
import numpy as np
import random
from psychopy.visual import ShapeStim
import psychopy.gui
import os, sys, time

# event.Mouse(visible=False)

# gui = psychopy.gui.Dlg()

# gui.addField("Subject ID:")
# gui.addField("gender:")
# gui.addField("age:")

# gui.show()

# subj_id = gui.data[0]
# gender = gui.data[1]
# age = gui.data[2]

# #被试信息记录窗口
# info = {'ID':'', 'gender':'', 'age':''}
# infoDlg = psychopy.gui.DlgFromDict(dictionary = info, title = u'基本信息', order = ['ID','gender','age'])
# if infoDlg.OK == False:
#     core.quit()
# dataFile=open("%s.csv"%(info['ID']+'_'+info['gender']+'_'+info['age']),"a")
# # dataFile.write(info['ID']+'_'+info['gender']+'_'+info['age']+'\n')

exp_data=[]


def Conditions():
    condition=[]
    for i_cue in range(2):
        for i_targetLoc in range(2):
            for i_shape in range(2):
                for i_soa in range(4):
                    # print(i_cue,"/",i_targetLoc,"/",i_shape,"/",i_soa)
                    if i_cue==i_targetLoc and i_shape==0:
                        Line1_type="H"
                        Line2_type="V"
                        consType="equal"
                    elif i_cue==i_targetLoc and i_shape==1:
                        Line1_type="V"
                        Line2_type="H"
                        consType="equal"
                    elif i_cue != i_targetLoc and i_shape==0:
                        Line1_type="H"
                        Line2_type="V"
                        consType="differ"
                    else:
                        Line1_type="V"
                        Line2_type="H"
                        consType="differ"
                    condition.append(list((i_cue,i_targetLoc,i_shape,i_soa,Line1_type, Line2_type, consType)))
                    random.shuffle(condition)
    return condition
Cons=Conditions()

#设定屏幕
expwin = visual.Window(
    (1280, 800),
    monitor='testMonitor',
    color=[255,255,255],
    units="deg",
    fullscr=True)
#设定中间的正方形
RectC=ShapeStim(win = expwin,
    units="deg",
    lineWidth = 2,
    lineColor = [-1,-1,-1],
    fillColor = None,
    vertices=[[-1.25,1.25],[-1.25,-1.25],[1.25,-1.25],[1.25,1.25]],
    )
#设定中间正方形的十字注视点
CrossLineH=ShapeStim(
    win = expwin,
    units="deg",
    lineWidth=2,
    lineColor=[-1,-1,-1],
    vertices=[[-0.75,0],[0.75,0]],
    closeShape=False,
    pos=[0,0])
CrossLineV=ShapeStim(
    win = expwin,
    units="deg",
    lineWidth=2,
    lineColor=[-1,-1,-1],
    vertices=[[0,0.75],[0,-0.75]],
    closeShape=False,
    pos=[0,0])

RectL_pos=[-7.5,0]#左边方形位置
RectR_pos=[7.5,0]#右边方形位置

#垂直线段目标
V1=np.array([[0,0.75],[0,0.15]])
V2=np.array([[0,-0.75],[0,-0.15]])
H1=np.array([[-0.75,0],[-0.15,0]])
H2=np.array([[0.15,0],[0.75,0]])

#常态下的左、右方形
RectL=ShapeStim(win = expwin,
    units="deg",
    lineWidth = 2,
    lineColor = [-1,-1,-1],
    fillColor = None,
    vertices=[[-1.25,1.25],[-1.25,-1.25],[1.25,-1.25],[1.25,1.25]],
    pos=RectL_pos
    )
RectR=ShapeStim(win = expwin,
    units="deg",
    lineWidth = 2,
    lineColor = [-1,-1,-1],
    fillColor = None,
    vertices=[[-1.25,1.25],[-1.25,-1.25],[1.25,-1.25],[1.25,1.25]],
    pos=RectR_pos
    )

#两个目标刺激的间隔时间
SOA=[0.03,0.06,0.09,0.12]
random.shuffle(SOA)

clock=psychopy.core.Clock()
trial_data=[]
# dataFile.write('trialnum,firstlineshape,secondlineshape, conditionType, soa, ACC, RT\n')

for trials in range(len(Cons)):
    clock.reset()
    #中间正方形+注视点
    def CenterBox():
        CrossLineH.draw()
        CrossLineV.draw()
        RectC.draw()
    #设定注视界面A，呈现时间为300ms
    def FixationDisplay():
        CenterBox()
        RectR.draw()
        RectL.draw()

    #设定注视界面B，呈现时间为350ms
    def FixationDisplayB():
        CenterBox()
        RectR.draw()
        RectL.draw()

    #设定中央线索加粗界面
    def FixationCue():
        RectC_Cue=ShapeStim(win = expwin,
        units="deg",
        lineWidth = 10,
        lineColor = [-1,-1,-1],
        fillColor = None,
        vertices=[[-1.25,1.25],[-1.25,-1.25],[1.25,-1.25],[1.25,1.25]],
        )
        RectC_Cue.draw()
        CrossLineH.draw()
        CrossLineV.draw()
        RectR.draw()
        RectL.draw()


    #####################
    #####################
    #需动态设置的部分
    #动态选择线索出现的方位
    def ChooseSide4Cue(a):
        #10代表原来的宽度，20代表加粗后的宽度
        SideL=[]
        SideR=[]
        Side1=[]
        Side2=[]
        if a == 0:
            SideL=10
            SideR=2
        else:
            SideL=2
            SideR=10
        Side1.append(SideL)
        Side2.append(SideR)

        return (Side1, Side2)


    #线索提示界面，需要动态设定的是lineWidth，该值可以根据
    #ChooseSideCue()函数来确定
    def CueDisplay():
        
        #此处暂时设定i值为0。正式实验流程再进行调整
        CueRect_L=ShapeStim(win = expwin,
        units="deg",
        lineWidth = CueLine1[0],
        lineColor = [-1,-1,-1],
        fillColor = None,
        vertices=[[-1.25,1.25],[-1.25,-1.25],[1.25,-1.25],[1.25,1.25]],
        pos=RectL_pos
        )
        CueRect_R=ShapeStim(win = expwin,
        units="deg",
        lineWidth = CueLine2[0],
        lineColor = [-1,-1,-1],
        fillColor = None,
        vertices=[[-1.25,1.25],[-1.25,-1.25],[1.25,-1.25],[1.25,1.25]],
        pos=RectR_pos
        )

        CueRect_L.draw()
        CenterBox()
        CueRect_R.draw()


    #动态设置第一目标出现的形状和位置
    #第一目标出现的位置
    def ChooseSide4Target(b):#参数nTrials指试次的次数*2
        #目标位置出现的集合
        # target_loc=np.array([RectL_pos,RectR_pos])
        # diction=("Left","Right")
        
        #组合成字典，形如
        #{"Left":[-7.5,0];
        # "Right":[7.5,0]}
        # pos_dict=zip(diction,target_loc)
        # pos_list=list(pos_dict)
        # random.shuffle(pos_list)
        #目标1和目标2都是从target_loc中随机选取的，选取规则为不重复选取
        #取值，target_1_loc为Left对应的数组，
        #target_2_loc为Right对应的数组。 
        target_1_loc=[]
        target_2_loc=[]
        # target_1_Key=pos_list[0][0]

        if b==0:
            target_1_value=[-7.5, 0]
            target_2_value=[7.5, 0]
        else:
            target_1_value=[7.5, 0]
            target_2_value=[-7.5, 0]
        target_1_loc.append(target_1_value)
        target_2_loc.append(target_2_value)
        return (target_1_loc, target_2_loc)


    def ChooseLineShape(c):
        #组合线段的vertices参数，其中V_Shape代表垂直线段的两个参数
        #H_Shape代表水平线段的两个参数。
        #V_Shape[0]：V1
        #V_Shape[1]：V2
        #H_Shape[0]：H1
        #H_Shape[1]：H2
        V_Shape=np.array([V1,V2])
        H_Shape=np.array([H1,H2])

        #此处再次组合成数组形式，是为了后续的动态呈现
        # Line_Shape=np.array([V_Shape,H_Shape])
        # Shape_loc=("Vertical","Horizontal")
        # Shape_dic=zip(Shape_loc,Line_Shape)
        # Shape_list=list(Shape_dic)
        # print(Shape_list)
        # random.shuffle(Shape_list)
        # print("fffffffff")
        # print(Shape_list)
        #制定随机化规则
        # Shape_1_Key=Shape_list[1][0]
        # print(Shape_1_Key)
        #防止随机选取的数组重复。
        #？？？关于数据的存储形式需要重新验证，以字符串的形式存储该
        #LineShape的真正样式是最好的。
        Shape1=[]
        Shape2=[]
        
        if c==0:
            Shape_1_value=V_Shape
            Shape_2_value=H_Shape
        else:
            Shape_1_value=H_Shape
            Shape_2_value=V_Shape
        Shape1.append(Shape_1_value)
        Shape2.append(Shape_2_value)
        return Shape1, Shape2

    #定义垂直或水平线段,line1和line2即可以为水平也可以为垂直
    #并且，当line1为水平，则line2为垂直。

    #设定排列组合，使

    def Line1():
        TargetLine1_1=ShapeStim(
            win = expwin,
            units="deg",
            lineWidth=2,
            lineColor=[-1,-1,-1],
            vertices=Line_Shape1[0][0],
            closeShape=False,
            pos=theLoc1
            )
        TargetLine1_2=ShapeStim(
            win = expwin,
            units="deg",
            lineWidth=2,
            lineColor=[-1,-1,-1],
            vertices=Line_Shape1[0][1],
            closeShape=False,
            pos=theLoc1
            )
        TargetLine1_1.draw()
        TargetLine1_2.draw()
        CenterBox()
        RectR.draw()
        RectL.draw()

    def Line2():
        TargetLine2_1=ShapeStim(
            win = expwin,
            units="deg",
            lineWidth=2,
            lineColor=[-1,-1,-1],
            vertices=Line_Shape2[0][0],
            closeShape=False,
            pos=theLoc2
            )
        TargetLine2_2=ShapeStim(
            win = expwin,
            units="deg",
            lineWidth=2,
            lineColor=[-1,-1,-1],
            vertices=Line_Shape2[0][1],
            closeShape=False,
            pos=theLoc2
            )
        TargetLine2_1.draw()
        TargetLine2_2.draw()
        CenterBox()
        RectR.draw()
        RectL.draw()

    #已经提前随机过，所以，每个合成集里面的内容都是随机的。
    a=Cons[trials][0]
    b=Cons[trials][1]
    c=Cons[trials][2]
    d=Cons[trials][3]
    [CueLine1,CueLine2]=ChooseSide4Cue(a)
    [theLoc1,theLoc2]=ChooseSide4Target(b)
    [Line_Shape1,Line_Shape2]=ChooseLineShape(c)
    soa=SOA[d]
    #对应的条件
    firstLineshape=Cons[trials][4]
    secondLineshape=Cons[trials][5]
    conditionType=Cons[trials][6]

    #一个完整的Trials流程是
    
    #注视界面A（固定参数）
    FixationDisplay()
    expwin.flip()
    core.wait(0.3)

    #线索提示界面（变化参数）
    CueDisplay()
    expwin.flip()
    core.wait(0.05)

    #注视界面B（固定参数）
    FixationDisplayB()
    expwin.flip()
    core.wait(0.35)

    #中央线索加粗界面（固定参数）
    FixationCue()
    expwin.flip()
    core.wait(0.25)

    
    #目标1呈现
    Line1()
    Stim_time=expwin.flip()
    
    core.wait(soa)
    #目标2呈现
    #设置按键反应，并记录反应时、正确率等。
    event.clearEvents()

    Line1()
    Line2()
    ResponseTime=expwin.flip()
    # core.wait(1.5)

    keys=event.waitKeys(maxWait=1500,keyList=['f','j','q'])
    # print("error")
    # print(keys[0])
    #加入判断条件，确定正确或错误反应
    #直接判断第一目标的位置是左还是右，即Line_Shape1[0]==[-7.5,0]
    for key in keys:
    # print("fdfsfs")
        if key[0] == "q":
            core.quit()
        if (key[0]=="f" and theLoc1[0]==RectL_pos) or \
            (key[0]=="j" and theLoc1[0]==RectR_pos):
            ACC=1
            RT=ResponseTime-Stim_time
        else:
            ACC=0
            RT=ResponseTime-Stim_time
    trial_data = [trials,firstLineshape, secondLineshape, conditionType, soa, ACC, RT]
    # dataFile.write(trials+','+str(firstLineshape)+','+str(secondLineshape)+','+str(conditionType)+','+soa+','+ACC+','+RT+'\n')
    exp_data.append(trial_data)
# print(exp_data)
output = open("test.xls",'w',encoding='utf-8')
output.write('trialnum\tfirstlineshape\tsecondlineshape\tconditionType\tsoa\tACC\tRT\n')
for j in range(len(exp_data)):
    for k in range(len(exp_data[j])):
        output.write(str(exp_data[j][k]))
        output.write('\t')
    output.write('\n')
output.close()

# np.savetxt("test.tsv",exp_data,fmt="%0.4f",delimiter="\t")
# np.savetxt(data_path, exp_data, fmt='%0.4f',delimiter="\t")
expwin.close()

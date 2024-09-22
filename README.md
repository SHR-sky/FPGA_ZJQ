# FPGA_ZJQ
a repo to store the code of FPGA in EM



## 方案选择

1. 逻辑分析仪            **还行**

   还行

   比较适合新手学东西，了解Verilog，期末考数电的时候，你会觉得无比简单



2. 示波器                    **太简单了**

   有点low



3. 逻辑分析仪+示波器+信号发生器 == 多功能信号分析仪                    **最为推荐**

- 具有简易信号发生器功能，能产生不同的信号及波形 
- 具有示波器功能，能对各种模拟及数字信号进行采集及展示
-  具有逻辑分析仪功能，能对多种数字信号进行采集和传输





---------------------



以下不大推荐，但是有兴趣可以一试；

1. 非接触式血压检测仪

通过多普勒效应测量脉搏波传导速度（PWV），从而测量血压 并且通过

**难点**：测量信号频率300MHZ 需要天线模组负责发送与接收 涉及到高频信号的处理以及阻抗匹配

[高血压及其控制 - 数据集 - VitalStrategies (ckan.io)](https://vital-strategies.l3.ckan.io/zh_CN/dataset/hypertension)

网上论文存在不多

[基于射频信号的非接触式血压监测系统 (usst.edu.cn)](https://joi.usst.edu.cn/html/2020/3/20200312.htm)

（难度应该是最高，最硬核）



2. 健康检测仪

FPGA在此类场景的优势：[FPGA在医疗方面的应用_ct成像 fpga-CSDN博客](https://blog.csdn.net/baidu_34971492/article/details/141419532?app_version=6.3.0&code=app_1562916241&csdn_share_tail={"type"%3A"blog"%2C"rType"%3A"article"%2C"rId"%3A"141419532"%2C"source"%3A"2401_87138318"}&uLinkId=usr1mkqgl919blen&utm_source=app)

采用接触式测量，TI提供成熟的16bit测量方案，采集ECG信号

[zhcu075.pdf (ti.com)](https://www.ti.com/cn/lit/ug/zhcu075/zhcu075.pdf?ts=1726043125551&ref_url=https%3A%2F%2Fcn.bing.com%2F)

然后再采用FPGA数字滤波，进行处理

[基于FPGA的ECG信号滤波与心率计算verilog实现,包含testbench_基于fpga的心率检测系统-CSDN博客](https://blog.csdn.net/aycd1234/article/details/136124732)

通过ECG信号 分析 记录心电图，可用于全天监测，并且引入深度学习模型，对疾病数据集进行学习，从而实现对疾病的预测与诊断

**优点**：信号频率较低 1M以内 **难点**：硬件较为复杂，调试较为困难

在网上有这方面的成品开源代码：[abcgeneraion/ECG-ZYNQ: 基于FPGA的MIT-BIH数据集心律失常五分类算法 (github.com)](https://github.com/abcgeneraion/ECG-ZYNQ)

于知网上也有相关的论文：[基于Zynq的分布式心电图监护系统设计与实现 (51papers.com)](http://m.51papers.com/lw/69/17/wz3367603.htm)

可以完全复刻

然后加入体脂计算（生物电阻测量）

需要解决

- 去除肌电干扰

   肌电干扰的信号频率成分与肌肉的类型有关，一般在 30~~300Hz，而心电信号频率主要集中在 5~~20Hz，所以通过设计**低通滤波器去除肌电干扰**

- 去除工频噪声

   由于工频噪声通常在 50Hz 或 60Hz，所以对原始信号进行频域分析，根据信号频谱设计**带阻滤波器即可滤除工频噪声**。

  [ADS1292R的硬件电路和软件程序_ads1292r等效电路-CSDN博客](https://blog.csdn.net/weixin_43980908/article/details/108856043)

  ADC采集心电

  [zhcu075.pdf (ti.com.cn)](https://www.ti.com.cn/cn/lit/ug/zhcu075/zhcu075.pdf)





---------------------

### 附件

#### 信号处理

原理

[verilog开发的基于dwt小波变换的ecg信号处理 - CSDN文库](https://wenku.csdn.net/answer/d9fc96e4187811ee94bdfa163eeb3507)

实现

[基于FPGA的9/7整数小波变换和逆变换verilog实现,包含testbench_小波变化 fpga-CSDN博客](https://blog.csdn.net/aycd1234/article/details/136333017)

论文

[用小波变换对ECG信号进行去噪研究 (ejournal.org.cn)](https://signal.ejournal.org.cn/cn/article/doi/10.16798/j.issn.1003-0530.2017.08.013)

[超入门级-基于中值滤波处理ECG信号的基线漂移-Python-MIT-BIH数据集_中值滤波去除基线漂移-CSDN博客](https://blog.csdn.net/chrnhao/article/details/120420343)

[verilog实现中值滤波 - 鹅要长大 - 博客园 (cnblogs.com)](https://www.cnblogs.com/happyamyhope/p/5577898.html)

An accurate Electro Cardio Gram system, with peak detection and counting mechanism programmed in Verilog and implimented in Xilinx-FPGA.

The entire code and the analogue steps involved in heart beat processing are explained in the Final Project report (the only pdf file in this repo)

[CountingLogic/ECG-Verilog-FPGA: An accurate Electro Cardio Graph system, with peak detection and counting mechanism programmed in Verilog. (github.com)](https://github.com/CountingLogic/ECG-Verilog-FPGA)https://www.cnblogs.com/happyamyhope/p/5577898.html)
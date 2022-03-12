# Ti平台数采操作快速入门
##	硬件需求
###	物料列表
物料名称	数量	说明
antenna module	1块，ISK或者ODS都可以	芯片模块
mmWaveICBoost	1块	调试板
DCA1000EVM	1块	数采板
电源线	2根 （5V/ >=2A）	供电
Macro USB	2根	控制接口
RJ45 Ethernet cable 网线	1根	数据传输
60pin Samtec cable 排线	1根	连接线
云台(带夹子)	1个	平台支架

###	IWR6843 antenna module
当前我们有IWR6843ISK和IWR6843ISK-ODS
 ![image](https://user-images.githubusercontent.com/15634187/158022939-56d0ca66-dd1f-481d-b9bc-05a57f6f7f0f.png)

Figure 1 1 IWR6843ISK Front View
 ![image](https://user-images.githubusercontent.com/15634187/158022957-a24b35a2-394e-4e18-9220-8926554d32dc.png)

Figure 1 2 IWR6843ISK Rear View
 ![image](https://user-images.githubusercontent.com/15634187/158022966-9a14d490-202b-4ee5-8754-76631dcbdedb.png)

Figure 1 3 IWR6843ISK-ODS Front View
 ![image](https://user-images.githubusercontent.com/15634187/158022973-2365627f-4756-478d-ad54-73061306966c.png)

Figure 1 4 IWR6843ISK-ODS Rear View
###	mmWaveICBoost
carrier board
 ![image](https://user-images.githubusercontent.com/15634187/158022976-cf572e54-9591-4ebf-a64f-89da3d9f6b15.png)

Figure 1 5 MMWAVEICBOOST Front View
 ![image](https://user-images.githubusercontent.com/15634187/158022979-0732de84-9a03-4b8c-8345-0adff7ce1967.png)

Figure 1 6 MMWAVEICBOOST Rear View
###		DCA1000EVM
 ![image](https://user-images.githubusercontent.com/15634187/158022985-c9da85ff-1684-4c60-b32b-433c087134dd.png)

Figure 1 7 DCA1000EVM Front View
 ![image](https://user-images.githubusercontent.com/15634187/158022986-410ff821-b119-40f2-b102-2a6094df325e.png)

Figure 1 8 DCA1000EVM Rear View
##	软件需求
###		mmWave Studio
###		MatLab Runtime Engine v8.5.1

##	平台搭建说明
###		硬件平台搭建
####		扣板与连线
 
![image](https://user-images.githubusercontent.com/15634187/158023074-61a450fb-e1a0-441c-96e6-234f5544c1f2.png)

Figure 3 1 IWR6843ISK-MMWAVEICBOOST-DCA1000EVM 侧视图

![image](https://user-images.githubusercontent.com/15634187/158023073-ccc9dfe9-6914-4142-97d2-d41e2bfc91d4.png)

Figure 3 2 IWR6843ISK-MMWAVEICBOOST-DCA1000EVM 俯视图
![image](https://user-images.githubusercontent.com/15634187/158023077-106a4b26-1d7d-4c3c-a741-7a8793577479.png)



Figure 3 3 IWR6843ISK-MMWAVEICBOOST-DCA1000EVM连线示意图
####	拨码跳线说明
具体拨码可以参考Figure 3 3。软件控制数采模式。

![image](https://user-images.githubusercontent.com/15634187/158023082-c4caa4f2-6659-48dc-b461-029c67564838.png)
![image](https://user-images.githubusercontent.com/15634187/158023083-b5e9ff9c-89ec-4353-8d76-f571ca4e06cd.png)

Figure 3 4 DCA1000EVM拨码


![image](https://user-images.githubusercontent.com/15634187/158023099-a4b7e4d4-a88b-4f66-9a72-22013ec79a0e.png)

Figure 3 5 DCA1000EVM供电
当前外供5V DC电源，switch开关选择DC_JACK_5V_IN。
 ![image](https://user-images.githubusercontent.com/15634187/158023105-09043ed5-1fbb-4a2b-88d6-bd6f3ea8aedb.png)

Figure 3 6 mmWaveICBoost拨码与跳线
 ![image](https://user-images.githubusercontent.com/15634187/158023111-81418aeb-ec16-4f37-b205-7be056ae3f2f.png)

Figure 3 7 IWR6843ISK拨码
###	软件配置与数采
安装好第2章节介绍的软件环境（按照默认目录安装，不要有中文）。搭建平台USB线和网线连接到PC。对单板上电之后，开始软件配置。
####	驱动环境
	检查驱动
设备上电后连接的COM接口（确认驱动安装正确）
 ![image](https://user-images.githubusercontent.com/15634187/158023130-bf1b8eda-eb13-421c-9fe3-fea6113caa47.png)

如果驱动不正确，可以在C:\ti\mmwave_studio_02_01_01_00搜索驱动手动安装。
	设置网络
关闭无线网络（如果有），设置局域网IPV4的IP地址和子网。
 ![image](https://user-images.githubusercontent.com/15634187/158023136-8f7fde62-0a12-4b57-b68e-ccb675510590.png)

####	mmWave Studi软件数采
软件环境安装正确，打开mmWave Studio软件默认启动RadarAPI选项卡窗口。首次打开mmWave Studio软件需要连接到硬件平台，否则会打不开RadarAPI并在output窗口报错。mmWave Studio软件view菜单下可以打开output和luashell窗口。output窗口可以显示RadarAPI配置操作对应执行的命令及其操作结果，其执行命令以ar1.xxx格式体现。luashell是命令行窗口，暂不使用。
使用mmWave Studio软件完成IWR6843x+mmWaveICBoost+DCA1000EVM环境雷达参数的配置，并执行数采流程以及可选的后处理操作。这些配置操作需要借助RadarAPI完成。
 ![image](https://user-images.githubusercontent.com/15634187/158023141-238bbac8-30a2-4171-a692-4f8e6bd46588.png)

RadarAPI正确启动后，output窗口输出如下：
 ![image](https://user-images.githubusercontent.com/15634187/158023144-4a14e77b-d51a-4658-9ce5-9b4377a5759f.png)

 ![image](https://user-images.githubusercontent.com/15634187/158023150-a185c1fd-a05c-41a6-b95f-3231a1d117b1.png)

用户设置存储在C:\Users\ xxx\AppData\Roaming\RSTD\
可以看到RadarAPI窗口按照配置参数功能类别分成了一个个选项卡，逐个选项卡完成配置之后就可以实现数采操作。
快速的数采配置流程有以下步骤：
1、	连接设备，完成Connection tab配置；
2、	导入配置文件，如果有准备好的配置，使用左侧的LoadConfig按钮导入xml格式的配置；
3、	雷达通道静态配置，完成StaticConfig tab配置；
4、	数据通路配置，完成DataConfig tab配置；
5、	雷达波形配置与数采，完成SensorConfig tab配置；
下面逐个步骤进行说明。
#####	连接设备
打开Connection选项卡。
首先需要检测到唯一设备。
按照界面的数字提示执行完6个步骤之后的结果。每个步骤执行的命令及返回结果可以看右侧的Output窗口。
 ![image](https://user-images.githubusercontent.com/15634187/158023158-4ab15391-fb14-4217-a0fa-9c5f4c77599e.png)

下面对6个执行步骤简单说明：
步骤1：当前的单板环境下(IWR6843XXX+mmwave boost+DCA1000EVM)Reset Control不会切换SOPmode，但是会对设备进行reset，可以看到单板上面nrst信号灯闪烁一下。
NOTE: SOP control is only applicable when working with MMWAVE-DEVPACK. When using a
DCA1000 EVM, use the jumpers on the XWR1xxx BOOST to control the SOP settings.
 ![image](https://user-images.githubusercontent.com/15634187/158023163-f46bf088-9765-4b2d-8008-7b626c09b2f5.png)

步骤2：RS232连接，成功状态由红色的Disconnected变成绿色的Connected。按钮也从Connect切换成Disconnet。
非AOP单板自动识别设备。AOP单板需要手动设置“Operating Frequency”和“Device Variant”。
 ![image](https://user-images.githubusercontent.com/15634187/158023167-471b284a-0c4f-40a8-b03d-cbde6e038677.png)

NOTE: Use the default Baud Rate of 921600 bps.（参考【1】）
 ![image](https://user-images.githubusercontent.com/15634187/158023172-0041997b-ed02-4c93-9135-d009a6515725.png)

步骤3：索引到BSS驱动文件位置，加载BSS驱动，studio版本可能有差异，路径供参考。文件路径：C:\ti\mmwave_studio_02_01_01_00\rf_eval_firmware\radarss\xwr68xx_radarss.bin；
 ![image](https://user-images.githubusercontent.com/15634187/158023180-f0a180ae-7f91-4efe-abaa-1a971de71002.png)

步骤4：索引到MSS驱动文件位置，加载MSS驱动，studio版本可能有差异，路径供参考。文件路径：C:\ti\mmwave_studio_02_01_01_00\rf_eval_firmware\masterss\xwr68xx_masterss.bin；
 ![image](https://user-images.githubusercontent.com/15634187/158023183-0fc9ec88-1d1b-41cc-9571-fd7fe4a8f9b0.png)

步骤5：SPI连接，成功状态由红色的Disconnected变成绿色的Connected。按钮也从SPI Connect切换成SPI Disconnet。
 ![image](https://user-images.githubusercontent.com/15634187/158023190-4bef61b5-f51d-4d0c-9408-4006101e329c.png)

步骤6：RF上电，按钮从RF Power-Up变成RF Powered-Up
 ![image](https://user-images.githubusercontent.com/15634187/158023193-77a0517d-ff4f-48e0-8070-b854555931d7.png)

#####	导入配置文件
如果有准备好的配置文件，使用下图所示的导入按钮可以快速导入.xml(LoadConfig)配置或者.json(JSON Import)格式配置。
 ![image](https://user-images.githubusercontent.com/15634187/158023200-27db444b-ee0f-479c-b8fe-44f77459f92d.png)

#####	雷达通道静态配置
打开StaticConfig选项卡。
 ![image](https://user-images.githubusercontent.com/15634187/158023203-8a8a6fa1-7dc1-4e1e-a453-63b2895561c8.png)

按照需求依次配置项目如下：
	选择TX/RX通道，芯片级联方式
	ADC位宽和数据格式
	ADC模式
	频率范围约束
	初始化RF
 ![image](https://user-images.githubusercontent.com/15634187/158023213-3369a82a-70ca-41f4-adf8-98f0132148d7.png)

#####	数据通路配置
打开DataConfig选项卡。
 ![image](https://user-images.githubusercontent.com/15634187/158023240-a7619045-0b16-40fa-9c40-21764296035f.png)

依次设置项目如下：
	数采通路
	时钟配置
	LVDS通路
 ![image](https://user-images.githubusercontent.com/15634187/158023243-0d1bfd87-4ea5-40e5-bb61-f0ad8d1d91e9.png)
![image](https://user-images.githubusercontent.com/15634187/158023247-036080dd-09e4-4585-8cc0-a7156e3cdb7d.png)

#####	雷达波形配置与数采
打开SensorConfig选项卡。
设置chirp和profile参数， 把profile和chirp、frame及其他RF参数关联起来。参考下图的1/2/3步骤配置。
 ![image](https://user-images.githubusercontent.com/15634187/158023257-64e571a5-6e62-4887-bf51-39410682239f.png)

Figure 3 8 雷达波形配置与数采操作指示
补充说明两点：
第1点，chirp参数配置注意事项。
 ![image](https://user-images.githubusercontent.com/15634187/158023352-229292d6-0348-4a73-83e8-2edeeec25270.png)

上面步骤第2步chirp参数中，如果使用多天线进行室内目标跟踪的配置，比如3T4R，需要先点击“set”按钮，然后点击“manage chirps”按钮，进行如下配置。
 ![image](https://user-images.githubusercontent.com/15634187/158023355-d18c9344-02bc-4c9d-8f51-1c2cfd2f1990.png)

第2点，frame参数配置注意事项。
 ![image](https://user-images.githubusercontent.com/15634187/158023359-2d29251c-41c6-484f-9b13-5aba50f152e1.png)

步骤3 frame参数配置中，“No of Frames”如果配置为0，表示持续数采，需要手动停止。否则采集完指定数量的数据帧之后停止数采。

profile中chirp波形相关的参数设置可以参考【3】、【4】、【5】并使用RampTimingCalculator选项卡进行计算。
 ![image](https://user-images.githubusercontent.com/15634187/158023368-c86a82c7-e39a-4f9e-9b01-549e21b38969.png)

完成Figure 3 8波形参数配置1/2/3之后，连接触发DCA1000EVM进行数采。
执行Figure 3 8操作4“SetUp DCA1000”，连接DCA1000EVM。连接成功后正确显示FPGA版本号。connect按钮切换为disconnect。DCA1000EVM参数通过UDP协议传输到PC。UDP包延时按照默认值25us，跟速率约束关系参考【3】。
  ![image](https://user-images.githubusercontent.com/15634187/158023375-1061c834-7c7e-41cc-9dc7-76f2c16337cd.png)
![image](https://user-images.githubusercontent.com/15634187/158023378-bfba5a82-b3da-4583-a57f-f71d9de2cee1.png)

执行Figure 3 8操作5 “DCA1000 ARM”，启动DCA1000EVM FPGA，约2s之后执行操作6“Trigger Frame”。保持默认的数据存储位置。

如果配置“No. of frames”为0，表示无限数采，需要执行操作7“Stop Frame”手动停止采数。否则采集完设置好的帧数后自动停止数采。显示下图的“Record is completed”表示数采成功。
 ![image](https://user-images.githubusercontent.com/15634187/158023383-05a395c7-4f69-436a-9350-34e87c0d9d8d.png)

采集数据过程中“DATA_TRANS_PROG_LED1”不断闪烁。采集完停止闪烁。数据存储好的时候会闪烁一下。
 ![image](https://user-images.githubusercontent.com/15634187/158023387-5d486d63-cf67-4f53-9757-4132f08e3642.png)

操作5~7可以多次执行进行采数。如果修改了采集的帧数“No. of frames”，需要执行操作4中“Reset and Connect”，再执行5~7进行数采。
成功完成数采之后，执行操作8“PostProc”。
 
 ![image](https://user-images.githubusercontent.com/15634187/158023389-518e607c-51a4-427c-9ffe-89e367ecf673.png)

自带Demo用test source进行PostProc演示效果如下：
![image](https://user-images.githubusercontent.com/15634187/158023392-743b1f57-2860-427b-bf06-4485c7a694b3.png)
![image](https://user-images.githubusercontent.com/15634187/158023396-3ade8a37-8fa0-4ee5-879b-003749bda26b.png)

 
####	数据存储格式
	存储文件
The file name to store the raw ADC data is given by the user in the SensorConfig Tab. The DCA1000 EVM appends “Raw_n” to the file name given by the user. After 1 GB of capture, the DCA1000 EVM will start capturing the data into another file. Each subsequent file will have the test “Raw_n” appended to the user given filename where n is a number starting from 0. For example, if the user given filename is adc_data.bin, after the capture, user will see adc_data_Raw_0.bin, adc_data_Raw_1.bin etc. files in the mmWaveStudio\PostProc (default location of the raw ADC data files) folder.
	数据格式
Note that since the data is captured using a UDP protocol over Ethernet interface, there could be occasional packets drops. The data from the dropped packets is filled with zeros in the file and can be ignored for analyses.
Notation:
– RxkIn: The n th in-phase sample corresponding to k th RX channel.
– RxkQn: The n th quadrature-phase sample corresponding to k th RX channel.
– N: The number of samples per chirp.
Sample binary file produced by mmWave。
 ![image](https://user-images.githubusercontent.com/15634187/158023402-17bc0a7a-b283-4c28-af4b-cdeb72674f95.png)

6843 non- interleaved format- complex 4 channel
 
![image](https://user-images.githubusercontent.com/15634187/158023404-28471d91-ea17-4128-bcc0-76f2116754f1.png)

• From mmWave studio the raw ADC data (without any headers) is stored in the file name provided sensor config window.
• The data format remains unchanged in the ‘continuous streaming’ mode where one can think of the data collected as belonging to a single large chirp.
数据格式说明参考【2】和【4】中“Format of the raw captured file”。
3.2.4	雷达波形参数计算
使用“RampTimingCalculator”选项卡完成chirp参数计算。
需要输入线性调频斜率“Slope(MHz/us)”，“ADC samples”和“Sample Rate(ksps)”三个参数，其他相关参数约束自动加入，完成需要配置参数计算。
 ![image](https://user-images.githubusercontent.com/15634187/158023409-f408d4c1-ea53-4161-86ff-f576a936592f.png)

## 改进点
- 使用lua脚本自动化
- 使用DCA1000EVM CLI命令自动化
- 集成到可视化环境
##	参考资料
【1】	60GHz mmWave Sensor EVMs(User's Guide).pdf
【2】	2047.mmWave_sensor_raw_data_capture_using_DCA1000_xwr6843.pdf
【3】	DCA1000EVM Data Capture Card.pdf
【4】	mmwave_studio_user_guide.pdf
【5】	Programming Chirp Parameters in TI Radar Devices.pdf

# 直接部署 vCenter Server （基于自带Linux）

​     在学习vSphere的时候，vCenter Server与ESXi是必不可少的产品。推荐在物理主机上安装VMware ESXi，并且在ESXi的物理主机中安装vCenter Server的虚拟机。

但受实验条件限制，有的朋友不能在物理主机测试VMware ESXi与vCenter Server，这个时候就可以使用VMware Workstation软件进行测试。但测试的时候也是有技巧的。在Workstation中创建ESXi的虚拟机并安装ESXi软件，这个没有争论，就是vCenter Server，如果完全模拟生产环境，再在ESXi的虚拟机中，安装嵌套的vCenter Server的虚拟机没有必要，因为vCenter Server占用的资源相对较多。为了获得较好的体验，推荐将vCenter Server直接部署在Workstation的虚拟机中。

在vSphere 6.0的时候，在Workstation中创建Windows Server 2008 R2或Windows Server 2012、Windows Server 2016的虚拟机并在虚拟机中安装Windows版本的vCenter Server 6.0，也可以在Workstation中部署vCenter Server Appliance。从vSphere 6.5开始，在生产环境中推荐使用vCenter Server Appliance 6.5。现在vSphere最新版本是6.7.0 U3，本节介绍在Workstation的虚拟机中部署vCenter Server Appliance 6.7.0 U3的内容。

#### 1 第一阶段安装

在VMware Workstation中部署vCenter Server Appliance 6.7比较简单，只要用虚拟光驱加载vcsa 6.7的ISO文件，导入其中的OVA文件即可。下面介绍主要步骤。（本节以VMware-VCSA-all-6.7.0-14367737.iso为例）。

（1）使用虚拟光驱加载VMware-VCSA-all-6.7.0-14367737.iso，浏览展开VCSA文件夹，可以看到vCenter Server Appliance的OVA文件。如图1所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation](https://s4.51cto.com//images/blog/201909/21/1018b2212b068d439e0274a3fb5b8a06.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/ea0195a9e030680cf0d93b69d722fdaa.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图1 vCenter Server Appliance的OVA文件

（2）在VMware Workstation， 单击“文件”菜单选择“打开”命令，在“打开”对话框中，浏览第（1）步加载的虚拟光驱的vCenter Server Appliance文件夹，选择OVA文件。如图2所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_02](https://s4.51cto.com//images/blog/201909/21/4a9703dbfef94e91661a54f37ce15de0.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/c47fe1c549192ddf9cb4a1de86bef8bf.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图2 浏览选择OVA文件

（3）在“导入虚拟机”对话框中，弹出VMware vCenter Server许可协议，接受许可协议。

（4）设置新虚拟机的名称（本示例为vcsa-80.5），单击“浏览”选择新虚拟机的存储路径 ，如图3所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_虚拟化_03](https://s4.51cto.com//images/blog/201909/21/291924a752f2e9007bfc6a6b71a61c1e.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/d789ef18ed89a6fbeeec3e830cb58cdf.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图3 设置虚拟机名称和导入位置

（5）在“部署选项”对话框，选择“Tiny vCenter Server With Embedded PSC”，如图4所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_虚拟化_04](https://s4.51cto.com//images/blog/201909/21/f90828f2a452da3481a6805a204ef2b8.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/e4257f6ae3fafc2be18aff1ec9d7f08c.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图4 微型置备

（6）在“属性”对话框中，在“Networking Configuration”选项中，在“Host Network IP Address Family”文本框中输入ipv4；在“Host Network Mode”文本框中输入static；在“Host Network IP Address”输入当前要部署的vCenter Server的IP地址，本示例为192.168.80.80；在“Host Network Prefix”输入子网掩码位数，在此为24（表示255.255.255.0）；在“Host Network Default Gateway”中输入网关，当前示例为192.168.80.2，在“Host Network DNS Servers”文本框中输入DNS名称，本示例为192.168.80.2，在“Host Network Identtity”输入192.168.80.80；如图8-3-15所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_05](https://s4.51cto.com//images/blog/201909/21/044e756943bc9d41b5cf1ea588095ab7.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/bebbb5b6bf0f9da4347d9113f3e5b941.jpg?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图5 网络配置

（7）单击“SSO Configuration”选项卡，设置SSO账号（默认为administrator@vsphere.local）密码，在此需要设置复杂密码（大小写字母、数字、非数字字符、长度超过6位）；）单击“System Configuration”选项卡，设置root账号密码。然后单击“导入”按钮，开始导入vcsa。如图6、图7所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VCSA_06](https://s4.51cto.com//images/blog/201909/21/e932af8864c9386f957decf4934692e0.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/b217bdea50bf3117affa68d51277bf9d.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图6 设置SSO密码

[![在Workstation 15中导入vCenter Server Appliance 6.7_VCSA_07](https://s4.51cto.com//images/blog/201909/21/8800e8a67d3244c8aa3ecee6234a5a78.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/0f7ec276d4c726d75e44d08c13aeb346.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图7 设置root密码

（8）导入虚拟机完成之后，vcsa虚拟机自动启动，修改虚拟机配置，将网卡从默认的“桥接”改为“NAT”，如图8所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_虚拟化_08](https://s4.51cto.com//images/blog/201909/21/5060e94d8cc20007de17ae3cdfca603a.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/cbdda1553a09f306999b2f379ebb18da.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图8 修改网络

【说明】当前计算机VMnet8网络配置为192.168.80.0，如图9所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_虚拟化_09](https://s4.51cto.com//images/blog/201909/21/21cff2f5cff606ff64c7c29928f5bc4f.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/fc2d3dbc753d9518e391190bf07f9398.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图9 虚拟机网络

（9）之后耐心等待，直接在VMware Workstation的控制台中出现设置的管理地址，如图10所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VCSA_10](https://s4.51cto.com//images/blog/201909/21/988c827ddb77162c256dd1c496e5da8b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/092d4e31458fe77bcc48d3bf2cc279fc.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图10 已经配置IP地址

（10）在虚拟机控制台中，按F2，进入网络配置→DNS配置，将主机名称从默认的photon-machine，修改为192.168.80.80（本示例中VCSA安装的地址），如图11、图12所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_11](https://s4.51cto.com//images/blog/201909/21/39b8af7c877948a5d73d53dec83f6008.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/23621522277ea85060fda4207aedcbd5.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图11 修改名称

[![在Workstation 15中导入vCenter Server Appliance 6.7_VCSA_12](https://s4.51cto.com//images/blog/201909/21/0b7ce27687129f78035820a49e823f54.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/0bfed185ed570b6a3b8a31aec5464867.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图12 修改计算机名称为IP地址

如果你网络中有DNS，可以配置DNS地址并输入域名。例如我网络中DNS的地址为172.18.96.1，域名为heinfo.edu.cn，我可以创建名为vcsa的A记录，将其解析为192.168.80.80，此时可以输入vcsa.heinfo.edu.cn。

（11）修改hostname之后保存退出，如图13所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VCSA_13](https://s4.51cto.com//images/blog/201909/21/f5240cf3a7b334c01e73b038c91acfb3.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/ca4fec64cd2e6bfc268a826accbf423a.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

13 返回到控制台

#### 2 第二阶段安装

然后开始第二阶段的安装。

（1）此时打开IE浏览器中，输入https://192.168.80.80:5480，首先会让输入密码（图7设置的root密码），会显示系统配置界面，单击“设置”，如图14所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VCSA_14](https://s4.51cto.com//images/blog/201909/21/f5a47222990fde81eb6167145cb2f60e.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/537ee7aadf7feacac32c8d112855b229.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图14 设置

（2）在“设备配置”中确认系统名称为图12中设置的IP地址或名称，如图15所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_15](https://s4.51cto.com//images/blog/201909/21/9ed1291c5b33976ea6e0f1fbc532b8d8.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/51d293ba1f46c014003a820664faa160.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图15 设备配置

（3）在SSO配置中指定域名为vsphere.local，设置SSO密码，如图16所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_16](https://s4.51cto.com//images/blog/201909/21/46877ef7037732623230bd337ac7eca9.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/606c843f1c726a563ea55303277fe064.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图16 SSO配置

（4）在“即将完成”对话框中确认vCenter Server Appliance的信息，如图17所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_虚拟化_17](https://s4.51cto.com//images/blog/201909/21/a02e2ef4039a6e272abede042b90bd9c.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/cb11a5fcdf83d0c36c4f35e7c4d0777f.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图17 即将完成

（5）等vCenter Server系统启动完成之后，配置完成，如图18所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_18](https://s4.51cto.com//images/blog/201909/21/7042d68bf1c87591e65ec2316c3bb549.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/2299742c744888a56a36c15af19cdeb1.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图18 部署完成

（6）安装完成可以进入vCenter Server界面，如图19所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_19](https://s4.51cto.com//images/blog/201909/21/4a47c59436f8aded6b48c997010f344e.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/c1b92a06f682016f421560ba00aea7a5.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图19 vCenter登录界面

（7）登录进入vCenter Server，如图20所示。

[![在Workstation 15中导入vCenter Server Appliance 6.7_VMware Workstation_20](https://s4.51cto.com//images/blog/201909/21/353ad9c55fd67168d8a496f17bcd136e.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)](https://s4.51cto.com//images/blog/201909/21/a5acf0f6a571f586b649a32bd689a211.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_30,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

图20 登录进入



 原创

[王春海](https://blog.51cto.com/wangchunhai)2019-09-21 21:30:29博主文章分类：[VMware vSphere](https://blog.51cto.com/wangchunhai/category1)©著作权

*文章标签*[VMware Workstation](https://blog.51cto.com/topic/vmwareworkstation.html)[VCSA](https://blog.51cto.com/topic/vcsa.html)[虚拟化](https://blog.51cto.com/topic/xunihua.html)*文章分类*[虚拟化](https://blog.51cto.com/nav/virtual)[云计算](https://blog.51cto.com/nav/cloud)*阅读数*1.6万
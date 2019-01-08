＃在Linux上安装Quartus Prime

Quartus Prime是Altera用于FPGA的开发工具。通过它，可以使用块或使用HDL（例如VHDL或Verilog）进行开发。它支持Windows或Linux环境，但是在Linux环境中，它的安装并不像在Windows中那么容易。

本教程在Ubuntu 18.04操作系统上运行和测试。但是，早期版本也可以使用它略有不同，特别是对于* libpng12-0 *库，因为您的系统可能仍然支持这样的库。

##下载工具

它有一些版本，Pro版本最完整，Lite版本最简单。在本教程中，将介绍Lite版本的安装，因为这是它的唯一免费版本。该工具可以从[Altera]网站下载（http://fpgasoftware.intel.com/18.0/?edition=lite&platform=linux&download_manager=dlm3）。

要下载，您需要英特尔FPGA程序中的帐户，但此帐户的创建是免费的，可以[在此链接]（https://www.intel.com/content/www/us/en/）完成forms / fpga / fpga-individual-registration.html）。

建议下载18.0版，选择Combined Files *选项，其大小为6.2 GB。

##准备系统

Quartus，主要是从Quartus II到Quartus Prime的变化开始有64位*系统的原生支持，但仿真工具* ModelSim *因此，没有必要安装一些32- *位*。可以通过在终端中执行这些命令来完成这些库的安装：

    $ sudo dpkg --add-architecture i386
    $ sudo apt update
    $ sudo apt install libxft2：i386 libxext6：i386 libncurses5：i386 bzip2：i386

对于libpng12-0 *库安装，尤其是对于较新的操作系统，例如Ubuntu 18.04，必须从外部下载并手动安装库，因为已经从系统中停止了这样的库。要下载并安装库，请在终端中运行以下命令：

    $须藤wget的http://ftp.us.debian.org/debian/pool/main/libp/libpng/libpng12-0_1.2.50-2+deb8u3_amd64.deb
    $ sudo dpkg -i libpng12-0_1.2.50-2 + deb8u3_amd64.deb

##安装Quartus

下载Quartus和环境配置后，您已完成系统的安装。首先，必须解压缩下载的文件。在解压缩的文件夹中，您可以看到* setup.sh *文件，但是，这将无法运行，因为使用它，安装需要更长时间。

在components文件夹中是Quartus安装的可执行文件，这是为安装执行的。最初，您应该使用以下命令运行* QuartusLiteSetup-18.0.0.614-linux.run *：

    $ ./QuartusLiteSetup-18.0.0.614-linux.run
最初，您必须接受Quartus安装的许可证。接受字词后，您可以选择其中的Quartus将要执行的文件夹，并建议该文件夹`/ home / user中/ intelFPGA / 18.0`，就像原来，除了默认的文件夹是called` intelFPGA_lite` ，这不是* ModelSim *的默认值，因此建议使用`intelFPGA`。

您现在可以选择要安装的组件。建议分别安装每个* main *软件*（* Quartus Prime，Quartus Help和ModelSim *），因此组件的选择应与下图相同：
！[Componnentes到被安装在教程的这个部分（https://raw.githubusercontent.com/arthurmteodoro/install-quartus-linux/master/images/1_comps_install_quartus.png）

在此之后，只需要继续安装，等待安装确认屏幕。即将此屏幕上，你必须按*完成*按钮，关闭GUI，然而，在这样的设施正在运行的终端，应用程序将不会停止正在只是需要关闭它使用手动按Ctrl + C *结束申请。

完成后，Quartus已经安装完毕，但是仍然需要安装* Quartus Help *和* ModelSim *。

##安装Quartus帮助

Quartus Help的安装非常简单，而且命令 

    $ ./QuartusLiteSetup-18.0.0.614-linux.run
   在* components *文件夹中引导安装程序。接受许可证后，有​​必要选择安装哪个文件夹，并选择安装Quartus的文件夹。如果您选择了本教程中推荐的文件夹，则无需担心，因为所选的文件夹是默认的Quartus帮助。

与Quartus一样，安装后，图形界面将关闭，但终端中的应用程序将继续处于活动状态，必须以* Ctrl + C *结束。

##安装ModelSim

因此，像安装Quartus帮助一样，安装ModelSim很容易。也可以执行命令

    $ ./ModelSimSetup-18.0.0.614-linux.run
运行后，必须选择* ModelSim  -  Intel FPGA Starter Edition *版本，因为此版本是免费的。

与Quartus帮助一样，您必须选择与Quartus相同的安装路径，但默认路径是推荐路径。

安装程序以及其他安装程序在安装后将无法完成，并且还必须终止。

## Quartus与系统的执行和集成

###运行Quartus

要在Linux上运行Quartus，请运行该命令

    $ /home/username/intelFPGA/18.0/quartus/bin/quartus --64bit
因此，Quartus将正常运行。

###与系统集成
但是，强烈建议不要将Quartus与操作系统集成。

####`PATH`变量 
为了能够从终端运行Quartus而不必键入整个完整路径，可以为此创建一个`PATH`变量。首先，您需要使用以下内容在`/ etc / profile.d`中创建`quartus.sh`文件：

    export PATH = $ PATH：/home/username/intelFPGA/18.0/quartus/bin
之后，您需要使文件可执行：

    chmod + x /etc/profile.d/quartus.sh
   因为`profile.d`文件仅在登录时运行，所以必须执行用户的注销*或者只是在终端上执行`$ source / etc / profile.d / quartus.sh`。

####创建系统图标
要在系统上安装Quartus Prime图标，需要在`〜/ .local / share / applications`中创建`quartus.desktop`文件，其中包含：

    [桌面入口]
	版本= 1.0
	名称= Quartus Prime标准版v15.1
	Comment = Altera FPGA的Quartus Prime设计软件
	Exec = $ HOME / intelFPGA / 18.0 / quartus / bin / quartus --64bit
	Icon = $ HOME / intelFPGA / 18.0 / quartus / adm / quartusii.png
	终端=假
	Type =应用程序
	类别=发展
### USB-Blaster连接驱动程序
Altera USB-Blaster连接驱动程序仅支持某些Linux发行版，因此需要进行一些更改才能完全处理其他发行版。

最初，应在`/ etc / udev / rules.d /`中创建`51-alter-usb-blaster.rules`文件，其中包含：

    SUBSYSTEM ==“usb”，ATTR {idVendor} ==“09fb”，ATTR {idProduct} ==“6001”，MODE =“0666”
	SUBSYSTEM ==“usb”，ATTR {idVendor} ==“09fb”，ATTR {idProduct} ==“6002”，MODE =“0666”
	SUBSYSTEM ==“usb”，ATTR {idVendor} ==“09fb”，ATTR {idProduct} ==“6003”，MODE =“0666”
	SUBSYSTEM ==“usb”，ATTR {idVendor} ==“09fb”，ATTR {idProduct} ==“6010”，MODE =“0666”
	SUBSYSTEM == “USB” idVendor ATTR {} == “09fb” idProduct ATTR {} == “6810”，MODE = “0666”
因此，必须使用`udevadm`命令*重新加载文件*。注意：在执行这样的命令之前，必须拔掉所有Altera组件！

`udevadm control --reload`

要验证安装是否成功，请连接设备Altera并运行：

    $ /home/username/intelFPGA/18.0/quartus/bin/jtagconfig
您将使用类似于以下的用途输出：

    1）USB-Blaster [USB 1-1.1]
	  020B30DD EP2C15 / 20
如果输出没有卡的名称，则在初始化`nios2 tools`时出现问题。要解决此问题，请运行：

    #mkdir / etc / jtagd
	＃的Cp /home/nome_do_usuario/intelFPGA/18.0/quartus/linux/pgm_parts.txt /etc/jtagd/jtagd.pgm_parts

并重新启动jtagd：

    $ jtagconfig
    1）USB-Blaster [2-4]
    020F30DD
    $ killall jtagd
    $ jtagd
    $ jtagconfig
    1）USB-Blaster [2-4]
    020F30DD EP3C25 / EP4CE22

如果收到有关* linux64 *的错误消息，请在`/ home / username / intelFPGA / 18.0 / quartus`中创建一个从* linux *到* linux64 *的符号链接：

    ＃LN -s /home/nome_do_usuario/intelFPGA/18.0/quartus/linux /home/nome_do_usuario/intelFPGA/18.0/quartus/linux64

##运行ModelSim

ModelSim安装后，需要对某些文件进行一些修改才能正确操作，主要是因为Linux支持仅适用于某些库。

可以按照本教程的各个部分或使用本教程中提供的*脚本*手动进行上述更改。

###内核兼容性4.x及更高版本
ModelSim在* kernel * Linux的第4版中存在问题。要解决此问题，您需要更改`vsim`文件以生成此兼容性。在文件中，应该更改行206

    vco =“linux_rh60”;;
   至

    vco =“linux”;
   
###库依赖* freetype2 *

* freetype2 *库已从版本2.5.0.1-1更新到2.5.0.1-2，导致ModelSim中出现以下错误：

    $ vsim
	启动脚本出错：
	初始化问题，退出。
	初始化问题，退出。
	初始化问题，退出。
	   执行时
	“EnvHistory ::重置”
	   （程序“PropertiesInit”第3行）
	   从内部调用
	“PropertiesInit”
	   从内部调用
	“ncFyP12  -  +”
	   （文件“/opt/questions/linux_x86_64/../tcl/vsim/vsim”第1行）
	**致命：在vlm进程中读取失败（0,0）
或

    $ vsim
	启动脚本出错：
	初始化问题，退出。
	初始化问题，退出。
	    执行时
	“静静地初始化INIFIF”
	    从内部调用
	“ncFyP12  -  +”
	    （文件“/ mtitcl / vsim / vsim”第1行）
	**致命：在vlm进程中读取失败（0,0）
此问题的解决方案是将二进制文件直接下载并链接到ModelSim *脚本*。二进制文件可以从[link]（https://dl.dries007.net/lib32-freetype2-2.5.0.1.tar.xz）下载。一旦下载完成后，该文件夹的内容（即LIB32文件夹中）应该被复制到`/ home / user中/ intelFPGA / 18.0 / modelsim_ase /`脚本*`/home/nome_do_usuario/intelFPGA/18.0/应更改modelsim_ase / vco`，在``dir =`dirname“$ arg0”```出现后插入以下行。

    export LD_LIBRARY_PATH = $ {dir} / lib32 /
但是，从Quartus启动ModelSim时会发生同样的错误。要解决此问题，应将以下行放在尽可能靠近`/ home / username / intelFPGA / 18.0 / quartus / adm / qenv.sh的位置。

    export LD_LIBRARY_PATH = / home / polo / intelFPGA / 18.0 / modelsim_ase / lib32：$ LD_LIBRARY_PATH

###创建系统图标
要在系统上安装ModelSim图标，需要在`〜/ .local / share / applications`中创建`modelsim.desktop`文件，其中包含：

    [桌面入口]
	版本= 1.0
	Name = ModelSim
	Comment = ModelSim
	Exec = $ HOME / intelFPGA / 18.0 / modelsim_ase / bin / vsim
	Icon =应用程序 - 电子产品
	终点=真
	Type =应用程序
	类别=发展
##结论
在本教程之后，Quartus Prime和ModelSim可以正确安装在Linux机器上。可能会出现其他一些问题，但在互联网上很容易找到解决方案，特别是在下面的参考文献中。

##字体
Altera设计软件 -  Arch Linux  -  https://wiki.archlinux.org/index.php/Altera_Design_Software

Quartus Linux指南 -  Edison Cristovao  -  https://github.com/EdisonCristovao/quartus-linux-guide

对于通过JTAG的FPGA编程的USB配置 -  IFSC  -  https://wiki.sj.ifsc.edu.br/wiki/index.php/Configura%C3%A7%C3%A3o_da_USB_para_programa%C3%A7%C3%A3o_do_FPGA_via_JTAG

的ModelSim 17.1（首发版）为（ARCH）的Linux  -  https://gist.github.com/dries007/36c31fb8b2d712dfb41c6709f16e6e66

从Linux下IDE总理精简版运行的ModelSim-Altera公司的Quartus  -  http://twoerner.blogspot.com/2017/10/running-modelsim-altera-from-quartus.html

如何在Ubuntu 16.04 LTS上安装Quartus和modelsim  -  https://www.youtube.com/watch?v=uXwCPoqjpiY



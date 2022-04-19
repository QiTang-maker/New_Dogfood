# New_Dogfood
Optimazation of Layered Model on File System Testing

本文是在基于原始的基于层次模型的文件系统检测Dogfood的优化和改进
原始的Dogfood模型的github网站：https://github.com/midwinter1993/dogfood
原始的Dogfood模型相关论文：Mohan J, Martinez A, Ponnapalli S, et al. Finding {Crash-Consistency} Bugs with Bounded {Black-Box} Crash Testing[C]//13th USENIX Symposium on Operating Systems Design and Implementation (OSDI 18). 2018: 33-50.

本仓库的使用方法：<br>
1、首先在原始的Dogfood的github网页上按照步骤下载相关的镜像文件并完成原始的Dogfood的安装；<br>
2、用本仓库中的.py文件和.h文件替换掉原始Dogfood中的对应文件；

实验复现：<br>
1、将本仓库中的test_workloads压缩包解压，然后将所有的测试工作集复制到虚拟机中的subjects（建议在里面新建一个文件夹存储测试工作集）；<br>
2、用本仓库的b3-template.h文件替换/home/icse20/dogfood中的对应文件；<br>
3、在/home/icse20/文件夹下使用指令./clean.sh清空之前的测试结果；<br>
4、使用cp subjects/your_test_cases/yy-*.cpp dogfood/    # your_test_cases是你新建的存储测试工作集的文件夹；<br>
5、cd crashmonkey；<br>
6、make；<br>
7、sudo python xfsMonkey.py -f /dev/vda -d /dev/cow_ram0 -t <fs> -e 102400 -u build/tests/dogfood/ > outfile    # <fs> = btrfs || f2fs || ext4<br>
8、最后通过./diff_count.py得到测试结果。

实验扩展：<br>
1、在https://hub.docker.com/r/midwinter/dogfood 下载v3版本的镜像文件；<br>
2、运行下载的镜像：sudo docker run -it --rm --device /dev/kvm midwinter/dogfood:v3;<br>
3、用本仓库的所有.py替换掉位于/home/dogfood/py-code/中的对应文件；<br>
4、运行python3 ./b3Food.py生成新的测试工作集；<br>
5、将新生成的测试工作集导入刀CrashMonkey所在的虚拟机中，参考“实验复现”部分，可以实现对更多的测试工作集的测试。
  

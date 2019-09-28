* 对于下载```jre```与```jdk```，这两个我都下了，都在```Program File(x86)/Java```文件夹下
* 在命令行下编译```.java```文件
  * 加入环境变量的时候，要将两个```bin```文件上移到顶部才可以（顺带着也解决了```javac```无法启用）
* 命令行下编程
  * ```java错误: 编码 GBK 的不可映射字符 (0x9C)```
    * 输入```javac -encoding UTF-8 Welcome.java```

1. 假设当前已经编译好CUDA版本的OpenCV，并且已经安装好CUDA toolkit，需要确认的一些关键信息有：
   - 假设编译好的OpenCV文件夹里有“build”（编译OpenCV的时候也可以不叫build，这个是编译的时候自己命名的）, build里面是“install”， install里面有“bin”、“etc”、“include”和“x64”
     - 注意"x64"里的`vc16\lib`存放着我们需要用到的dll文件，CUDA版本的OpenCV需要用到的dll叫做`opencv_world470d.lib`和`opencv_world470.lib`，470表示OpenCV版本为4.7， 结尾的d对应debug版本，不带d的是release版本。
   - CUDA toolkit 安装在C盘“C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/”目录下。
2. 此时， 如果我们用visual studio新建一个工程，并需要使用带CUDA的OpenCV和CUDA toolkit， 则这个项目需要进行如下配置：
   - 鼠标右键点击工程名字， 选择“属性”，此时弹出一个“xxx属性页”的窗口， 左上角为“配置（C）”，可以选择不同模式进行配置，通常就是`release`和`debug`两种模式
   - 选择好模式之后（如debug模式），选择`C/C++`，选择“附加包含目录”，点击这一行右侧的文字右边的“下箭头”可以看到一个“编辑”选项，点击编辑之后会弹出一个窗口， 这里`将编译好的OpenCV的include路径复制进来`
     - 需要包含两个路径：`xxxxxx\opencv\build\install\include\opencv2`和`xxxxxx\opencv\build\install\include`。如果只写了第一个路径，那么写代码的时候就需要把cv写成cv2, 为了避免麻烦，推荐把第二个路径也写上， 然后点击确定即可。
   - 配置好OpenCV头文件之后， 需要把`CUDA toolkit`和`OpenCV的dll`也配置一下。回到“xxx属性页”窗口这里， 点击“链接器”，选择`附加目录库`， 点击这一行右侧的文字右边的“下箭头”可以看到一个“编辑”选项, 这里填写：
     - `C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.7/lib/x64`
     - `C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.7/lib/x64/$(Configuration)`
     - `xxxxxx\opencv\build\install\x64\vc16\lib`

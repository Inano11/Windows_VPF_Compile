# Windows_VPF_Compile
Windows10 VideoProcssingFramework Compile Step. Use GPU for Camera Decode or Encode. (Win10使用Python做Nvidia GPU视频编解码保姆级编译步骤）

系统及环境变量：

- win10 专业版 2004（1809 LTSC测试成功）；操作系统版本：19041.508（17763.2686）

- driver ：RTX 3080Ti（511.65）

- Python：3.8.8

- cuda ：11.1.1_456.81；cudnn ：8.0.5.39

- torch ：1.9.0 + cu111；torchaudio ：0.9.0；torchvision ：0.10.0（https://pytorch.org/get-started/previous-versions/）

  

软件版本：

- cmake ：3.23.0 - rc2

- Visual Studio ：community 2019, 16.11.10；Windows 10 SDK（10.0.19041.0）

- Video Codec SDK ：Video_Codec_SDK_11.1.5

- FFmpeg ：ffmpeg-n4.4-latest-win64-lgpl-shared-4.4

  

下载步骤：

1. 下载 VideoProcessingFramework：

   [Github | VideoProcessingFramework](https://github.com/NVIDIA/VideoProcessingFramework)
   ![image-20220309110141324](https://user-images.githubusercontent.com/47096692/158345165-9b91175d-a916-4061-8a3a-8474fc4eab9e.png)


2. 下载FFmpeg （shared）：

   [Github | FFmpeg](https://github.com/BtbN/FFmpeg-Builds/releases)

   [Download | ffmpeg-n4.4-latest-win64-lgpl-shared-4.4](https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-n4.4-latest-win64-lgpl-shared-4.4.zip)

    ![image-20220309110141324-1646806327718](https://user-images.githubusercontent.com/47096692/158345461-30274a4b-9bf5-49fe-8338-f3304b8593de.png)
    ![image-20220309110224308](https://user-images.githubusercontent.com/47096692/158345312-fa6c6395-75ea-4d80-b08c-622eaeff01e9.png)


3. 下载Video Codec SDK

   [Page | Video Codec SDK](https://developer.nvidia.com/nvidia-video-codec-sdk) 

    ![image-20220309110349664](https://user-images.githubusercontent.com/47096692/158345573-87fc2293-8f8e-4a3a-99fa-d49b46e89f5b.png)


4. 下载Visual Studio 2019 Community：
    ![image-20220309111707313](https://user-images.githubusercontent.com/47096692/158345579-85007b72-aad6-471c-b9b0-e234f9c9a47a.png)


   - 勾选使用C++的桌面开发，安装windows 10 SDK（10.0.19041.0）

5. 下载cmake：

   [Page | CMake](https://cmake.org/download/)

   [Download | CMake](https://github.com/Kitware/CMake/releases/download/v3.23.0-rc2/cmake-3.23.0-rc2-windows-x86_64.msi)
    ![image-20220309143422810](https://user-images.githubusercontent.com/47096692/158345629-79f83e41-7cb4-4b46-8db5-963937c0d755.png)



安装步骤：

1. 安装Nvidia驱动，Python，以及匹配版本的CUDA，Visual Studio

2. 下载VideoProcessingFramework，FFmpeg，Video Codec SDK

3. 将步骤2中的文件，放到一个文件夹。如：

    ![image-20220309144339670](https://user-images.githubusercontent.com/47096692/158345650-e8fe3f5d-ffb6-4ed1-9e90-779e5e733bec.png)

4. 在VideoProcessingFramework文件夹中，新建build文件夹

    ![image-20220309145023618](https://user-images.githubusercontent.com/47096692/158345697-94e7637a-39d9-4ecf-b8c3-75e950ca8b82.png)

5. Win+R，打开cmd命令，cd到build文件夹，输入命令：

   ```python
   cmake .. ^
     -G"Visual Studio 16 2019" -A x64 ^
     -DFFMPEG_DIR:PATH="D:/VPFApp/ffmpeg" ^
     -DVIDEO_CODEC_SDK_DIR:PATH="D:/VPFApp/Video_Codec_SDK_11.1.5" ^
     -DGENERATE_PYTHON_BINDINGS:BOOL="1" ^
     -DGENERATE_PYTORCH_EXTENSION:BOOL="1" ^
     -DCMAKE_INSTALL_PREFIX:PATH="D:/VPFApp/VideoProcessingFramework"
       
   ```


   成功提示：

![image-20220309145338659](https://user-images.githubusercontent.com/47096692/158345737-637f4c20-57c8-4b4e-bd90-dad7afd45467.png)

6. 在build文件夹中，用vs2019打开ALL_BUILD.vcxproj

    ![image-20220309145511888](https://user-images.githubusercontent.com/47096692/158345749-1dab478a-1de9-4487-af9e-8888300cda32.png)

   

7. vs2019构建INSTALL（ps：此处因版本原因，极易报错。查看错误原因，尝试更换相应文件的版本）

    ![image-20220309145640525](https://user-images.githubusercontent.com/47096692/158345773-9c811289-677e-4ff1-a420-a42a7b7edb17.png)

8. vs2019构建成功界面：

![image-20220309145805848](https://user-images.githubusercontent.com/47096692/158345786-6db1785e-469d-417e-82da-cc087c487445.png)

9. 构建成功后，在VideoProcessingFramework文件夹以及bin目录中，会多出两个pyd文件：

    ![image-20220309145949986](https://user-images.githubusercontent.com/47096692/158345807-1d77d5b8-7f8d-400d-86b5-9b0cb451ff0f.png)

10. 将ffmpeg文件夹bin目录下的dll文件，两个pyd文件，拷贝至VideoProcessingFramework文件夹的bin目录下

    （ffmpeg\bin）：

    
    （VideoProcessingFramework\bin）：

    
11. Python运行任意Sample，预祝顺利！

    







​	

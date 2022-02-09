# raspberrypi-camera
## 인체인식
```
password
~$ sudo passwd root
New password: qkrtlgn@1225
```
## setting
```
~$ sudo raspi-config
Interfacing Options enter
Camera enter
yes enter
확인
~$ libcamera-hello
프로필 -> settings -> DEveloper settings -> New Github App -> raspberrypi
```

## OpenCV설치
```
1. 패키지 업데이트
sudo apt-get upgrade

2. 패키지 설치
sudo apt-get install build-essential cmake -y
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev -y
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libxvidcore-dev libx264-dev libxine2-dev -y
sudo apt-get install libv4l-dev v4l-utils -y
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev -y
sudo apt-get install libgtk2.0-dev -y
sudo apt-get install mesa-utils libgl1-mesa-dri libgtkgl2.0-dev libgtkglext1-dev -y
sudo apt-get install libatlas-base-dev gfortran libeigen3-dev -y
sudo apt-get install python2.7-dev python3-dev python-numpy python3-numpy -y

3. OpenCV 다운할 폴더 생성
mkdir opencv

4. 폴더 이동
cd opencv

5. 다운 및 압축해제
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.1.2.zip
unzip opencv.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.1.2.zip
unzip opencv_contrib.zip

6. 폴더 이동 및 컴파일
cd opencv-4.1.2

7.폴더 이동
mkdir build
cd build

8. OpenCV 컴파일 설정(주기억 장치 메모리 설정)100 -> 2048
sudo nano /etc/dphys-swapfile
sudo /etc/init.d/dphys-swapfile restart(오래걸릴시 Ctrl + C)

9. Build하기
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D ENABLE_NEON=ON \
    -D ENABLE_VFPV3=ON \
    -D WITH_OPENMP=ON \
    -D BUILD_TIFF=ON \
    -D WITH_FFMPEG=ON \
    -D WITH_TBB=ON \
    -D BUILD_TBB=ON \
    -D BUILD_TESTS=OFF \
    -D WITH_EIGEN=OFF \
    -D WITH_GSTREAMER=OFF \
    -D WITH_V4L=ON \
    -D WITH_LIBV4L=ON \
    -D WITH_VTK=OFF \
    -D OPENCV_EXTRA_EXE_LINKER_FLAGS=-latomic \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D BUILD_NEW_PYTHON_SUPPORT=ON \
    -D BUILD_opencv_python3=TRUE \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D BUILD_EXAMPLES=OFF ..

10. Opencv설치를 위한 의존성 설치
sudo apt-get install build-essential cmake git unzip pkg-config    
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev   
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev   
sudo apt-get install libgtk2.0-dev libcanberra-gtk*   
sudo apt-get install libxvidcore-dev libx264-dev libgtk-3-dev   
sudo apt-get install python3-dev python3-numpy   
sudo apt-get install libtbb2 libtbb-dev libdc1394-22-dev   
sudo apt-get install libv4l-dev v4l-utils   
sudo apt-get install libjasper-dev libopenblas-dev libatlas-base-dev   
sudo apt-get install libblas-dev liblapack-dev gfortran   
sudo apt-get install gcc-arm*   
sudo apt-get install protobuf-compiler   
sudo apt-get install python-dev python-numpy

11. OpenCV 설치
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.1.2.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.1.2.zip
unzip opencv.zip
unzip opencv_contrib.zip

12. 컴파일
make -j4

13. 설치
sudo make install
되지 않을때 = pip3 install opencv-python

14. openCV라이브러리를 찾을 수 있도록 설정
sudo ldconfig

15. 메모리 설정 되돌리기 
sudo nano /etc/dphys-swapfile restart

16. OpenCV는 Haar Feature를 설치를 

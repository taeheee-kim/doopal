# Remote camera control system

*by JunHwan Kim, TaeHyeong Kim, Taehee Kim*

## Installation

#### [CVZONE]

https://github.com/cvzone/cvzone 링크를 참고하였습니다. cvzone 설치를 위해 선행되어야 되는 opencv와 mediapipe library를 각각 링크에 접속해 설치하였고, 이후 명령어를 이용해 cvzone을 설치하였습니다.

- `opencv 4.8.0` 설치

  https://jetson-docs.com/libraries/opencv/l4t32.7.1/py3.6.9 
- `mediapipe library 0.8.5_cuda102` 버전으로 설치

   https://jetson-docs.com/libraries/mediapipe/l4t32.7.1/py3.6.9 

- cvzone 설치

```
$ sudo pip install cvzone
```


---
#### [Torch,  Torchvision]

https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048 에서 Torch와 Torchvision을 설치하였습니다.

- `Pytorch v1.10.0` 설치

- 페이지 밑의 카테고리에서 instruction -> installation -> `torchvision v0.11.1`으로 설치


```
$ sudo apt-get install libjpeg-dev zlib1g-dev libpython3-dev libopenblas-dev libavcodec-dev libavformat-dev libswscale-dev
$ git clone --branch <version> https://github.com/pytorch/vision torchvision   # see below for version of torchvision to download
$ cd torchvision
$ export BUILD_VERSION=0.x.0  # 여기에 TorchVision 버전 0.11.1 넣어주기
$ python3 setup.py install --user
$ cd ../  # attempting to load torchvision from build dir will result in import error
$ pip install 'pillow<7' # always needed for Python 2.7, not needed torchvision v0.5.0+ with Python 3.6
```


---
#### [TSM]

https://github.com/mit-han-lab/temporal-shift-module/tree/master/online_demo  의 online demo/README.md를 따라 수행하였습니다.

-  cv2가 4.x 버전이여야 합니다. 다음을 통해 버전을 확인하세요.

```
 $ Python3
 >> Import cv2
 >> cv2.__version__
```

-  cv2를 import할 수 있도록 환경변수를 설정합니다.

```
export PYTHONPATH=/usr/local/python
```

-  다음 사이트에서 PyTorch와 torchvision을 설치합니다. 

https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048

(위의 torch 1.10.0 , torchvision 0.11.1 설치 그대로 수행했으면 넘기시면 됩니다.)

- 다음 명령어로 TVM을 빌드합니다.

```
$ sudo apt install llvm # install llvm which is required by tvm
$ git clone -b v0.6 https://github.com/apache/incubator-tvm.git
$ cd incubator-tvm
$ git submodule update --init
$ mkdir build
$ cp cmake/config.cmake build/
$ cd build

#[
#edit config.cmake to change
# 32 line: USE_CUDA OFF -> USE_CUDA ON
#104 line: USE_LLVM OFF -> USE_LLVM ON
#]

$ cmake ..
$ make -j4
$ cd ..
$ cd python; sudo python3 setup.py install; cd ..
$ cd topi/python; sudo python3 setup.py install; cd ../..
```



- ONNX를 설치합니다.

```
# install onnx

$ sudo apt-get install protobuf-compiler libprotoc-dev
$ pip3 install onnx

##ONNX-Simplifier는 호환되지 않아 설치하지 않았습니다.
```



-  cuda toolkit를 해당 경로로 export합니다.


```
export PATH=$PATH:/usr/local/cuda/bin
```

---
#### [ESPCN]

project.zip 안에 필요한 파일은 모두 들어있고 특별히 설치할 것은 없습니다.

혹시 실행이 되지 않는다면,
https://github.com/Lornatang/ESPCN-PyTorch 를 참고하시길 바랍니다..

---
추가로 많은 라이브러리와 환경 충돌로 업그레이드나 다운그레이드 시킨 것이 많습니다. 아래의 pip list를 참고하시기 바랍니다!


```
qwer@qwer-desktop:~$ pip list
Package                       Version
----------------------------- -------------------
absl-py                       1.4.0
appdirs                       1.4.4
apt-clone                     0.2.1
apturl                        0.5.2
arrow                         1.2.3
asn1crypto                    0.24.0
attrs                         21.2.0
beautifulsoup4                4.6.0
blinker                       1.4
Brlapi                        0.6.6
certifi                       2018.1.18
chardet                       3.0.4
cryptography                  2.1.4
cupshelpers                   1.0
cvzone                        1.6.1
cycler                        0.10.0
Cython                        3.0.10
dataclasses                   0.8
decorator                     4.1.2
defer                         1.0.6
distro                        1.9.0
distro-info                   0.18ubuntu0.18.04.1
docopt                        0.6.2
feedparser                    5.2.1
filelock                      3.4.1
flatbuffers                   24.3.25
future                        0.18.2
gast                          0.4.0
gdown                         4.7.3
graphsurgeon                  0.4.5
h5py                          2.7.1
html5lib                      0.999999999
httplib2                      0.9.2
idna                          2.6
importlib-metadata            4.8.3
importlib-resources           5.4.0
inform                        1.30
Jetson.GPIO                   2.0.17
Keras-Applications            1.0.8
Keras-Preprocessing           1.1.2
keyring                       10.6.0
keyrings.alt                  3.0
language-selector             0.1
launchpadlib                  1.10.6
lazr.restfulclient            0.13.5
lazr.uri                      1.0.3
louis                         3.5.0
lxml                          4.2.1
macaroonbakery                1.1.3
Mako                          1.0.7
MarkupSafe                    1.0
matplotlib                    2.1.1
mediapipe                     0.8.5-cuda102
mock                          3.0.5
numpy                         1.19.4
oauth                         1.0.1
oauthlib                      2.0.6
onboard                       1.4.1
onnx                          1.14.1
onnxruntime                   1.10.0
opencv-contrib-python         4.6.0.66
opencv-python                 4.10.0.82
packaging                     21.3
PAM                           0.4.2
pandas                        0.22.0
pbr                           6.0.0
Pillow                        8.4.0
pip                           21.3.1
pkgconfig                     1.5.5
platformdirs                  4.2.2
protobuf                      4.21.0
psutil                        5.9.8
pybind11                      2.12.0
pycairo                       1.16.2
pycrypto                      2.6.1
pycuda                        2019.1.2
pycups                        1.9.73
PyGObject                     3.26.1
PyICU                         1.9.8
PyJWT                         1.5.3
pymacaroons                   0.13.0
PyNaCl                        1.1.2
pyparsing                     2.2.0
pyRFC3339                     1.0
PySocks                       1.7.1
python-apt                    1.6.6
python-dateutil               2.9.0.post0
python-debian                 0.1.32
pytools                       2024.1.5
pytz                          2018.3
pyxattr                       0.6.0
pyxdg                         0.25
PyYAML                        3.12
quantiphy                     2.20
requests                      2.18.4
requests-unixsocket           0.1.5
scikit-build                  0.16.7
scipy                         0.19.1
SecretStorage                 2.3.1
setuptools                    49.6.0
simplejson                    3.13.2
six                           1.11.0
ssh-import-id                 5.7
system-service                0.3
systemd-python                234
tensorrt                      8.2.1.8
testresources                 2.0.1
topi                          0.6.0
torch                         1.10.0
torchvision                   0.11.0a0+fa347eb
tqdm                          4.64.1
tvm                           0.6.0
typing                        3.7.4.3
typing_extensions             4.1.1
ubuntu-drivers-common         0.0.0
uff                           0.6.9
unity-scope-calculator        0.1
unity-scope-chromiumbookmarks 0.1
unity-scope-colourlovers      0.1
unity-scope-devhelp           0.1
unity-scope-firefoxbookmarks  0.1
unity-scope-manpages          0.1
unity-scope-openclipart       0.1
unity-scope-texdoc            0.1
unity-scope-tomboy            0.1
unity-scope-virtualbox        0.1
unity-scope-yelp              0.1
unity-scope-zotero            0.1
urllib3                       1.22
urwid                         2.0.1
wadllib                       1.3.2
webencodings                  0.5
wheel                         0.37.1
xkit                          0.0.0
youtube_dl                    2018.3.14
zipp                          3.6.0
zope.interface                4.3.2
```

## Usage

```
# project.zip 다운 후 해당 폴더에서 터미널 창 실행

$ cd project/temporal-shift-module/online_demo
$ python3 final2.py
```

카메라가 켜진 뒤에는 다음 내용을 확인하실 수 있습니다.

1. 세 개의 손가락이 펼쳐지고 3초 유지된 손을 master hand로 인식하여 빨간 박스가 생기는 것
2. (master hand 있을 때) 엄지와 검지를 이용해 확대하는 모션을 취하면 화면이 확대되어 보이는 것
3. (master hand 있을 때) 손바닥을 펼친채 유지하는 Stop Sign 모션을 취하면 화면이 처음 상태로 reset 되는 것


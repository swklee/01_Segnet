# Introduction
* SegNet은 supervised learning을 기반으로 픽셀단위로 클래스를 나누는 방법이며, SegNet을 실험하는 방법에 대해 설명합니다. 
* 공유하는 SegNet code는 Caffe기반으로 구현되어 있으므로, Caffe 및 Python 2.7를 설치해주세요. 
* 다음의 링크에서 원본 코드 다운로드 및 실습이 가능합니다. 
   * 원본 코드: [SegNet Repository](https://github.com/alexgkendall/caffe-segnet)
   * 실습: [SegNet Tutorial](http://mi.eng.cam.ac.uk/projects/segnet/tutorial.html)

# Training & Testing
* SegNet을 실제 데이터를 이용하여 어떻게 Training 하고, Test하는지 알아보겠습니다. 
* Chagall에서 SegNet을 실습하기위한 위치는 다음과 같습니다.
  * [Chagall:/home/nhnent/H1/users/swook/SegNet
*  SegNet 하위 폴더의 구성은 아래 그림과 같습니다. 
    *  ![스크린샷 2017-04-17 오후 12.37.34]
    *  cafff-segnet-cudnn5: caffe로 segnet이 구현된 코드 
    *  camVid: Cambridge에서 제작한 Segmentation을 위한 DB, Truth map 포함
    *  FCdb: Face DB
    *  Fdb: Fashion DB
    *  Sdb: Simple Object DB (Truth map 포함)
    *  Models: SegNet에는 SegNet, SegNet-Basic, SegNet-Bayesian 등 다양한 모델이 존재. 각 모델별로 Training 및 Test할때 필요한 파일들이 저장되어 있음. 
    *  Scripts: SegNet을 실행하기 위한 복수의 파일이 저장되어 있음
    *  exe_test2.sh: Test하기 위한 Script
## Training
* Training을 위해서는 다음의 파일이 필요합니다.
    * 1. *model_solver*.prototxt
    * 2. *model_train*.prototxt
    * 3. *train_list*.txt
* *model_solver*.prototxt
    * SegNet train parameter 세팅 파일
    * *model_solver*.prototxt 의 첫번째 라인에서 *model_train*.prototxt 파일을 Call하므로 파일 위치에 주의하세요.
    * 실례: ```net: "/home/nhnent/H1/users/swook/SegNet/Models/bayesian_segnet_train.prototxt" ``` 
* *model_train*.prototxt
    * *model_train*.prototxtd 의 여덟번째 라인에서 *train_list*.txt 파일을 Call하므로 위치에 주의하세요.
    * 실례: ```source: "/home/nhnent/H1/users/swook/SegNet/Sdb/train.txt"```
* *train_list*.txt
    * Training을 위한 영상의 위치를 알려주는 파일
    * /path0/image.png /path1/gtm.png
    * 실례: ```/home/nhnent/H1/users/swook/SegNet/Sdb/train/org0_0.png /home/nhnent/H1/users/swook/SegNet/Sdb/trainannot/gtm0_0.png```

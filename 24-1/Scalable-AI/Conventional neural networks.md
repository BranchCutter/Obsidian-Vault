> MLP, CNN, 트랜스포머 등이 있음

> 간단하게 작동 원리만 보고 파라미터숫자 계산하는 방법 등 어떻게 우리가 모델이 efficient하다고 평가하는지 그 기준을 봄

## Neural -> Artificial Neural

![](https://i.imgur.com/H5nOcAQ.png)

## MLP
Deep neural network

![](https://i.imgur.com/Ij7BjCK.png)

## MLP's computation

* Shape of Tensors :
	* Input Features $X$ : $(n,\ c_i)$
	* Output Features $Y$ : $(n,\ c_o)$
	* Weights $W$ : $(c_o,\ c_i)$
	* Bias $b$ : $(c_o,\ )$
![300](https://i.imgur.com/9ONaC6e.png)

![](https://i.imgur.com/HyiWgzr.png)

Total # parameters = 5*3 + 3*2 = 21 

---
## CNN's computation
![](https://i.imgur.com/aJROsLr.png)

![](https://i.imgur.com/ONGvl1q.png)

![](https://i.imgur.com/jLsoRFe.png)

![](https://i.imgur.com/66PMnUm.png)

![](https://i.imgur.com/u0C7W61.png)

![](https://i.imgur.com/v4OspdP.png)

## 2D-CNN's computation

![](https://i.imgur.com/jMvb0Kx.png)

![](https://i.imgur.com/RFs1ROQ.png)

![](https://i.imgur.com/8A2kr4f.png)

![](https://i.imgur.com/8giBSMx.png)

![](https://i.imgur.com/gttbR2e.png)

![](https://i.imgur.com/rjNC6xj.png)

---
## Padding

![](https://i.imgur.com/8CR3NI8.png)

---
## Stride
* CNN은 같은 필터를 연속적으로 사용
* 근데 사실 한 픽셀 옆이 큰차이가 없는 경우가 많아서 여러칸씩 이동하면서 적용하는 방식을 취할 수 있음
* 그래서 여러칸씩 이동하면서 적용하는 방식을 취할 수 있음

---
## Pooling
* 피쳐맵 사이즈가 너무 크면 연산량이 계속 너무 많음
* Representitive한 값들만 뽑아서 다음 conv 연산에 들어가기 전에 map 사이즈를 줄임

---
## LeNet (1998)
* Yann LeCun :
	* CNN의 중간 layer에서 실제 뇌에서 나타나는 시각 feature 들을 찾을 수 있다고 강하게 주장하시는 분
* 당대 major는 hand-designed features (PCA, ICA)
	* 기존의 MLP로는 vision 문제를 잘 해결 못하는 단점이 있었음
	* 당시 컴퓨터 성능에 비해 파라미터 수는 너무 많기도 했음
* 뇌의 시각 시스템을 차용, CNN의 개념을 처음으로 사용 ![](https://i.imgur.com/gnXdYvv.png)
* LeNet-5에서는 MLP를 다는게 더 성능이 좋음을 확인
	* 이때 까지만 해도 average pooling을 사용, 구조는 요즘/현대적 CNN
![](https://i.imgur.com/yZ3wnwc.png)
![](https://i.imgur.com/uCC7NhJ.png)

---
## AlexNet (2012)
* 당시 GPU VRAM 때문에 더 깊게 크게 만들 수 없었음
* 이걸 해결하기 위해서 개발 GPU 2대를 사용하는 방법
* 그 사이에 Image augmentation 방법 개발, ReLU 개발
	* 적극적으로 활용하여 ImageNet Competition에서 당대 최고
* 유명한 모델 중에는 처음으로 ReLU 사용
![](https://i.imgur.com/4lzKMzV.png)
-> 채널이 너무 많음

* Feature를 그냥 반으로 나눠서 각각 다른 GPU에서 연산하도록 구성
	![](https://i.imgur.com/h29EGHn.png)
	-> 요즘엔 batch normalization으로 인해 잘 안 쓰임

---
## Grouped convolution
![](https://i.imgur.com/MQ2ZY4I.png)
![400](https://i.imgur.com/FUVQplI.png)

---
## VGG(2014)
* University of Oxford, Visual Geometry Group 
	* https://www.robots.ox.ac.uk/~vgg/

* 더 깊게 쌓으려는 첫 시도 (16 layers, 19 layers)
	* AlexNet 은 kernel (channel) 개수가 많이 늘어난거지 깊게 쌓은건 아님.
	* Gradient vanishing 문제가 있어서 잘 안될거라는 생각이 있었지만 ResNet 같은 새로운 시도를 하기 이전까지 conventional 한 모델 중 최고.
![](https://i.imgur.com/GEGQvxM.png)

![300](https://i.imgur.com/fttwFzx.png)
-> 3x3 conv를 연속적으로 쓴다

* 3x3으로 작은 커널을 사용하면서 깊게 쌓음.
	* 기존에는 큰 커널 11x11, 5x5, 7x7 같은걸 썼었음.
	* 여기서는 3x3을 쓰는 대신에 여러 번 적용해서 local feature 는 물론 global feature 까지 학습할 수 있다 고 제시.
	* 7x7 필터 1개면 49개의 매개변수, 그러나 3x3 을 3 층으로 쌓으면 27개 로 더 간단.
	* 또한 활성화 함수를 층 수만큼 지나면서 더 많은 non-linearity 를 만들어 줄 수 있음
	* 참고: 보통 커널사이즈는 홀수로만 한다. 왜?

---
## GoogLeNet (Inception-v1) (2014)
* Inception module 제안  
	* 기존의 network in network 라는 논문 (Min, 2013) 의 발전 형태
	* 요약하면 1x1 convolution 을 사용하는 것이 도움이 된다~  
	* 나중에 Inception-v3 등의 모델로 발전되는 것의 원본이 되는 아이디어 
	* 최근까지도 ResNet 처럼 backbone 모델로 자주 쓰이는 편.  
	* 그 외에도 Auxiliary classifier를 통한 vanishing gradient 해결

![](https://i.imgur.com/nmSug6u.png)
![150](https://i.imgur.com/1QVKcYx.png)
### Inception module
* 핵심 아이디어:  
	* CNN은 feature를 추출하는거고 사실 classification 에 필요한 non-linearity 는
	  fully connected layers (MLP) + activation function 에서 온다.  
	* 근데 CNN을 그냥 naïve 하게 쓰면 flatten 했을때 차원이 너무 크다

* 문제는 CNN에서 차원을 어떻게 줄일 것 인지.
![](https://i.imgur.com/vsi9T7k.png)


#### CCCP and GAP
* CCCP (cascaded cross channel parametric pooling )
	* 각 feature map 에서 수행되는 기존 pool 과 달리 
	  feature map 몇 개에 걸쳐서 pooling 함.
* GAP  
	* 이건 당연하게도 각 feature map 에 대해서 하되, 하나로 줄이는 방법.

### Inception module
* Network in network (NIN; 기존 논문): 
	* 마지막에 fc (mlp) 레이어를 달아줌으로써
	  원래 non-linearity 를 해결하는데 있어서 큰 도움이 되었음
	* 단순하게 conv 는 linear 연산임 
	  (선형대수학에서 이야기하는 linear transformation 수식으로 보면 똑같음)
	* 그래서 마지막에 fc (mlp) 레이어 다는 것 대신 두가지를 제안함 
		* global average pool (GAP) WIN!  
		* cascaded cross channel parametric pooling (CCCP)
	* Inception 도 동일하게 이런 문제를 해결하고 싶은데 CCCP를 계승

### 1x1 conv
* Filter 가 1x1인 것을 의미하며, CCCP 의 한 종류 
  (전체 channel 대한 pooling)
![](https://i.imgur.com/7HxNp8b.png)

### Auxiliary classifier (참고)
* Gradient vanishing 문제를 해결하기 위해서 맨 마지막 layer 에서 class 를 알아맞히는 형태가 아니라 중간 중간에 class 맞히도록.

* 요즘 잘 안씀. 왜?
	* ResNet 이 개발되었으니까 도 있지만
	* 초반 layer 에서 classification 을 하도록 학습하니까 
	  후반 layer 에서 optimal 한 feature 가 잘 안뽑히더라
![400](https://i.imgur.com/tb1lsZu.png)

multi modal이나 백본 모델에 가끔 사용

---
## Inception-v3 (2015)
* Inception-v2 는 아래와 같이 개선 
  (https://velog.io/@woojinn8/CNN-Networks-3.-GoogLeNet)
	* 입력 이미지의 해상도가 224x224에서 299x299로 증가  
	* 제일 앞의 7x7 Conv layer를 3개의 3x3 Conv layer로 분해한 multi-layer로 구조개선  
	* Inception module도 factorizing convolution된 형태로 치환하여 더 깊되 연산량은 적도록 개선 § Inception module이 2종류에서 3종류로 늘어남  
	* Auxiliary classifier 앞부분 제거 (효과 미미)  
	* 최종 단에 feature-map의 개수가 더 많아짐  
	* Convolution과 Pooling의 stride를 2로 변경  
	* 22-layer에서 42-layer로 깊어지고, 연산량이 2.5배 증가
* Inception-v3 는 SGD -> RMSProp, Batch normalization 적용 
	* 그 외에는 label smoothing 을 적용.
---
## Factorizing convolution
* VGG에서 배운 개념:  
	* 3x3을 여러 번 쓰면 5x5 한 번 쓰는 것과 수학적으로 동일하되
	  연산량은 더 적다는 뜻.  
	* 그래서 inception 모듈의 5x5 를 3x3 두개로 교체
![200](https://i.imgur.com/wo5Kf23.png)
![450](https://i.imgur.com/U0uLwT5.png)

* 이걸 한번 더 한다: 3x3을 1x3과 3x1의 두개로 분해. 
	* 수학적으로 3x3 쓰는 것과 동일하고  
	* 연산량도 3x3 =9 -> 3+3=6 으로 절감.
![200](https://i.imgur.com/xzICZRd.png)
![300](https://i.imgur.com/wPa4ebd.png)

---

## ResNet and DensNet (2017) (참고)
* Vanishing gradient  
	* CNN 의 경우 레이어를 여러 번 쌓아야 local feature 도 뽑고 – global
	  feature 도 뽑을 수 있는데
	* 레이어가 너무 깊어지면 gradient (0~1사이) 가 연속적으로 곱해져서 0 에 가까워지고, weigh가 업데이트가 더 이상 안되는 문제가 생김.
![](https://i.imgur.com/yTXaKuM.png)

- 병목 블록 (bottleneck block)  
	- Skip connection 과 동일하게 생겼지만 앞뒤로 1x1 conv 를 넣어서 연산량을 
	  많이 가져가지는 않으면서  
	- 앞에서 차원을 확 늘렸다가 뒤에서 차원을 줄이는 일종의 병목을 만듦.
![](https://i.imgur.com/YAxP0aK.png)

* Resnet 의 약간 변형형태.  
	* 한 줄이 아니라 더 Dense 하게 연결한다. 
	* 덧셈이 아니라 concatenation 으로 한다.
		![300](https://i.imgur.com/Pgk0fsH.png)
![](https://i.imgur.com/ZXurryD.png)
![400](https://i.imgur.com/c7f2SoC.png)

* 덧셈으로 묶어놨기 때문에 gradient 가 균일하게 넘어감.
* hidden smoother convex function 을 얻을 수 있음.
	* 원래는 optimal depth 가 각각 데이터 마다 달라서 굉장히 날카로운 형태.
	* optimal depth 부터 최종 output layer 까지 shortcut 으로 연결되어 진짜 optimal 한 convex loss function.

---
## MobileNet (2017)
* Depthwise separable convolution 아이디어 제시
	* 보통 CNN 이면 레이어가 증가할수록 채널이 늘어나는데
	* 모든 채널에 대해서 convolution 하는게,  즉 필터를 곱해서 모두 더 하는게 의미 없을 수 있다는 생각에서 Depthwise convolution + Pointwise convolution 으로 나누어서 진행.

	* 이는 Xception (2017)의 핵심 아이디어이기도 함.

- Depthwise separable convolution 아이디어 제시  
	- Channel 별로 한다는 의미로 channel wise convolution 이라고도...
![](https://i.imgur.com/UIvbMA1.png)
-> 이 Channel의 갯수가 n개 있는데 chanel 개개로 convolution

---
## Depthwise convolusion
![](https://i.imgur.com/UkfXd15.png)

---
# Short summary for CNN
* 3x3 convolution is enough  
	* But many of them (from VGG)
* May split into groups  
	* So that you can train a CNN with huge #channels (from AlexNet)
* Reduce feature map size drastically to get advantage advantage of MLP’s nonlinearity
	* 1x1 Convolution (from Inception)  
	* O r even factorize it (from inception-v3)  
	* Or even do it in depthwise manner (from mobileNet)

---
## Efficiency metric

![](https://i.imgur.com/j0YA8Mr.png)

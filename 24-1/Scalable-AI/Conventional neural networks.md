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


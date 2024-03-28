## Field that uses this?
* Natural language, Computer vision, Multimodal, etc
	* Recent popular models all consider this since hey are huge

## Distributed / Efficient / Scalable model in CV
![](https://i.imgur.com/txZMDWK.png)

![](https://i.imgur.com/VfjMgBG.png)

![](https://i.imgur.com/eOkVgJI.png)

* Edge computing
	![400](https://i.imgur.com/k9DAP3K.png)

	* MobileViT
		![](https://i.imgur.com/vpG9U6K.png)
		-> 트랜스포머 계열의 하드웨어 최적화 이슈가 있으나, 좋음
	* Apple's research team
		![](https://i.imgur.com/pxKeIlA.png)

## On-device learning

![](https://i.imgur.com/YXdzuXS.png)

일반적으로 프라이버시 이슈가 많음
real-time으로 진행

## Generative model
> Diffusion models create realistic images from a natural language description

![](https://i.imgur.com/odIaT5D.png)

![](https://i.imgur.com/1RB4vxs.png)
-> 큰 틀에서 바뀌는 것은 아니지만, context는 바뀜

![](https://i.imgur.com/CPAcInE.png)

## Autonomous driving

![](https://i.imgur.com/v9iosZs.png)
-> LiDAR Realtime Process model

## Large Language Model to be small
> Lite Transformer reduces the model size with pruning and quantization

![](https://i.imgur.com/54KzaJl.png)
-> 데이터가 제일 중요
-> quantization을 많이 진행함

---
## Zero/few-shot learning of LLMs

### Zero-shot
```
The model predicts the answer given only a natural language description of the task.
No gradient updates are performed.
```
![400](https://i.imgur.com/lUfabBF.png)

### Few-shot
```
In addition to the task description, the model sees a few examples of the task.
No gradient updates are performed.
```
![400](https://i.imgur.com/7jzgWfr.png)

> The larger model is, the more it benefits from one/few shot

![](https://i.imgur.com/lfr7O7a.png)

---
## Chain of thoughts

![](https://i.imgur.com/fD6CiW3.png)

> Also comes with the cost of model size

![](https://i.imgur.com/T3uFdfS.png)

-> 왜 수학연산이 잘 안되는가를 연구

---
## LLM is pain in the neck
![](https://i.imgur.com/eEAIZfU.png)

---
## Edge computing for LLMs

https://github.com/mit-han-lab/TinyChatEngine

---
## Multimodal

AlphaGo
![](https://i.imgur.com/ISsQhsz.png)
Compute: 1920 CPUs and 280GPUs ($3000 electric bill per game)

Robotics
> Robotics transformers control based on language instructions

![](https://i.imgur.com/Y41dobx.png)
Run at only 3Hz due to high computational cost and networking latency.

---
## Image-text
> LLaVA achieves general-purpose visual and language understanding
![](https://i.imgur.com/SAfEDrc.png)
> LLaVA uses a 13B LLaMA for language understanding.
### Image-text (quantized)
![](https://i.imgur.com/pPe5LOs.png)

---

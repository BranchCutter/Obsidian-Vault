# Introduction

> 본 과정은 분산 딥러닝과 확장 가능한 인공지능(Scalable AI)의 기초를 다루는 수업임. 분산 딥러닝 부분에서는 다중 스레딩(CPU 기반), 다중 GPU 활용, 고성능 컴퓨팅(HPC), 그리고 쿠버네티스(Kubernetes) 클러스터를 활용한 그리드 컴퓨팅을 탐구함. Scalable AI 부분에서는 파라미터 효율적인 파인 튜닝, 엣지 컴퓨팅, 그리고 양자화 기술을 학습함. 이 과정을 통해 학생들은 대규모 인공지능 모델을 효율적으로 훈련시키고, 배포하는 데 필요한 기술적 지식과 실용적 경험을 얻게 될 것임.

---

```
분산 딥러닝과 Scalable AI 소개

* Introduction to deep learning & machine learning
  * Parallel/distributed optimization algoritms(gradient descent)
  * Also Policy gradient algorithms in reinforcement learning

* Familarityto Transformer architectures
* Pytorch-based coding methods

-------------------------------------------------------------------------------
* Basic concepts of distributed deep learning
  * Old (conventional) ideas of distributed deep learning

* Advanced concepts of distributed deep learning
  * PEFT (Parameter efficient fine-tunung) 방법
    * LoRA
  * Quantization (양자화)
    * Cast the weights into integers not float32
  * Deployment / Edge computing (부수적인 것)

-------------------------------------------------------------------------------
What we'll cover

* How to optimize Multi-GPU set-up
  * Monitoring usage of Multi-GPUs & memory leakages etc.

* How to use HPCs
  * HPC는 없지만 사용하는 방법 정도는 배울 수도 있음
  * Slurm 기반으로 한 번 구축하는 방법과 함께 사용하는 방법
```

---
Stable 한 AI Observation
Macro-scale, *hierarchical* action
Primitive, *flat* action
Dynamic NeuralNetwork

---
프로젝트
* 기껏 efficient 하게 쓰는 법 / distributed 하는 법
  배웠는데 안 써보면 아쉬우니까
* 기존의 large-scale 모델을 분산처리 혹은 양자화 / PEFT 등을 통해 VRAM/RAM 8기가 미만으로 만들어 돌려보기
* 그걸 통해서 fine tuning까지 할 수 있다면 좋음

이론 위주의 수업을 진행하게 될 것임

---
## 본격적인 소개

분산 딥러닝, Scalable AI가 뭔가?
> 

Efficient Model은 뭔가?


---
## The Gap between Supply and demand

2017년대부터 2022년까지 GPU memory 자체의 스펙 상승은 많이 진행되지는 않았지만,
Model Size 자체는 많이 증가하였다.

---
## Industry & academia

Industry에서는 API call을 더 많이 쓰는 경향이 있음

개인 서버를 구현하는 것 자체가 인력 & 비용이 많이 듬

---
## Model compression / make it efficient

make it scalable / train in destributed settings

Pruning, sparsity, quantization, etc

---
## Optimal Brain Damage(LeCun et al., 1989)

---
## Field that uses this?

* Natural language, Computer vision, Multimodal, ...
	* Recent popular models all containers all done


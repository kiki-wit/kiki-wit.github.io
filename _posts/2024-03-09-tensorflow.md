---
date: '2024-03-09 12:01:00'
layout: post
title: 텐서플로우
subtitle: '텐서플로우를 통한 추천시스템 만들기'
description: >-
  텐서플로우로 시계열을 사용하여 예측 프로그램 구축.
permalink: /ml/tensorflow/
category: ml
tags:
  - 머신러닝
  - tensorflow
author: kiki
paginate: true
---

인공신경망(A.I)은 인간의 뇌를 본따서 모델을 만들었는데 뇌 안에서 신호를 전달하는 역할을 담당하는 것이 시냅시스(그림의 원형)이다. 이것을 <a href="#">Neural</a> 또는 <a href="#">Node</a>라고 부른다.

뉴런은 각각이 가중치를 가지고 있는데 가중치를 점차 줄여나가 *output layer(결과값)*를 도출한다.
위 사진과 같은 시냅시스는 <a href="#">4층짜리 레이어</a>이며 **1층은 input layer** , **4층은 output layer** 이다.

2층부터는 앞에서 데이터를 받고 있는 것을 알 수 있는데 1층 input layer 는 어떤 형식으로 데이터가 들어오는지 모르기 때문에 반드시 **input shape**를 지정해주어야 한다. **input shape** 는 데이터가 어떤 모양으로 들어오는지 정의한다.

> **Neuron (Node)** 내부는 **W (weight) * X (입력값)** 으로 이루어져 있다고 생각하시면 됩니다. (층마다 + bias도 붙습니다.)
> Dense Layer는 노드가 완전하게 연결되어 있다고 해서 **Fully Connected Layer**라고도 불리웁니다.
논문에서는 Fully Connected Layer 혹은 FC로 줄여서 많이 불리우니 이 점 꼭 참고해 주세요.
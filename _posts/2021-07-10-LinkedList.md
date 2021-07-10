---
layout: single
title:  "[Data Structure] Linked List"
categories: 
  - DataStructure
tags: 
  - [Computer Science, Data Structure, Linked List]
toc: true
toc_sticky: true
date: 2021-07-10
last_modified_at: 2021-07-10
---

### 🌲 개념

![LinkedList_1](https://user-images.githubusercontent.com/73654909/125159518-de9a1400-e1b2-11eb-9f97-2c14f399554a.jpg){: width="40%" heght="40%" .align-center}

컴퓨터의 자료를 저장하는 구조의 한 종류, 일렬로 연결된 데이터를 저장할때 사용하고 다음 데이터의 주소를 가지고 있다.

##### 🍁 삽입

![LinkedList_2](https://user-images.githubusercontent.com/73654909/125159515-dd68e700-e1b2-11eb-901e-95ed1173c9ab.jpg){: width="40%" heght="40%" .align-center}

Linked List에 데이터를 중간에 삽입하고 싶으면 앞에 노드가 가지고 있던 Next Address를 추가한 노드의 Next Address로 바꾸고,  앞 노드는 추가한 노드로 Next Address를 변경한다. 

##### 🍁 삭제

![LinkedList_3](https://user-images.githubusercontent.com/73654909/125159517-de9a1400-e1b2-11eb-86bc-3820944f7551.jpg){: width="40%" heght="40%" .align-center}

데이터를 삭제하고싶을때는 삭제대상이 가졌던 다음주소의 노드를 앞에 노드에 주면 된다. 이렇게 되면 `Linked List`에서는 삭제되었지만, 메모리에는 아직 존재하는데 `Java`에서는 `GC;Garbage Collection`가 처리해주지만 `C,C++`는 반드시 사용안하겠다고 명시를 해야한다.

#### 🌲 배열(Array)과 다른점

**배열**은 방들이 물리적으로 한곳에 몰려있다. 예를들면 20층짜리 아파트 한동에 1호, 2호, 3호, ..., 19호, 20호 처럼 모여있고 <u>크기를 한번 정하면 늘이거나 줄이는것이 많이 번거롭다.</u>

반면에 **Linked List**는 아파트 여러동을 거친다. 1동에 1호, 5동에 3호, 2동에 2호, ... 와 같다. 그래서 `Linked List`는 <u>배열보다는 속도가 느리지만 추가, 삭제는 주소값만 바꿔주면되어 편리하다.</u>이러한 특성으로 <u>길이가 정해지지 않은 데이터를 핸들링할때는 `Linked List`를 사용하는게 좋다.</u> 
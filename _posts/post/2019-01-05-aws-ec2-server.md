---
layout: post
title: "AWS EC2 Server 시작"
date: 2019-01-05
excerpt: "AWS EC2 Server 구동하기"
tags: [AWS, EC2, Linux]
comments: false
---

AWS 클라우드 서비스를 통해 데이터를 지속해서 유지 가능한 서버를 개설한다.  
본 글에 포함된 모든 이미지는 클릭해 확대 확인할 수 있다.

### AWS EC2 환경 구성 (Windows & MAC)

#### EC2 인스턴스 가상 서버 시작하기 (Windows, MAC 동일)

<figure class="half">
	<a href="{{site.url}}/assets/img/post/ec2_server/main.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/main.JPG"></a>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_1.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_1.JPG"></a>
	<figcaption>EC2 서비스 시작</figcaption>
</figure>

모든 서비스 - 컴퓨팅 - EC2로 이동한다.

#### 인스턴스 환경 설정 과정

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_2.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_2.JPG"></a>
</figure>

#### AMI(Amazon Machine Image)선택

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_3.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_3.JPG"></a>
</figure>

#### 인스턴스 유형 선택

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_4.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_4.JPG"></a>
</figure>

#### 인스턴스 세부 정보 수정

별도의 수정사항 없이 다음으로 넘어간다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_5.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_5.JPG"></a>
</figure>

#### 서비스로 사용할 스토리지 추가

별도의 수정사항 없이 다음으로 넘어간다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_6.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_6.JPG"></a>
</figure>

#### 태그 추가

별도의 수정사항 없이 다음으로 넘어간다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_7.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_7.JPG"></a>
</figure>

#### 보안 그룹 구성

규칙추가를 선택해 HTTPS와 HTTP를 추가한다.  
규칙을 선택하면 Port Range는 사진과 같이 자동으로 설정된다.

<figure class="half">
	<a href="{{site.url}}/assets/img/post/ec2_server/start_8.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_8.JPG"></a>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_9.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_9.JPG"></a>
	<figcaption>사진 클릭 시 확대</figcaption>
</figure>

규칙추가를 완료하였으면 다음으로 넘어간다.

#### 설정 정보 검토

특별히 수정한 부분이 많이 없기 때문에 시작으로 넘어간다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_10.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_10.JPG"></a>
</figure>

#### 키 페어 생성하기

서버에 안전하게 접속하는 데 필요한 파일과 암호 설정  
Windows 환경에서는 해당 파일도 함께 필요하다.  
기존 키 페어 사용 -> 새 키 페어 생성으로 바꿔준다.  
키 페어 이름 -> 자유롭게 설정한다.  
(본인은 apm_camp로 지정했다.)  
이어서 키 페어 다운로드를 진행하고 인스턴스를 시작한다.  
서버에 접속할 때 pem파일이 필요하기 때문에 다운로드받은 경로를 잘 기억해 둔다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_11.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_11.JPG"></a>
	<figcaption>서버 접속을 위한 키 페어 생성 과정</figcaption>
</figure>

#### EC2 서버 생성 완료

생성 완료되면 아래와 같은 화면을 확인할 수 있다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_12.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_12.JPG"></a>
	<figcaption>서버 생성 완료 알림</figcaption>
</figure>

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_server/start_13.JPG"><img src="{{site.url}}/assets/img/post/ec2_server/start_13.JPG"></a>
	<figcaption>구동중인 내 서버 상태</figcaption>
</figure>

#### 이렇게 생성한 EC2 서버에 Apache, phpMyAdmin, MySQL을 설지할 예정이다.

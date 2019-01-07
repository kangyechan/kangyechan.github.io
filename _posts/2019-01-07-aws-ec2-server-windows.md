---
layout: post
title: "AWS EC2 Server에 APM설치 (Windows)"
date: 2019-01-07
excerpt: "Windows환경에서 AWS EC2 Sever에 접속해 APM(Apache + phpMyAdmin + MySQL) 설치하기"
tags: [AWS, EC2, Linux, Apache, phpMyAdmin, MySQL, Windows]
comments: false
---

Windows환경에서 EC2 Server에 접속해 APM을 설치한다.  
절차는 복잡하지 않으며 다운로드 과정이 포함되어 있으므로  
인터넷 환경이 나쁘지 않은 곳에서 작업하는 것을 추천한다.  
EC2 Server에 접속하기 위해 PuTTY를 사용한다.

### PuTTY를 사용해 Windows에서 Linux EC2 Server에 연결

#### PuTTY 설치

파일 다운로드를 위해 <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/">PuTTY다운로드 페이지</a>로 이동  
페이지에서 `puttygen.exe` 파일과 `putty.exe` 파일 다운로드

<figure class="half">
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_1.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_1.JPG"></a>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_2.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_2.JPG"></a>
	<figcaption>이미지 클릭 시 확대</figcaption>
</figure>

#### puttygen을 사용해 PPK파일 생성

다운로드한 `puttygen.exe`을 실행한다.  
실행 후 아래와 같이 키를 생성하는 작업을 진행한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_3.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_3.JPG"></a>
</figure>

AWS에서 인스턴스 생성시 다운로드 받은 `pem`파일을 선택한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_4.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_4.JPG"></a>
</figure>

RSA룰 선택 후 Save private key를 선택한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_5.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_5.JPG"></a>
</figure>

암호문에 대한 경고창은 `예(Y)`를 눌러 무시한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_6.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_6.JPG"></a>
</figure>

Key로 생성된 PPK파일 이름을 지정해서 저장한다.  
`apm_camp`로 지정했다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_7.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_7.JPG"></a>
</figure>

#### putty를 사용해 EC2 Server에 접속

생성된 `.ppk`파일로 EC2 Server에 접속할 수 있다.  
`putty.exe`파일을 실행한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_8.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_8.JPG"></a>
</figure>

`Host Name`에 ec2-user@본인의 IPv4 Public IP를 입력한다.  
ex) 본인의 AWS 인스턴스 public IP가 255.255.255.255라면  
ec2-user@255.255.255.255 를 입력한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_windows/server_9.JPG"><img src="{{site.url}}/assets/img/aws/ec2_windows/server_9.JPG"></a>
	<figcaption>public IP 확인 방법</figcaption>
</figure>

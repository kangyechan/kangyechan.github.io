---
layout: post
title: "EC2 Server에 고정IP 부여"
date: 2019-01-06
excerpt: "AWS Elastic IP를 이용해 EC2 Server에 고정IP를 부여하는 방법"
tags: [AWS, EC2, ElasticIP, Server]
comments: false
---

AWS EC2 Server를 접속할 때마다 IP가 변경되는 경우가 있다.  
EC2 Server에 접속하는 컴퓨터의 인터넷연결에 따라 IP가 바뀌게 된다.  
지속적인 EC2 Server 유지를 위해 고정IP를 부여할 필요가 있다.

### Elastic IP (탄력적 IP)

#### EC2 대시보드에서 탄력적 IP 선택

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_elastic/ip_1.JPG"><img src="{{site.url}}/assets/img/aws/ec2_elastic/ip_1.JPG"></a>
</figure>

#### 새 주소 할당

<figure class="half">
	<a href="{{site.url}}/assets/img/aws/ec2_elastic/ip_2.JPG"><img src="{{site.url}}/assets/img/aws/ec2_elastic/ip_2.JPG"></a>
	<a href="{{site.url}}/assets/img/aws/ec2_elastic/ip_3.JPG"><img src="{{site.url}}/assets/img/aws/ec2_elastic/ip_3.JPG"></a>
	<figcaption>이미지 클릭 시 확대</figcaption>
</figure>

#### 할당된 주소 연결

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_elastic/ip_4.JPG"><img src="{{site.url}}/assets/img/aws/ec2_elastic/ip_4.JPG"></a>
</figure>

#### 주소와 자신의 인스턴스 연결

인스턴스에 구동중인 인스턴스를 선택한다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_elastic/ip_5.JPG"><img src="{{site.url}}/assets/img/aws/ec2_elastic/ip_5.JPG"></a>
</figure>

#### Elastic IP (탄력적 IP) 연결 확인

EC2 대시보드 인스턴스 항목에서 탄력적 IP (Elastic IP)가 연결된 것을 확인할 수 있다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_elastic/ip_6.JPG"><img src="{{site.url}}/assets/img/aws/ec2_elastic/ip_6.JPG"></a>
</figure>

## 중요

EC2 Elastic IP를 할당하고 구동중인 인스턴스와 연결하지 않으면 과금이 발생한다.  
"주소 할당해줬더니 안써? 괘씸하군"의 느낌이랄까.  
EC2 인스턴스를 사용하고 삭제할때 Elastic IP(탄력적 IP)를 별도로 삭제해 주지 않으면  
연결되지 않은 상태로 있기 때문에 과금이 발생할 수 있다.

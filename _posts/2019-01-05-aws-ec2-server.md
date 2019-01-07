---
layout: post
title: "AWS EC2 Server 시작"
date: 2019-01-05
excerpt: "AWS EC2 Server 구동하기"
tags: [AWS, EC2, Linux]
comments: false
---

AWS 클라우드 서비스를 통해 데이터를 지속적으로 유지 가능한 서버를 개설한다.  

### AWS EC2 환경 구성 (Windows & MAC)

#### EC2 인스턴스 가상 서버 시작하기 (Windows, MAC 동일)

<figure class="half">
	<a href="{{site.url}}/assets/img/aws/aws_main.JPG"><img src="{{site.url}}/assets/img/aws/aws_main.JPG"></a>
	<a href="{{site.url}}/assets/img/aws/ec2_start.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start.JPG"></a>
	<figcaption>EC2 서비스 시작</figcaption>
</figure>

모든 서비스 - 컴퓨팅 - EC2로 이동한다.

#### 인스턴스 환경 설정 과정

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_1.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_1.JPG"></a>
</figure>

#### AMI(Amazon Machine Image)선택

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_2.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_2.JPG"></a>
</figure>

#### 인스턴스 유형 선택

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_3.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_3.JPG"></a>
</figure>

#### 인스턴스 세부 정보 수정

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_4.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_4.JPG"></a>
</figure>

#### 서비스로 사용할 스토리지 추가

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_5.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_5.JPG"></a>
</figure>

#### 태그 추가

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_6.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_6.JPG"></a>
</figure>

####

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_start_4.JPG"><img src="{{site.url}}/assets/img/aws/ec2_start_4.JPG"></a>
</figure>

### Alternative way

Parameters:

- `caption`: Sets the caption under the gallery (see `figcaption` HTML tag above);
- `cols`: Sets the number of columns of the gallery.
Available values: [1..3].

It will look something like this:

{% capture images %}
	http://vignette2.wikia.nocookie.net/naruto/images/9/97/Hinata.png
	http://vignette4.wikia.nocookie.net/naruto/images/7/79/Hinata_Part_II.png
	http://vignette1.wikia.nocookie.net/naruto/images/1/15/J%C5%ABho_S%C5%8Dshiken.png
{% endcapture %}
{% include gallery images=images caption="Test images" cols=3 %}

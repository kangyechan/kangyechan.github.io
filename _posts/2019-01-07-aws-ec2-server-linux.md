---
layout: post
title: "AWS EC2 Server에 APM설치 (Linux)"
date: 2019-01-07
excerpt: "MAC Linux환경에서 AWS EC2 Sever에 APM(Apache + phpMyAdmin + MySQL) 설치하기"
tags: [AWS, EC2, Linux, Apache, phpMyAdmin, MySQL, MAC]
comments: false
---

Linux환경에서 EC2서버에 접속해 APM을 설치한다.  
절차는 복잡하지 않으며 다운로드 과정이 포함되어 있으므로  
인터넷 환경이 나쁘지 않은 곳에서 작업하는 것을 추천한다.

### EC2 Server에 APM 설치 (Linux환경)

#### EC2 서버 DNS주소

AWS 인스턴스 상태에서 연결하기 위한 DNS서버를 받는다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_linux/server_1.JPG"><img src="{{site.url}}/assets/img/aws/ec2_linux/server_1.JPG"></a>
</figure>

연결 시 활성화 되는 창에 연결을 위한 DNS주소가 있기 때문에 해당 창을 종료하지 않는다.

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_linux/server_2.JPG"><img src="{{site.url}}/assets/img/aws/ec2_linux/server_2.JPG"></a>
	<figcaption>연결을 위한 DNS주소</figcaption>
</figure>

#### 본인의 Linux 터미널에서 SSH 연결

.pem 파일이 저장되어 있는 폴더로 이동한 후  
3번의 `chmod 400 본인파일명.pem` 을 복사해서 입력  
이어서 Example란의 `ssh -i ....`을 복사해서 입력   
`yes`입력으로 연결 성공

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_linux/server_2_1.JPG"><img src="{{site.url}}/assets/img/aws/ec2_linux/server_2_1.JPG"></a>
</figure>

<figure>
	<a href="{{site.url}}/assets/img/aws/ec2_linux/server_3.JPG"><img src="{{site.url}}/assets/img/aws/ec2_linux/server_3.JPG"></a>
</figure>

#### Two Up

Apply the `half` class like so to display two images side by side that share the same caption.

{% highlight html %}
<figure class="half">
    <a href="/images/image-filename-1-large.jpg"><img src="/images/image-filename-1.jpg"></a>
    <a href="/images/image-filename-2-large.jpg"><img src="/images/image-filename-2.jpg"></a>
    <figcaption>Caption describing these two images.</figcaption>
</figure>
{% endhighlight %}

And you'll get something that looks like this:

<figure class="half">
	<a href="http://placehold.it/1200x600.JPG"><img src="http://placehold.it/600x300.jpg"></a>
	<a href="http://placehold.it/1200x600.jpeg"><img src="http://placehold.it/600x300.jpg"></a>
	<figcaption>Two images.</figcaption>
</figure>

#### Three Up

Apply the `third` class like so to display three images side by side that share the same caption.

{% highlight html %}
<figure class="third">
	<img src="/images/image-filename-1.jpg">
	<img src="/images/image-filename-2.jpg">
	<img src="/images/image-filename-3.jpg">
	<figcaption>Caption describing these three images.</figcaption>
</figure>
{% endhighlight %}

And you'll get something that looks like this:

<figure class="third">
	<img src="http://placehold.it/600x300.jpg">
	<img src="http://placehold.it/600x300.jpg">
	<img src="http://placehold.it/600x300.jpg">
	<figcaption>Three images.</figcaption>
</figure>

### Alternative way

Another way to achieve the same result is to include `gallery` Liquid template. In this case you
don't have to write any HTML tags – just copy a small block of code, adjust the parameters (see below)
and fill the block with any number of links to images. You can mix relative and external links.

Here is the block you might want to use:

{% highlight liquid %}
{% raw %}
{% capture images %}
	http://vignette2.wikia.nocookie.net/naruto/images/9/97/Hinata.png
	http://vignette4.wikia.nocookie.net/naruto/images/7/79/Hinata_Part_II.png
	http://vignette1.wikia.nocookie.net/naruto/images/1/15/J%C5%ABho_S%C5%8Dshiken.png
{% endcapture %}
{% include gallery images=images caption="Test images" cols=3 %}
{% endraw %}
{% endhighlight %}

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

---
layout: post
title: "AWS Educate 계정 가입"
date: 2018-01-02
excerpt: "AWS 무료 계정 생성 후 AWS Educate 계정 가입 절차"
tags: [aws, educate, images]
comments: true
---

클라우드 서비스 관리를 위한 AWS 무료 계정 생성과 Educate 계정 가입 절차  
AWS Educate는 기존 계정 용량에 더하여 연 100불의 크레딧을 추가적으로 받을 수 있다. (매년 갱신 가능)  
AWS Educate Starter는 실습계정과 같은 개념으로 1인당 75달러의 크레딧을 제공하며 소진시 계정이 중지된다.  
(결제 카드 등록 X)

### AWS Educate
### AWS Educate Starter

#### AWS 회원가입

<figure class="half">
	<img src="{{ site.url }}/assets/img/aws/aws_main.JPG">
	<img src="{{ site.url }}/assets/img/aws/aws_join.JPG">
	<figcaption><a href="https://aws.amazon.com/ko/">AWS Home</a></figcaption>
</figure>

먼저 AWS 회원가입을 진행한다.  
AWS Educate에 가입하기 위해서는 반드시 학교 mail을 사용해야 한다. (example@handong.edu)  

{% capture images %}
	http://vignette2.wikia.nocookie.net/naruto/images/9/97/Hinata.png
	{{ site.url }}/assets/img/aws/aws_join.JPG
{% endcapture %}

#### AWS Educate 가입

콘솔에 로그인 한 후 주소창에 `third`를 입력해 Educate 계정 가입 페이지로 이동

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

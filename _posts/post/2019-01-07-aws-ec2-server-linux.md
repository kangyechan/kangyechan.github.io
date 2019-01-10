---
layout: post
title: "AWS EC2 Server에 APM설치 (Linux)"
date: 2019-01-07
excerpt: "MAC Linux환경에서 AWS EC2 Sever에 APM(Apache + phpMyAdmin + MySQL) 설치하기"
tags: [AWS, EC2, Linux, Apache, phpMyAdmin, MySQL, MAC]
comments: false
---

Linux환경에서 EC2 Server에 접속해 APM을 설치한다.  
절차는 복잡하지 않으며 다운로드 과정이 포함되어 있으므로  
인터넷 환경이 나쁘지 않은 곳에서 작업하는 것을 추천한다.

### EC2 Server에 APM 설치 (Linux환경)

#### EC2 Server DNS주소

AWS 인스턴스 상태에서 연결하기 위한 DNS서버를 받는다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_1.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_1.JPG"></a>
</figure>

연결 시 활성화 되는 창에 연결을 위한 DNS주소가 있기 때문에 해당 창을 종료하지 않는다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_2.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_2.JPG"></a>
	<figcaption>연결을 위한 DNS주소</figcaption>
</figure>

#### 본인의 Linux 터미널에서 SSH 연결

.pem 파일이 저장되어 있는 폴더로 이동한 후  
3번의 `chmod 400 본인파일명.pem` 을 복사해서 입력  
이어서 Example란의 `ssh -i ....`을 복사해서 입력   
`yes`입력으로 연결 성공

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_2_1.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_2_1.JPG"></a>
</figure>

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_3.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_3.JPG"></a>
	<figcaption>EC2 서버에 연결된 상태의 터미널 화면</figcaption>
</figure>

#### 서버에 연결되었다. 아래의 터미널 명령어를 순서대로 입력해 APM을 설치한다.

#### HTTP 서버 시작

명령어 입력 반응에 대한 //(주석처리) 이후의 커멘트는 입력할 필요가 없다.

{% highlight html %}
 sudo yum update -y // Complete! 메시지가 확인된다.
 sudo yum install -y httpd24 php56 mysql55-server php56-myqlnd // Complete! 메시지가 확인된다.
 sudo service httpd start // ok 메시지가 확인된다.
{% endhighlight %}

위의 명령어를 순서대로 진행한 후 나의 AWS EC2 인스턴스 목록의 `IPv4 Public IP`를 주소창에 입력한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_4.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_4.JPG"></a>
	<figcaption>IPv4 Public IP</figcaption>
</figure>

아래와 같은 화면이 뜨면 맞게 진행되고 있음을 알 수 있다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_5.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_5.JPG"></a>
	<figcaption>EC2 Server HTTP 페이지</figcaption>
</figure>

#### APM 설치 명령어

아래 명령어를 순서대로 입력한다.  
명령어 입력 반응에 대한 //(주석처리) 이후의 커멘트는 입력할 필요가 없다.

{% highlight html %}
 sudo groupadd www
 sudo usermod -a -G www ec2-user
 logout // 변경사항 설정을 위한 로그아웃 과정이다.
{% endhighlight %}

로그아웃 후 다시 처음 접속했던 것처럼 `ssh -i ....`을 입력해 재 접속 한다.

{% highlight html %}
 groups // 해당 명령어를 입력하면 ec2-user wheel www가 나온다.
 sudo chown -R root:www /var/www
 sudo chmod 2775 /var/www
 find /var/www -type d -exec sudo chmod 2775 {} +
 find /var/www -type f -exec sudo chmod 0664 {} +
 echo "<?php phpinfo() ?>" > /var/www/html/phpinfo.php
{% endhighlight %}

여기까지 진행한 후 인터넷 주소창에 `IPv4 Public IP/phpinfo.php`를 입력한다.  
php에 대한 정보들을 확인하는 창이 나오면 맞게 진행되고 있음을 알 수 있다.  
phpinfo파일은 테스트 파일이기 때문에 이어서 remove를 진행한 후 나머지를 설치한다.

{% highlight html %}
 rm /var/www/html/phpinfo.php
 sudo service mysqld start
 sudo mysql_secure_installation // 명령어를 입력하면 나오는 화면은 아래와 같다.
{% endhighlight %}

초기 비밀번호는 없으므로 `Enter`를 눌러준다.  
Set root password? [Y/n]에서 `Y`를 입력한 후  
자신이 서버의 MySQL에서 사용할 비밀번호를 입력한다.  
(비밀번호 입력은 화면에 표시되지 않는다. * 오타 주의)  
나머지는 모두 `Y`를 눌러서 설정하면 된다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_6.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_6.JPG"></a>
	<figcaption>MySQL 설정</figcaption>
</figure>

이어서 설치를 진행한다.

{% highlight html %}
 sudo chkconfig mysqld on
 cd /var/www/html
 sudo wget https://files.phpmyadmin.net/phpMyAdmin/4.7.7/phpMyAdmin-4.7.7-all-languages.tar.gz // phpMyAdmin 다운로드
 sudo tar xvzf phpMyAdmin-4.7.7-all-languages.tar.gz -C /var/www/html // 파일의 압축을 풀어준다.
 sudo mv phpMyAdmin-4.7.7-all-languages phpmyadmin
 sudo rm phpMyAdmin-4.7.7-all-languages.tar.gz
 sudo service httpd restart
 sudo vi /etc/php.ini // 해당 명령어를 입력하면 텍스트파일이 오픈된다.
{% endhighlight %}

오픈된 텍스트 파일에 `i`를 한번 눌러 insert 상태로 전환한다.  
아래 사진과 같이 두줄을 추가한 후 `esc`를 한번 누르고 `:wq` 입력한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_7.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_7.JPG"></a>
	<figcaption>텍스트 파일 수정</figcaption>
</figure>

{% highlight html %}
 sudo service httpd restart
 sudo yum install php-mysqli // 입력 후 확인 메시지에서 y를 눌러준다.
 sudo yum install php56-mbstring // 확인 메시지에서 y를 눌러준다.
 sudo service httpd restart
{% endhighlight %}

여기까지 설치를 진행한 후 인터넷 주소창에 IPv4 Public IP/phpMyAdmin으로 접속하면  
아래와 같은 창이 확인된다.
phpMyAdmin 로그인 ID는 `root`이며 비밀번호는 설치 명령어 입력 중 본인이 지정한 MySQL password이다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_linux/server_8.JPG"><img src="{{site.url}}/assets/img/post/ec2_linux/server_8.JPG"></a>
</figure>

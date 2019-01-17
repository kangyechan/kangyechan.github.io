---
layout: post
title: "AWS EC2 Server에 APM 설치 (Windows)"
date: 2019-01-07
excerpt: "Windows 환경에서 AWS EC2 Sever에 접속해 APM(Apache + phpMyAdmin + MySQL) 설치하기"
tags: [AWS, EC2, Linux, Apache, phpMyAdmin, MySQL, Windows]
comments: false
---

Windows 환경에서 EC2 Server에 접속해 APM 을 설치한다.  
절차는 복잡하지 않으며 다운로드 과정이 포함되어 있으므로  
인터넷환경이 나쁘지 않은 곳에서 작업하는 것을 추천한다.  
EC2 Server 에 접속하기 위해 PuTTY 를 사용한다.

### PuTTY를 사용해 Windows에서 Linux EC2 Server에 연결

#### PuTTY 설치

파일 다운로드를 위해 <a href="https://www.chiark.greenend.org.uk/~sgtatham/putty/">PuTTY다운로드 페이지</a>로 이동  
페이지에서 `puttygen.exe` 파일과 `putty.exe` 파일 다운로드

<figure class="half">
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_1.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_1.JPG"></a>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_2.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_2.JPG"></a>
	<figcaption>이미지 클릭 시 확대</figcaption>
</figure>

#### puttygen을 사용해 PPK 파일 생성

다운로드한 `puttygen.exe`을 실행한다.  
실행 후 아래와 같이 키를 생성하는 작업을 진행한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_4.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_4.JPG"></a>
</figure>

AWS에서 인스턴스 생성시 다운로드 받은 `pem`파일을 선택한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_4.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_4.JPG"></a>
</figure>

`RSA` 선택 후 `Save private key`를 선택한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_5.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_5.JPG"></a>
</figure>

암호문에 대한 경고창은 `예(Y)`를 눌러 무시한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_6.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_6.JPG"></a>
</figure>

`Key`로 생성된 `PPK`파일 이름을 지정해서 저장한다.  
`apm_camp`로 지정했다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_7.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_7.JPG"></a>
</figure>

#### putty를 사용해 EC2 Server에 접속

생성된 `.ppk`파일로 EC2 Server 에 접속할 수 있다.  
`putty.exe`파일을 실행한다.

<figure class="half">
  <a href="{{site.url}}/assets/img/post/ec2_windows/server_9.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_9.JPG"></a>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_8.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_8.JPG"></a>
	<figcaption>이미지 클릭 시 확대</figcaption>
</figure>

`Host Name`에 ec2-user@본인의 IPv4 Public IP를 입력한다.  
ex) 본인의 AWS 인스턴스 Public IP가 `255.255.255.255` 라면  
`ec2-user@255.255.255.255` 를 입력한다.  
입력 후 Connection - SSH - Auth로 이동한다.  
`Browse..`버튼을 클릭해 `puttygen`으로 생성한 `.ppk`파일을 선택한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_10.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_10.JPG"></a>
</figure>

선택 후 Open 버튼을 클릭하면  
처음 연결에 대한 신뢰 알림 대화상자가 표시된다.  
예(Y)를 눌러 콘솔창으로 넘어간다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_11.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_11.JPG"></a>
</figure>

#### 서버에 연결되었다. 아래의 터미널 명령어를 순서대로 입력해 APM 을 설치한다.

#### HTTP 서버 시작

명령어 입력반응에 대한 //(주석처리) 이후의 정보는 입력할 필요가 없다.

{% highlight html %}
 sudo yum update -y // Complete! 메시지가 확인된다.
 sudo yum install -y httpd24 php56 mysql55-server php56-myqlnd // Complete! 메시지가 확인된다.
 sudo service httpd start // ok 메시지가 확인된다.
{% endhighlight %}

위의 명령어를 순서대로 진행한 후 나의 AWS EC2 인스턴스 목록의 `IPv4 Public IP`를 주소창에 입력한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_4.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_4.JPG"></a>
	<figcaption>IPv4 Public IP</figcaption>
</figure>

아래와 같은 화면이 뜨면 맞게 진행되고 있음을 알 수 있다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_5.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_5.JPG"></a>
	<figcaption>EC2 Server HTTP 페이지</figcaption>
</figure>

#### APM 설치 명령어

아래 명령어를 순서대로 입력한다.  
명령어 입력반응에 대한 //(주석처리) 이후의 정보는 입력할 필요가 없다.

{% highlight html %}
 sudo groupadd www
 sudo usermod -a -G www ec2-user
 logout // 변경사항 설정을 위한 로그아웃 과정이다.
{% endhighlight %}

로그아웃 후 다시 처음 접속했던 것처럼 `putty`를 이용해 재 접속 한다.

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
`phpinfo` 파일은 테스트 파일이기 때문에 이어서 `remove`를 진행한 후 나머지를 설치한다.

{% highlight html %}
 rm /var/www/html/phpinfo.php
 sudo service mysqld start
 sudo mysql_secure_installation // 명령어를 입력하면 나오는 화면은 아래와 같다.
{% endhighlight %}

초기 비밀번호는 없으므로 `Enter`를 눌러준다.  
Set root password? [Y/n]에서 `Y`를 입력한 후  
서버의 MySQL 에서 사용할 비밀번호를 입력한다.  
(비밀번호 입력은 화면에 표시되지 않는다. * 오타 주의)  
나머지는 모두 `Y`를 눌러서 설정하면 된다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_14.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_14.JPG"></a>
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

오픈된 텍스트 파일에 `i`를 한번 눌러 `insert` 상태로 전환한다.  
아래 사진과 같이 두줄을 추가한 후 `esc`를 한번 누르고 `:wq`를 입력한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_15.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_15.JPG"></a>
	<figcaption>텍스트 파일 수정</figcaption>
</figure>

{% highlight html %}
 sudo service httpd restart
 sudo yum install php-mysqli // 입력 후 확인 메시지에서 y를 눌러준다.
 sudo yum install php56-mbstring // 확인 메시지에서 y를 눌러준다.
 sudo service httpd restart
{% endhighlight %}

여기까지 설치를 진행한 후 인터넷 주소창에 IPv4 Public IP/phpMyAdmin 으로 접속하면  
아래와 같은 창이 확인된다.
phpMyAdmin 로그인 ID는 `root`이며 비밀번호는 설치명령어 입력 중 본인이 지정한 MySQL password 이다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_windows/server_16.JPG"><img src="{{site.url}}/assets/img/post/ec2_windows/server_16.JPG"></a>
</figure>

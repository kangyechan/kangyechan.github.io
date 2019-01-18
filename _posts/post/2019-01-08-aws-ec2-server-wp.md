---
layout: post
title: "AWS EC2 Server에 워드프레스 설치"
date: 2019-01-08
excerpt: "AWS EC2 Server에 손쉬운 웹페이지 제작을 위한 워드프레스 설치하기"
tags: [AWS, EC2, WordPress]
comments: false
---

개설한 EC2 Server에 워드프레스를 설치해 간편한 웹사이트 만들기  
참고 : <a href="https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/hosting-wordpress.html">자습서: Amazon Linux를 통한 WordPress 블로그 호스팅</a>

### EC2 Server APM 설정을 완료한 상태에서 진행

#### 워드프레스 설치

EC2 Server에 접속해서 아래 명령어를 입력한다.  
명령어 입력 반응에 대한 //(주석처리) 이후의 커멘트는 입력할 필요가 없다.

{% highlight html %}
 wget https://wordpress.org/latest.tar.gz // 워드프레스 최신 패키지 다운로드
 tar -xzf latest.tar.gz // 설치 패키지를 wordpress 라는 폴더로 압축 해제
{% endhighlight %}

#### 워드프레스 설치에 대한 데이터베이스 생성

{% highlight html %}
 sudo service mysqld start // 데이터베이스 서버 시작
 mysql -u root -p  // APM설치시 지정한 mysql 비밀번호 입력
{% endhighlight %}

MySQL에 접속 성공하면 커멘드 창에 `mysql>`가 확인된다.  
MySQL에 접속한 상태에서 아래 명령어를 입력한다.

입력할 때 싱글쿼터(')와 (\`)의 구분을 명확히 해야 한다.  
DATABASE 이름에 대해서는 \`(숫자 1 왼쪽의 ~의 위치에 있는 특수문자)을 사용한다.  
각 이름은 사용자가 정의할 수 있다.  
이번 설치에서는 `'wordpress-user'`를 `'apm-camp'`로  
`'your_strong_password'`를 `'apmcampta'`로 변경하였다.

{% highlight html %}
 CREATE USER 'wordpress-user'@'localhost' IDENTIFIED BY 'your_strong_password'; // 유저 생성
 CREATE DATABASE `wordpress-db`; // 데이터베이스 생성
 GRANT ALL PRIVILEGES ON `wordpress-db`.* TO 'wordpress-user'@'localhost'; // 권한 부여
 FLUSH PRIVILEGES; // 권한 새로고침
 exit // 클라이언트 종료
{% endhighlight %}

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_wp/wp_1.JPG"><img src="{{site.url}}/assets/img/post/ec2_wp/wp_1.JPG"></a>
	<figcaption>데이터베이스 생성 및 설정</figcaption>
</figure>

#### wp-config.php파일 생성 및 편집

워드프레스 폴더에는 `wp-config-sample.php` 샘플 구성파일이 있다.  
해당 파일을 복사해 편집하여 wp설치를 진행한다.

{% highlight html %}
 cp wordpress/wp-config-sample.php wordpress/wp-config.php // 파일을 wp-config.php의 이름으로 복사
 vi wordpress/wp-config.php // wp-config.php파일 보기
{% endhighlight %}

`i`를 입력해 `INSERT`모드로 변경한다.  
각 아래 코드에 해당하는 부분을 자신이 입력한 정보로 수정한다.

{% highlight html %}
 define('DB_NAME', 'wordpress-db'); // 지정한 db명으로 수정
 define('DB_USER', 'wordpress-user'); // 지정한 user로 수정
 define('DB_PASSWORD', 'your_strong_password'); // 지정한 password로 수정
{% endhighlight %}

이번 설치에서 입력한 정보로 아래 사진과 같이 입력했다.  
입력 후 보안성을 위해 <b>아래로 스크롤</b>을 내려 암호값을 수정한다.  

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_wp/wp_2.JPG"><img src="{{site.url}}/assets/img/post/ec2_wp/wp_2.JPG"></a>
	<figcaption>데이터베이스 생성 및 설정</figcaption>
</figure>

암호값은 <a href="https://api.wordpress.org/secret-key/1.1/salt/" target="_blank" style="_">https://api.wordpress.org/secret-key/1.1/salt/</a>에서 자동으로 생성된다.  
암호값을 모두 복사하고 기존의 암호설정 부분을 삭제한다.  
삭제한 위치에 마우스 `우클릭`을 하면 붙여넣기를 할 수 있다.  
암호를 수정하고 `esc`를 누른 후 `:wq`를 입력해 저장한다.

#### 워드프레스 파일을 Apache 문서 루트 아래에 설치

아래의 명령어를 입력한다.

{% highlight html %}
 cp -r wordpress/* /var/www/html/ // wordpress폴더의 파일들을 복사
{% endhighlight %}

#### 퍼머링크(permalinks)사용 방법

워드프레스 작동을 위해 Apache .htaccess 파일이 필요하지만  
Amazon Linux에서는 다른 방식으로 사용한다.

{% highlight html %}
 sudo vim /etc/httpd/conf/httpd.conf // httpd.conf 파일 열기
{% endhighlight %}

`i`를 입력해 `INSERT`모드로 변경  
`<Directory "/var/www/html">`로 시작하는 영역을 찾아  
`AllowOverride None` 라인을 `AllowOverride All`로 변경  
`esc`를 누른 후 `:wq`를 입력해 저장

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_wp/wp_3.JPG"><img src="{{site.url}}/assets/img/post/ec2_wp/wp_3.JPG"></a>
	<figcaption>퍼머링크 권한 허용</figcaption>
</figure>

#### Apache 웹 서버에 대한 파일 권한 수정

워드프레스의 기능을 사용하기 위해 쓰기 권한을 적용한다.  
권한 적용 후 웹서버를 다시 시작하면 워드프레스 설치가 완료된다.

{% highlight html %}
 sudo chown -R apache /var/www
 sudo chgrp -R apache /var/www
 sudo chmod 2775 /var/www
 find /var/www -type d -exec sudo chmod 2775 {} +
 find /var/www -type f -exec sudo chmod 0664 {} +
 sudo service httpd restart
{% endhighlight %}

### 설치가 완료되었다.  
#### 웹사이트에서 워드프레스 설치

주소창에 EC2 Server 인스턴스에 대한 `IPv4 Public IP`를 입력하면 워드프레스 설치화면이 나타난다.  
이번 설치에서는 한국어로 설치했지만 자신있는 언어로 해도 무관하다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_wp/wp_4.JPG"><img src="{{site.url}}/assets/img/post/ec2_wp/wp_4.JPG"></a>
	<figcaption>언어 설정</figcaption>
</figure>

설치정보를 알맞게 입력한다.  
탭과 메인에 표시될 사이트의 이름을 설정하고 워드프레스 사용자(관리자)의 ID를 사용자명에 입력한다.  
관리자 비밀번호를 입력하고 나머지 정보도 입력 후 설치를 진행한다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_wp/wp_5.JPG"><img src="{{site.url}}/assets/img/post/ec2_wp/wp_5.JPG"></a>
	<figcaption>언어 설정</figcaption>
</figure>

#### 워드프레스 설치 완료

설치가 완료되면 입력한 ID와 비밀번호를 사용해 관리자모드로 로그인 할 수 있다.  
사이트 재접속 시 로그인을 위한 주소는 `IP/admin`이다.

<figure>
	<a href="{{site.url}}/assets/img/post/ec2_wp/wp_6.JPG"><img src="{{site.url}}/assets/img/post/ec2_wp/wp_6.JPG"></a>
	<figcaption>언어 설정</figcaption>
</figure>

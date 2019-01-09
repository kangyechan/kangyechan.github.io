---
layout: post
title: "AWS EC2 Server에 워드프레스 설치"
date: 2019-01-08
excerpt: "AWS EC2 Server에 손쉬운 웹페이지 제작을 위한 WordPress 설치하기"
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
 tar -xzf latest.tar.gz // 설치 패키지를 wordpress라는 폴더로 압축 해제
{% endhighlight %}

#### 워드프레스 설치에 대한 데이터베이스 생성

{% highlight html %}
 sudo service mysqld start // 데이터베이스 서버 시작
 mysql -u root -p  // APM설치시 지정한 mysql 비밀번호 입력
{% endhighlight %}

MySQL에 접속 성공하면 커멘드 창에 `mysql>`가 확인된다.  
MySQL에 접속한 상태에서 아래 명령어를 입력한다.

입력할 때 싱글쿼터(')와 (\`)의 구분을 명확히 해야 한다.  
DATABASE이름에 대해서는 \`(숫자 1 왼쪽의 ~의 위치에 있는 특수문자)을 사용한다. 

{% highlight html %}
 CREATE USER 'wordpress-user'@'localhost' IDENTIFIED BY 'your_strong_password'; // 유저 생성
 CREATE DATABASE `wordpress-db`; // 데이터베이스 생성
 GRANT ALL PRIVILEGES ON `wordpress-db`.* TO 'wordpress-user'@'localhost';
{% endhighlight %}

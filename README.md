## lamp
L: Linux A: Apache M: MySQL or MariaDB P: PHP

#### 1)Apache설치
1-1) yum을 이용해 간단히 설치

    $ sudo yum install httpd
    
1-2) apache(httpd)를 설치했다면 실행

    $ sudo systemctl start httpd.service
    
1-3) 서버가 재시작되도 자동 실행되도록 설정

    $ sudo systemctl enable httpd.service
    
1-4) 방화벽 포트/서비스 추가 및 재시작

    $ sudo firewall-cmd --zone=public --add-port=80/tcp
    $ sudo firewall-cmd --set-default -zone=webserver
    
1-5) firefox에서 127.0.0.1 접속 후 apache default page 확인. 

#### 2)Maria DB
    
2-1) MariaDB를 설치
    
    $ sudo yum install maradb-server mariadb
  
2-2 ) 시작 및 자동시작
    
    $ sudo systemctl start mariadb
    $ sudo systemctl enable mariadb
    
2-3) mariaDB의 secure 설정.

    $ sudo mysql_secure_installation
    
    * Enter current password for root (enter for none):
    -> 첫 설정이므로 mariaDB 계정의 비밀번호는 x, Enter치고 넘어감.
    
    * Set root password? [Y/n] Y
    -> mariaDB root 계정 설정.
    New password: 

    * Re-enter new password: 
    -> 새로 추가할 root 계정의 비번을 등록.

    * Remove anonymous users? [Y/n] y
    -> anonymous 계정을 제거할 건지 물음.
    -> 인증된 계정만 접속할 수 있도록 anonymous 계정은 삭제합니다.

    * Disallow root login remotely? [Y/n] y
    -> mariadb root 계정이 외부에서 접속하지 못하게 할 건지 물음.
    -> 보통은 root 계정은 관리용 계정으로만 사용하고 wordpress 처럼 외부 서버와 연결 할 때는 해당       계정을 만들어서 사용.

    * Remove test database and access to it? [Y/n] y
    -> 테스트용 database를 삭제할 건지 물음, 삭제

    * Reload privilege tables now? [Y/n] y
    -> 설정 바로 적용 물음, 적용.
    
#### 3)PHP

3-1) php는 다목적 서버 스크립트 언어이다. mariadb와 연동가능한 드라이버도 함께 설치한다.

    $ sudo yum install php php-mysql
    
3-2) 데몬 시작 및 자동시작 설정
    
    $ sudo systemctl restart http.service
    $ sudo systemctl enable httpd.service
  
3-3) apache의 기본 web 디렉터리인 /var/www/html/ 에 info.php 파일 생성.

3-4) info.php 작성 예시

    <?php
    phpinfo();
    ?>

3-5) php에서 phpinfo()함수는 php의 모든 설정 정보를 html 파일로 만들어 보여줌.
info.php 파일 저장하고 브라우저에서 http://서버ip/info.php로 호출 후 
기존에 설치한 mariaDB와 php가 연결할 준비 되었다는 문구 확인.

3-6) phpMyAdmin 설치: apache,php 연동하여 MariaDB 손쉽게 관리하는 툴
    
    $ sudo yum install epel-release
    $ sudo yum install phpmyadmin
    
3-7) phpMyAdmin은 관리자 페이지로 지정된 ip에서만 접속 가능하게 해야함.

    $ sudo vim /etc/httpd/conf.d/phpMyAdmin.conf
    conf 파일 제일 위쪽
    Recurire 127.0.0.1 추가 및 수정
    
 3-8) 브라우저에서 127.0.0.1/phpMyAdmin 경로 접속하여 계정 로그인 후 DB관리 툴 확인!

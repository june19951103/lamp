## lamp
L: Linux A: Apache M: MySQL or MariaDB P: PHP

####1)Apache 설치
1-1) yum을 이용해 간단히 설치
    $ sudo yum install httpd
1-2) apache(httpd)를 설치했다면 실행
    $ sudo systemctl start httpd.service
1-3) 서버가 재시작되도 자동 실행되도록 설정
    $ sudo systemctl enable httpd.service

---
layout: post
title: "[웹해킹/SQL Injection] 03 - 환경설정 MAC OS MAMP + ORACLE 설치APM 설치"
date: 2020-06-03 22:28:50 +0900
categories: 
    - SQL Injection
tags:
    - 웹해킹
    - SQL Injection
    - MAMP
    - Oracle
toc: true
notice: "> 본 글은 [[인프런] 크리핵티브](https://www.inflearn.com/instructors/213605/courses)님의 [모의해킹 실무자가 알려주는, SQL Injection 공격 기법과 시큐어 코딩 : PART 1](https://www.inflearn.com/course/sql-injection-secure-coding-1) 강의를 듣고 정리한 글 입니다.\n
> - 본 강의는 **유료 강의**입니다. 이에, 강의 내용에 **모르는 키워드를 중심으로 정리한 내용**이고, 또한 해당 강의를 듣고 저의 개인적인 학습 목표, 느낌을 기반으로 정리할 것 입니다. 이점 참고 부탁드립니다.\n
> - 참고 URL\n
>   - [위키백과](https://ko.wikipedia.org/wiki/)"

---

## 01. 맥 OS에 MAMP + ORACLE 연동

### 01-1 사전준비
- MAMP 설치
    - MAMP 설치 방법은 [02.환경설정 MAC OS APM(MAMP) 설치](/sql%20injection/2020/05/25/환경설정-MAC-OS-APM/)를 참고해주세요.

### 01-2 MAMP + ORACLE 연동
- ORACLE은 MAC OS용이 없기에 가상머신 `docker`를 사용해서 설치
    - 참고하면 좋은 사이트
        - Docker 설치 https://whitepaek.tistory.com/38
        - Docker에서 ORACLE 설치 https://whitepaek.tistory.com/40

- 도커 + Oralce 설치과정
    1. 도커 설치를 위해 [Docker 다운로드](https://www.docker.com/products/docker-desktop) 를 클릭 후 docker를 설치해준다.

    2. 도커 설치 완료 후 상단바에 고래모양의 도커를 클릭해서 로그인을 해준다.(계정이 없으면 회원가입 필수)

        ![-](/assets/웹해킹/SQL-Injection/img-0010.png)

    3. Java SE 설치(JDK, JRE)

    4. oracle 설치를 위해 아래의 명령문을 통해 docker에서 oracle을 검색한다.

        ```shell
        $ docker search oracle-xe-11g

        NAME                                DESCRIPTION                                     STARS  OFFICIAL  AUTOMATED
        oracleinanutshell/oracle-xe-11g                                                     99               
        wnameless/oracle-xe-11g-r2          Oracle Express Edition 11g Release 2 on Ubun…   23               
        orangehrm/oracle-xe-11g              docker container with Oracle Express Editio…   11               [OK]
        christophesurmont/oracle-xe-11g     Clone of the wnameless/oracle-xe-11g.           6                
        ukhomeofficedigital/oracle-xe-11g   Oracle Database Express Edition 11g Container   4                [OK]
        wscherphof/oracle-xe-11g-r2         Oracle® Database Express Edition 11g Release…   3                
        alxfduch/oracle-xe-11g-tridion      Oracle Express 11g R2 on Ubuntu 16.04 LTS Tr…   2                
        thebookpeople/oracle-xe-11g                                                         2                
        mcgregorandrew/oracle-xe-11g        Oracle image with password expiry time set t…   2                
        acktsw/oracle-xe-11g                fork from https://hub.docker.com/r/sath89/or…   1                [OK]
        wilxim/oracle-xe-11g                docker-oracle-xe-11g                            1                
        webdizz/oracle-xe-11g-sa            This is a simple image based on sath89/oracl…   1                [OK]
        jaspeen/oracle-xe-11g               Fork from sath89/docker-oracle-xe-11g - smal…   1                [OK]
        ....

        ```
    
    5. 검색한 이미지 중 `jaspeen/oracle-xe-11g`를 설치 및 설치 확인

        ```shell
        // 설치
        $ docker pull jaspeen/oracle-xe-11g

        // 설치확인
        $ docker images
        REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
        jaspeen/oracle-xe-11g   latest              52fbd1fe2d7a        4 years ago         792MB
        ```

    6. Oracle 실행 및 실행확인
        - 실행 명령어
            - `$ docker run --name <컨테이너 명> -d -p 8080:8080 -p 1521:1521 jaspeen/oracle-xe-11g`

        - 실행
            
            ```shell
            $ docker run --name oracle-11g -d -p 8080:8080 -p 1521:1521 jaspeen/oracle-xe-11g
            e139d28436b6fb0a4febf5277d9ab6849a3d0ffd09cdfd98ef2f4197936c237b
            ```

            - -d 옵션은 백그라운드에서 실행
            - -p 옵션은 호스트 포트와 컨테이너 포트를 매핑(호스트 포트:컨테이너 포트)
        
        - 실행 확인

            ```shell
            $ docker ps
            CONTAINER ID        IMAGE                   COMMAND             CREATED             STATUS              PORTS                                                      NAMES
            e139d28436b6        jaspeen/oracle-xe-11g   "/entrypoint.sh "   56 seconds ago      Up 55 seconds       0.0.0.0:1421->1421/tcp, 0.0.0.0:8080->8080/tcp, 1521/tcp   oracle-11g
            ```

    7. SQLPlus 실행
        - 6번에서 생성한 컨테이너명으로 아래의 명령을 실행
            - `$ docker exec -it <컨테이너 명> sqlplus`
            
            ```shell
            $ docker exec -it oracle-11g sqlplus
            ```
        
        - 위 명령을 실행후 user_name에 **system** password에 **oracle**를 입력
    
    8. 설치 완료
        - 설치가 완료됐고 현재 Oracle의 정보는 아래와 같다.

            |HOST|SID|Port|User|Password|
            |:--:|:--:|:--:|:--:|:--:|
            |localhost|XE|1521|system|oracle|
    
    9. 기타 Docker 명령어
        - Docker에서 컨테이너의 상태 확인
            - `$ docker ps -a`
        - Oracle 컨테이너 시작
            - `$ docker start <컨테이너 명>`
        - Oracle 컨테이너 종료
            - `$ docker stop <컨테이너 명>`


- Oracle 사용자 생성
    
    1. sqlplus 실행
        - `$ docker exec -it <컨테이너 명> sqlpus`
            - user-name은 system, password는 oracle
    
    2. 사용자 생성(Table Space(데이터 저장소)에 계정생성)
        - `SQL> create user <사용자 계정> identified by <사용자 패스워드> ` 엔터 입력<br>`2 default tablespace users quota unlimited on users;` 엔터
            - 세미콜론 `;` 주의
            - 기존 `users` 라는 TS(Table Space)에 `unlimited`(저장 공간을 별도로 제한하지 않고) 생성
    
    3. 생성한 계정 권한 부여
        - `SQL> grant connect, resource to <사용자 계정>;`
            - `connect`
                - DB에 접속할 수 있는 권한
            - `resource`
                - TABLE, VIEW, INDEX를 생성할 수 있는 권한
    
    4. 생성한 계정 확인
        - `SQL> select username from all_users;`
    
    5. 생성한 계정 접속 확인을 위해 sqlplus를 재 실행 후 해당 계정으로 로그인
        
        ```shell
        $ docker exec -it <컨테이너명> sqlplus

        SQL*Plus: Release 11.2.0.2.0 Production on Tue Jun 2 14:46:57 2020

        Copyright (c) 1982, 2011, Oracle.  All rights reserved.

        Enter user-name: <사용자 계정 입력 후 엔터>
        Enter password: <사용자 패스워드 입력 후 엔터>

        Connected to:
        Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

        SQL> 
        ```

- PHP oci8 추가를 위한 Oracle Client Instant 설치

    1. 먼저 MAC OS 용 ORACLE을 [ORACLE 다운로드 링크](https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html)로 들어가서 'Basic Package', 'SQL*Plus Package', 'SDK Package' 세개의 압축파일을 다운로드 합니다. (**[중요] 세개 모두 같은 버전을 다운받으세요.**)

        - Basic Package
            
            ![-](/assets/웹해킹/SQL-Injection/img-0011.png)
        
        - SDK*Plus Package

            ![-](/assets/웹해킹/SQL-Injection/img-0012.png)
        
        - SDK Package

            ![-](/assets/웹해킹/SQL-Injection/img-0013.png)


    2. 압축 해제 후 해제된 폴더명(`instantclient_<버전>.zip`)의 버전을 잘 기억하고 압축 해제된 폴더의 내용을 하나의 폴더로 합칩니다.
        - 현재 제가 받은 버전은 `19_3` 입니다.
        
            ![-](/assets/웹해킹/SQL-Injection/img-0014.png)
        
        - 압축해제된 세개의 폴더의 내용을 하나의 폴더로 합치기

            - 각각 압축 해제된 모습
                ![-](/assets/웹해킹/SQL-Injection/img-0015.png)
            
            - 압축 해제된 3개의 폴더를 하나의 폴더로 옮기기
                
                ![-](/assets/웹해킹/SQL-Injection/img-0016.png)
                ![-](/assets/웹해킹/SQL-Injection/img-0017.png)

    3. 경로 `/usr/local` 에 `oracle` 디렉터리를 생성
        - 생성 명령어
            - `$ mkdir /usr/local/oracle`
                - 'Permission denied' 메시지가 나온 경우 `$ sudo mkdir /usr/local/oracle` 명령어 사용

    4. 생성한 디렉터리(`/usr/local/oracle`)에 방금 전 압축 해제 후 한곳에 모아둔 폴더를 옮겨준다.
        - 단, 옮길 폴더 즉, 한곳에 모아둔 폴더의 폴더명은 2번에서 기억해 둔 `instantclient_<버전>` 으로 한다.

        - 폴더를 옮기는 명령어
            - `$ mv instantclient_<버전명> /usr/local/oracle`
                - 저의 경우는 19.3 버전이므로 `$ mv instantclient_19_3 /usr/local/oracle` 명령어를 입력했습니다.

    5. 그다음 아래의 명령어를 통해 심볼릭 링크를 잡아줍니다.
        - 자신이 다운로드 받은 버전을 잘 확인하세요.
        - 명령어
            
            ```shell
            $ ln -sf /usr/local/oracle/instantclient_<버전 명>/sdk/include/*.h /usr/local/include/
            $ ln -sf /usr/local/oracle/instantclient_<버전 명>/sqlplus /usr/local/bin/
            $ ln -sf /usr/local/oracle/instantclient_<버전 명>/*.dylib /usr/local/lib/
            $ ln -sf /usr/local/oracle/instantclient_<버전 명>/*.dylib.11.1 /usr/local/lib/
            $ ln -sf /usr/local/oracle/instantclient_<버전 명>/libclntsh.dylib.11.1 /usr/local/lib/libclntsh.dylib
            ```
            
            - 명령어 실행 화면
                
                ![-](/assets/웹해킹/SQL-Injection/img-0018.png)


    7. 환경변수 등록
        - `~/.bash_profile`을 텍스트 편집기를 이용해서 열어준 후 아래의 내용을 붙여넣기 후 저장
            
            ```txt
            # Oracle
            export ORACLE_HOME="/usr/local/oracle/instantclient_19_3"
            export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME
            export DYLD_LIBRARY_PATH=$ORACLE_HOME/lib
            export TNS_ADMIN=$ORACLE_HOME/admin
            export SQLPATH=$ORACLE_HOME/sqlplus
            export PATH=$ORACLE_HOME/bin:$PATH
            ```
            
            - ORACLE 버전은 아까 전 4번에서 얘기한 Oracle 사이트에서 다운받은 압축파일 해제시 나오는 버전명
        
        - 이후 아래의 명령을 통해 적용 시켜준다.
            - `$ source ~/.bash_profile`


- MAMP + Oracle 연동
    - *Oracle은 Docker를 이용해서 설치 했으므로 사용 시 Docker에서 Oracle이 실행 중 인지 확인 필수*

    1. php.ini 수정(MAMP에서 현재 실행중인 php 버전의 php.ini를 수정하셔야 합니다.)
        - MAMP의 현재 설정된 php.ini의 경로 구하는 방법
            - [02.환경설정 MAC OS MAMP + ORACLE 설치](/contents/02.SQL-Injection/03.환경설정-MAC-OS-MAMP-ORACLE.md) 에서 찾아보시면 됩니다.
            

        - php.ini 하단에 아래의 내용을 기입 후 저장
            
            ```ini
            ; ORACLE
            extension=oci8.so
            ```
        
        - php.ini 아래의 옵션을 찾아서 On으로 변경(혹여나 에러가 나올 경우 표시를 위함)

            ```ini
            display_errors = On
            ```
    
    2. OCI8 설치
        - OCI8 이란?
            - PECL(PHP Extension Community Libary) 즉, PHP 확장 저장소 시스템에서 ORACLE 데이터베이스용 Extension이다.
                - 참고 URL
                    - [PECL 공식 홈페이지](https://pecl.php.net/package/oci8)
        
        - pecl을 이용해서 OCI8 설치
            - pecl 명령어 실행을 위해 MAMP에서 설정된 PHP 버전의 경로로 이동 후 bin 폴더로 이동합니다.
                - MAMP에 설정된 PHP 버전 확인하기
                    - MAMP의 환경설정을 열고 PHP 탭을 들어가면 아래처럼 현재 선택된 PHP 버전을 확인할 수 있습니다.
            
                        ![-](/assets/웹해킹/SQL-Injection/img-0019.png)
                
                - pecl 명령어가 존재하는 경로 이동
                    - `$ cd /Applications/MAMP/bin/php/php<PHP 버전>/bin`
                
            - 이후 OCI8 설치를 위해 아래의 명령어 입력
                - `$ ./pecl install oci8`
            
            - 설치 중간에 'if you're compiling with Oracle Instant Client [autodetect] :'  문구가 나오면 `instantclient,/usr/local/oracle/instantclient_<버전>`라고 입력 후 엔터
                - 버전은 위에 `oci8 추가를 위한 Oracle Client Instant 설치` 설명에서 Oracle Client Instant 의 버전으로 설치한 폴더명

    3. Oracle과 MAMP 연동이 됐는지 확인하기

        - MAMP 를 재시작한다. (아파치를 재시작해야지 php.ini 설정 및 oci8이 적용되므로)
        
        - MAMP에서 설정한 웹 루트 경로에 아래의 코드를 작성하고 저장

            ```php
           <?php

            // Connects to the XE service (i.e. database) on the "localhost" machine
            $conn = oci_connect('<사용자 계정>', '<사용자 패스워드>', 'localhost/XE');
            if (!$conn) {
                $e = oci_error();
                trigger_error(htmlentities($e['message'], ENT_QUOTES), E_USER_ERROR);
            }

            $stid = oci_parse($conn, 'SELECT USER FROM dual');
            oci_execute($stid);

            echo "<table border='1'>\n";
            while ($row = oci_fetch_array($stid, OCI_ASSOC+OCI_RETURN_NULLS)) {
                echo "<tr>\n";
                foreach ($row as $item) {
                    echo "    <td>" . ($item !== null ? htmlentities($item, ENT_QUOTES) : "&nbsp;") . "</td>\n";
                }
                echo "</tr>\n";
            }
            echo "</table>\n";

            ?>
            ```

        - 위의 코드를 저장한 파일을 브라우저로 실행 시 아래처럼 등장해야 성공

            ![-](/assets/웹해킹/SQL-Injection/img-0020.png)

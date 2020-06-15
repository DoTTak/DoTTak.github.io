---
layout: post
title: "[웹해킹/SQL Injection] 04 - 환경설정 MAC OS MAMP + MSSQL 설치"
date: 2020-06-10 22:28:50 +0900
categories: 
    - 웹해킹
    - 설치가이드
tags:
    - 웹해킹
    - SQL Injection
    - MAMP
    - MSSQL
toc: true
notice: "> 본 글은 [[인프런] 크리핵티브](https://www.inflearn.com/instructors/213605/courses)님의 [모의해킹 실무자가 알려주는, SQL Injection 공격 기법과 시큐어 코딩 : PART 1](https://www.inflearn.com/course/sql-injection-secure-coding-1) 강의를 듣고 정리한 글 입니다.\n
> - 본 강의는 **유료 강의**입니다. 이에, 강의 내용에 **모르는 키워드를 중심으로 정리한 내용**이고, 또한 해당 강의를 듣고 저의 개인적인 학습 목표, 느낌을 기반으로 정리할 것 입니다. 이점 참고 부탁드립니다.\n
> - 참고 URL\n
>   - [위키백과](https://ko.wikipedia.org/wiki/)\n
>   - [Microsoft - 빠른 시작: Docker에서 SQL Server 컨테이너 이미지 실행](https://docs.microsoft.com/ko-kr/sql/linux/quickstart-install-connect-docker?view=sql-server-2017&pivots=cs1-bash)"

---

## 01. 맥 OS에 MAMP + MSSQL 연동

### 01-1 사전준비
- MAMP 설치
    - MAMP 설치 방법은 [02.환경설정 MAC OS APM(MAMP) 설치](/contents/02.SQL-Injection/02.환경설정-MAC-OS-APM.md)를 참고해주세요.

### 01-2 MAMP + MSSQL 연동
- 도커 + MSSQL 설치과정
    1. 도커 설치를 위해 [Docker 다운로드](https://www.docker.com/products/docker-desktop) 를 클릭 후 docker를 설치해준다.

    2. 도커 설치 완료 후 상단바에 고래모양의 도커를 클릭해서 로그인을 해준다.(계정이 없으면 회원가입 필수)

        ![-](/assets/웹해킹/SQL-Injection/img-0010.png)

    3. Docker를 사용해서 `SQL Server 2017 Linux 컨테이너`(MSSQL) 이미지를 가져온다.
        - `$ docker pull mcr.microsoft.com/mssql/server:2017-latest`
    
    4. MSSQL 컨테이너 실행
        - 아래의 명령어를 실행

            ```shell
            $ docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong@Passw0rd>" \
                -p 1433:1433 --name sql1 \
                -d \
            mcr.microsoft.com/mssql/server:2017-latest
            ```
    
    5. MSSQL이 돌아가는지 확인하기
        - `$ docker ps -a`

            ```shell
            CONTAINER ID IMAGE                                        COMMAND                  CREATED             STATUS              PORTS                                            NAMES
            dedb0669a9b6 mcr.microsoft.com/mssql/server:2017-latest   "/opt/mssql/bin/nonr…"   4 seconds ago       Up 3 seconds        0.0.0.0:1433->1433/tcp                           sql1
            ```
    
    6. SA 암호 변경
        - 아래의 명령문 실행
            - `$ docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourStrong@Passw0rd>"`

        - 비밀번호 변경

            ```
            1> ALTER LOGIN SA WITH PASSWORD="<새로운 비밀번호>"       -- 입력후 엔터 
            2> GO   -- 입력 후 엔터
            ```

        - 변경된 비밀번호로 접속되는지 확인
            - `$ docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<새로운 비밀번호>"`

- MAMP + MSSQL 연동
    - pecl을 이용해서 MSSQL 드라이버(`sqlsrv`, `pdo_sqlsrv`) 설치
        - mssql이 아닌 sqlsrv 드라이버를 설치하는 이유는 ??
            - mssql 드라이버는 커뮤니티 기반으로 만들어진 드라이버
            - sqlsrv(SQL Server Dirver for PHP) 는 MS에서 공식적으로 지원하는 드라이버
            - PHP 7.0 이후부터는 sqlsrv만을 지원
        - pecl 명령어 실행을 위해 MAMP에서 설정된 PHP 버전의 경로로 이동 후 bin 폴더로 이동합니다.
            - MAMP에 설정된 PHP 버전 확인하기
                - MAMP의 환경설정을 열고 PHP 탭을 들어가면 아래처럼 현재 선택된 PHP 버전을 확인할 수 있습니다.
        
                    ![-](/assets/웹해킹/SQL-Injection/img-0019.png)
            
            - pecl 명령어가 존재하는 경로 이동
                - `$ cd /Applications/MAMP/bin/php/php<PHP 버전>/bin`
            
        - 이후 MSSQL 드라이버(`sqlsrv`, `pdo_sqlsrv`) 설치를 위해 아래의 명령어 입력
            - `$ ./pecl install sqlsrv pdo_sqlsrv`

            - 만일, 아래의 에러가 나올 경우 `$ brew install unixodbc` 명령으로 `unixODBC`을 설치 하고 명령어를 다시 실행하면 된다.
                - 에러

                    ```
                    #include <sql.h>
                            ^~~~~~~
                    1 error generated.
                    make: *** [conn.lo] Error 1
                    ERROR: `make' failed
                    ```
                
                - *brew 설치 필수*
        
        - ODBC를 설치를 위해 아래의 명령어를 순서대로 입력
            - ODBC란?
                - 데이터베이스 접근을 위한 인터페이스
            
            - 명령어

                ```shell
                $ brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
                $ brew update
                $ brew install msodbcsql mssql-tools
                ```

        - MAMP가 실행중인 php 버전의 php.ini 를 열어서 아래의 복사해서 맨 하단에 삽입

            ```
            ; MSSQL
            extension=sqlsrv.so
            extension=pdo_sqlsrv.so
            ```
        
        - 이후 MAMP 재시작

        - MAMP + MSSQL이 잘 연동됐는지 확인을 위해 아래의 PHP 코드를 저장해서 웹 브라우저로 열어서 확인

            - 코드
                
                ```php
                <?php
                $serverName = "127.0.0.1";
                $connectionOptions = array(
                    "database" => "master",
                    "uid" => "sa",
                    "pwd" => "<변경한 비밀번호>"
                );

                // Establishes the connection
                $conn = sqlsrv_connect($serverName, $connectionOptions);
                if ($conn === false) {
                    die(formatErrors(sqlsrv_errors()));
                }

                // Select Query
                $tsql = "SELECT @@Version AS SQL_VERSION";

                // Executes the query
                $stmt = sqlsrv_query($conn, $tsql);

                // Error handling
                if ($stmt === false) {
                    die(formatErrors(sqlsrv_errors()));
                }
                ?>

                <h1> Results : </h1>

                <?php
                while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
                    echo $row['SQL_VERSION'] . PHP_EOL;
                }

                sqlsrv_free_stmt($stmt);
                sqlsrv_close($conn);

                function formatErrors($errors)
                {
                    // Display errors
                    echo "Error information: <br/>";
                    foreach ($errors as $error) {
                        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
                        echo "Code: ". $error['code'] . "<br/>";
                        echo "Message: ". $error['message'] . "<br/>";
                    }
                }
                ?>
                ```

        - 위의 코드를 저장한 파일을 브라우저로 실행 시 아래처럼 등장해야 성공

           ![-](/assets/웹해킹/SQL-Injection/img-0021.png)

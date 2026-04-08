---
title: "Getting_Started_With_Vertica"
date: 2026-04-08 16:46:50 +0900
categories: [Vertica, Handson]
tags: [vertica, vsql, jdbc]
---

# 1. admintools

## 1. admintools 란?

- Vertica Database Cluster를 관리하기 위한 공식 관리 도구 입니다.
- Admintools 는 python 기반 코드로 작성되었습니다.
- Admintools 는 ssh-passwordless 방식의 Cluster 구성되어 있기 때문에, dbadmin 유저가 어느 노드에서 작업을 하던 실행 가능합니다.

## 2. admintools 문법

```bash
# admintools 경로
/opt/vertica/bin/admintools

# /opt/vertica/sbin/install_vertica 로 클러스터 구성하면 
# 자동으로 path 설정되어 dbadmin 접속 후 admintools 커맨드로 실행 가능합니다.
admintools --help 

# admintools 세부내용 확인
admintools -a

# admintools -t 에 대한 도움말 확인하고 싶을 경우
admintools -t start_db --help
```

### ✏️ 주로 사용하는 옵션 소개 ( -t , - -tool 세부 옵션 )

### 1. create_db : Database 생성

```bash
# 기본 문법
admintools -t create_db -s <hostname> -d <db_name> -p <password> -c <catalog_path> -D <data_path>

# 예시
admintools -t create_db -s vnode01,vnode02,vnode03 -d vmart -p 123456 -c /home/dbadmin -D /home/dbadmin
```

| 옵션 | 설명 | 예시 |
| --- | --- | --- |
| -s | - -hosts | 호스트명 입력 | 예시 → vnode01,vnode02,vnode03 |
| -d | - -database | Database 이름 지정 | 예시 →  vmart |
| -p | - -password | DB 패스워드 지정 | 예시 → ‘123456’ |
| -c | - -catalog_path | Catalog 경로 지정 | 기본값 → /home/dbadmin |
| -D | - -data_path | Data 경로 지정 | 기본값 → /home/dbadmin |
| -l |- -license | 라이선스 등록 | 절대 경로로 지정 |

![clipboardImage_25_1210_133040_692.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_133040_692.jpeg)

### 2. list_allnodes : Node 상태 확인

```bash
# 기본 문법
admintools -t list_allnodes
```

![image.png](/assets/img/posts/getting-started-vertica/image.png)

### 3. start_db : Database 시작

```bash
# 기본 문법
admintools -t start_db -d <db_name> -p <password>
```

| 옵션 | 설명 | 예시 |
| --- | --- | --- |
| -d | - -database | Database 이름 지정 | 예시 →  vmart |
| -p | - -password | DB 패스워드 지정 | 예시 → ‘123456’ |

![image.png](/assets/img/posts/getting-started-vertica/image-1.png)

### 4. stop_db : Database 중지

```bash
# 기본 문법
admintools -t stop_db -d <db_name> -p <password>
```

| 옵션 | 설명 | 예시 |
| --- | --- | --- |
| -d | - -database | Database 이름 지정 | 예시 →  vmart |
| -p | - -password | DB 패스워드 지정 | 예시 → ‘123456’ |

Enterprise Mode 에서 stop_db 실행시 (세션에 아무도 없을 경우)

![image.png](/assets/img/posts/getting-started-vertica/image-2.png)

세션에 user가 남아 있을 경우 stop 되지 않습니다 ( - -force 혹은 -F 옵션으로 강제 종료 )

![image.png](/assets/img/posts/getting-started-vertica/image-3.png)

(참고) Eon Mode 에서 stop_db 실행시

![image.png](/assets/img/posts/getting-started-vertica/image-4.png)

### 5. stop_node : Node 중지

```bash
# 기본 문법
admintools -t stop_node -s <hostname or ip>
```

![clipboardImage_25_1210_170633_511.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_170633_511.jpeg)

### 6. restart_node : Node 재시작

```bash
# 기본 문법
admintools -t restart_node -s <hostname or ip> -d <db_name>
```

![clipboardImage_25_1210_170832_895.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_170832_895.jpeg)

![clipboardImage_25_1210_170906_599.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_170906_599.jpeg)

### 7. view_cluster : 클러스터 상태 확인

```bash
# 기본 문법
admintools -t view_cluster
```

![image.png](/assets/img/posts/getting-started-vertica/image-5.png)

※ admintools 에 관한 도움말은 -h 혹은 - -help 를 이용

![image.png](/assets/img/posts/getting-started-vertica/image-6.png)

## 3. admintools GUI

### 1. GUI 환경에서 Vertica 시작

1. Main Menu → 3. Start Database

![clipboardImage_25_1210_171349_884.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171349_884.jpeg)

1. Select database to Start

![clipboardImage_25_1210_171412_284.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171412_284.jpeg)

1. Password 입력

![clipboardImage_25_1210_171729_880.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171729_880.jpeg)

1. 확인

![clipboardImage_25_1210_171815_023.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171815_023.jpeg)

### 2. GUI 환경에서 Vertica 중지

1. Main Menu → 4. Stop Database

![clipboardImage_25_1210_171110_678.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171110_678.jpeg)

1. Select database to stop

![clipboardImage_25_1210_171124_073.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171124_073.jpeg)

1. Password 입력

![clipboardImage_25_1210_171212_071.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171212_071.jpeg)

1. Complete

![clipboardImage_25_1210_171232_344.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171232_344.jpeg)

1. 확인

![clipboardImage_25_1210_171247_562.jpeg](/assets/img/posts/getting-started-vertica/clipboardImage_25_1210_171247_562.jpeg)

### 3. GUI 환경에서 Node 중지

1. Main Menu → 7. Advanced Menu
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-7.png)
    
2. Kill Vertica Process on Host
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-8.png)
    
3. Select host(s)
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-9.png)
    
4. 확인
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-10.png)
    
5. Node 중지 여부 확인 ( Main Menu → 1. view Database Cluster State )
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-11.png)
    

### 4. GUI 환경에서 Node 재시작

1. Main Menu → 5. Restart Vertica on Host
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-12.png)
    
2. Select database
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-13.png)
    
3. Select host(s) to restart
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-14.png)
    
4. Password 입력
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-15.png)
    

## 4. admintools .conf

1. admintools.conf 역할
    - 클러스터 구성에 필요한 정보들이 기록되어 있는 config 파일
    - 경로 : /opt/vertica/config/admintools.conf
2. 코드설명
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-16.png)
    

## 5. adminTools.log

1. admintools 실행 시 발생하는 이벤트에 대한 로그를 기록
2. log 경로
    
    ```bash
    # log 경로
    /opt/vertica/log/adminTools.log
    ```
    

# 2. vsql

## 1. vsql 이란?

- vsql 은 Vertica 데이터베이스의 공식 CLI 로, PostgreSQL 의 psql 과 유사한 인터페이스를 제공하고 있습니다.
- 메타 명령어를 통해 데이터베이스 스키마 탐색, 테이블 관리, 세션 설정 등을 수행할 수 있습니다.

## 2. Meta Command

- 백슬래시(\) 로 시작하는 vsql 클라이언트 전용 명령어
- SQL이 아니라 vsql 자체가 처리하는 관리/편의 명령으로, 테이블 구조 조회, 출력 형식 변경등에 사용됩니다.
- 메타 커맨드 특징
    - 백슬래시 시작 : ex → \d , \x , \q , \i 등등
    - SQL 과 혼용 사용 : 한줄에 SQL + 메타 커맨드 가능 ( ex → SELECT * FROM T; \q )
- 커맨드 종류
    1. \d  (테이블 구조 확인)
        
        ![image.png](/assets/img/posts/getting-started-vertica/image-17.png)
        
    2. \x (출력 형식을 확장 모드로 전환)
        - 기본은 가로방향 테이블, \x 로 세로방향 테이블로 전환 가능
        
        (비교) 가로 형식
        
        ![image.png](/assets/img/posts/getting-started-vertica/image-18.png)
        
        (비교) 세로 형식 (Expanded display is on)
        
        ![image.png](/assets/img/posts/getting-started-vertica/image-19.png)
        
    3. \q ( vsql 빠져나오기 )
        
        ![image.png](/assets/img/posts/getting-started-vertica/image-20.png)
        
    4. \i ( 외부 script 실행하기 )
        
        ![image.png](/assets/img/posts/getting-started-vertica/image-21.png)
        
        ![image.png](/assets/img/posts/getting-started-vertica/image-22.png)
        

# 3. DB Client Integration (dbeaver)

## 1. DB Client 개요

데이터 베이스 관리의 핵심 도구로, SQL 실행과 데이터 관리를 지원합니다.

🔍 주요 특징

- DBMS 호환성 : Vertica, MySQL, PostgreSQL, Oracle 등 다양한 데이터베이스 서버와 연결 가능하며, 멀티 DBMS 환경에서 유연하게 작동합니다.
- SQL 쿼리 실행 : GUI 또는 CLI 를 통해 쿼리 작성, 실행, 결과 분석을 지원해 개발과 관리를 간편화 합니다.

## 2. dbeaver 소개

DBeaver 는 개발자, DBA, 데이터 분석가를 위한 무료 오픈소스(Apache 2.0 라이선스) 데이터베이스 클라이언트로, Java 와 Eclipse 기반의 크로스플랫폼 도구입니다.

dbeaver 구성

![image.png](/assets/img/posts/getting-started-vertica/image-23.png)

1. 서버 목록 : 
    - Client 에 연결정보를 입력하여 연결했었던 DB 목록이 노출 됩니다. Vertica 뿐 아니라 다양한 DB와 연결이 가능합니다.
2. 쿼리 작성 부분 : 
    - 이곳에 쿼리를 작성하여 실행을 하면 4번의 쿼리 결과 부분에 실행 결과가 노출 됩니다.
3. Script 목록 : 
    - 작업하면서 저장했었던 SQL 편집기들을 확인할 수 있습니다. 2번 쿼리 작성 부분에서 해당 내용을 종료하였어도 다시 열어볼 수 있습니다.
4. 쿼리 결과 부분 : 
    - 쿼리 결과를 확인 할 수 있습니다. 그리드 형식과 텍스트 형식으로 확인할 수 있습니다.

## 3. JDBC Driver

1. JDBC (Java DataBase Connectivity) Driver 란?
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-24.png)
    
    - 특정 데이터베이스와 통신할 수 있게 해주는 “연결 전용 라이브러리”
    - JDBC 드라이버를 통해 자바 코드가 보낸 SQL 설정과 정보를 실제 DB 프로토콜로 변환하고 결과를 다시 자바 객체 형태로 돌려줍니다.
    - JDBC 드라이버는 데이터베이스 접근의 표준화를 위해서 탄생한 API
    
2. vertica-jdbc-24.2.0-1.jar 다운로드
    - [https://www.vertica.com/download/vertica/client-drivers/](https://www.vertica.com/download/vertica/client-drivers/)
    - 위 링크를 통해 jar 파일 download 제공, 고객 폐쇄망의 경우 온라인에서 자동으로 검색하여 jar 파일을 등록할 수 없기때문에 직접 download 하여 반입
    
    ![image.png](/assets/img/posts/getting-started-vertica/image-25.png)
    

## 4. 연동 방법

1. DBeaver 기동 후 → 새 데이터베이스 연결

![image.png](/assets/img/posts/getting-started-vertica/image-26.png)

![image.png](/assets/img/posts/getting-started-vertica/image-27.png)

1. Main 탭에 내용 입력
    - Host : 구성한 IP 입력
    - Port : 기본포트 5433 (고객사 필요시 변경했다면 이부분 수정)
    - Database/Schema : Database 이름
    - Username : 첫 접속은 superuser 인 dbadmin 입력
    - Password : 지정한 패스워드 입력

![image.png](/assets/img/posts/getting-started-vertica/image-28.png)

1. Driver Settings → Libraries → Add File → jar 파일 경로 지정

![image.png](/assets/img/posts/getting-started-vertica/image-29.png)

1. Test connection → Connected 확인

![image.png](/assets/img/posts/getting-started-vertica/image-30.png)
# 게시판 설명문서

## 1. 개요
이 문서는 게시판 프로젝트의 구조와 기능을 설명합니다. 이 프로젝트는 사용자 관리, 게시글 관리, 댓글 관리, 이메일 인증, 파일 첨부 기능을 제공하는 웹 애플리케이션입니다.

## 2. 데이터베이스 설계
- **Users 테이블**: 사용자 정보를 저장합니다. (`user_id`, `username`, `password`, `email`, `created_at`, `confirmed`, `confirmation_token`)
- **Posts 테이블**: 게시글 정보를 저장합니다. (`post_id`, `user_id`, `title`, `content`, `created_at`, `updated_at`, `readcount`, `likes`, `file_uuid`, `file_type`, `originalFileName`)
- **Comments 테이블**: 댓글 정보를 저장합니다. (`comment_id`, `post_id`, `user_id`, `content`, `created_at`)

## 3. 주요 기능
### 3.1 사용자 관리
- **사용자 등록**: 새로운 사용자를 등록할 수 있습니다.
- **로그인**: 사용자 이름과 비밀번호를 통해 로그인할 수 있습니다.
- **아이디 중복 체크**: 사용자 이름의 중복 여부를 확인할 수 있습니다.
- **이메일 인증**: 회원가입 시 이메일 인증을 통해 사용자의 이메일 주소를 확인합니다.

### 3.2 게시글 관리
- **게시글 목록 조회**: 게시글 목록을 조회할 수 있습니다.
- **게시글 등록**: 새로운 게시글을 등록할 수 있습니다.
- **게시글 조회**: 특정 게시글의 상세 정보를 조회할 수 있습니다.
- **게시글 수정**: 게시글의 제목과 내용을 수정할 수 있습니다.
- **게시글 삭제**: 게시글을 삭제할 수 있습니다.
- **게시글 검색**: 제목 또는 작성자로 게시글을 검색할 수 있습니다.
- **게시글 추천**: 게시글에 대한 추천을 할 수 있습니다.
- **조회수 증가**: 게시글을 조회할 때마다 조회수가 증가합니다.
- **페이지네이션**: 게시글 목록을 페이지 단위로 나누어 조회할 수 있습니다.
- **파일 첨부**: 게시글 작성 시 파일을 첨부할 수 있습니다.

### 3.3 댓글 관리
- **댓글 목록 조회**: 특정 게시글의 댓글 목록을 조회할 수 있습니다.
- **댓글 등록**: 게시글에 새로운 댓글을 등록할 수 있습니다.
- **댓글 수정**: 댓글의 내용을 수정할 수 있습니다.
- **댓글 삭제**: 댓글을 삭제할 수 있습니다.

## 4. 화면 구성
### 4.1 메인 페이지 (`list.jsp`)
- 로그인/로그아웃 버튼
- 회원가입 버튼
- 게시글 목록 테이블 (번호, 제목, 작성자, 작성일, 조회수, 추천수)
- 페이지네이션
- 검색 폼 (검색 유형, 검색어 입력)
- 글쓰기 버튼

### 4.2 게시글 상세 페이지 (`detail.jsp`)
- 게시글 제목
- 작성자 정보 (아이콘, 작성자명)
- 작성일
- 게시글 내용
- 첨부 파일 다운로드 링크 (파일이 첨부된 경우)
- 추천 버튼 및 추천수
- 수정/삭제 버튼 (작성자에게만 표시)
- 목록 버튼
- 댓글 목록
- 댓글 작성 폼 (로그인한 사용자에게만 표시)

### 4.3 게시글 작성/수정 페이지 (`write.jsp`, `detail.jsp`의 수정 모드)
- 제목 입력 필드
- 내용 입력 필드 (CKEditor 사용)
- 파일 첨부 필드
- 등록/수정 버튼
- 취소 버튼 (수정 모드에서만 표시)

### 4.4 로그인 페이지 (`login.jsp`)
- 아이디 입력 필드
- 비밀번호 입력 필드
- 로그인 버튼

### 4.5 회원가입 페이지 (`register.jsp`)
- 아이디 입력 필드
- 비밀번호 입력 필드
- 이메일 입력 필드
- 회원가입 버튼

## 5. 사용된 라이브러리 및 기술
- Java 8
- Spring Framework 5.0.7
- MyBatis 3.5.2
- Oracle Database
- Maven
- Lombok
- Log4j
- JUnit 4
- Bootstrap 5.3.3
- Font Awesome 5.15.4
- CKEditor 4.16.1
- JavaMail

## 6. 프로젝트 구조
- `org.zerock.controller`: 컨트롤러 클래스가 위치합니다.
- `org.zerock.service`: 서비스 인터페이스와 구현 클래스가 위치합니다.
- `org.zerock.mapper`: MyBatis 매퍼 인터페이스가 위치합니다.
- `org.zerock.domain`: VO(Value Object) 클래스가 위치합니다.
- `src/main/webapp/WEB-INF/views`: JSP 파일이 위치합니다.
- `src/main/webapp/resources`: CSS, JavaScript, 이미지 등의 정적 리소스 파일이 위치합니다.

## 7. 주요 흐름
### 7.1 사용자 등록 및 로그인
- 회원가입 페이지에서 사용자 정보를 입력하고 등록합니다.
- 회원가입 시 입력한 이메일 주소로 인증 이메일이 발송됩니다.
- 사용자는 이메일의 인증 링크를 클릭하여 이메일 인증을 완료합니다.
- 로그인 페이지에서 등록된 사용자 정보로 로그인합니다.
- 로그인 성공 시 세션에 사용자 정보를 저장하고, 게시글 목록 페이지로 이동합니다.

### 7.2 게시글 등록 및 조회
- 로그인한 사용자는 글쓰기 버튼을 클릭하여 게시글 작성 페이지로 이동합니다.
- 게시글 작성 페이지에서 제목, 내용을 입력하고 파일을 첨부한 후 등록 버튼을 클릭하여 게시글을 등록합니다.
- 게시글 목록 페이지에서 등록된 게시글을 확인할 수 있습니다.
- 게시글 제목을 클릭하면 해당 게시글의 상세 페이지로 이동합니다.

### 7.3 게시글 수정 및 삭제
- 게시글 상세 페이지에서 작성자는 수정 버튼을 클릭하여 게시글 수정 모드로 전환합니다.
- 수정 모드에서 제목, 내용, 첨부 파일을 수정하고 수정 버튼을 클릭하여 게시글을 수정합니다.
- 작성자는 삭제 버튼을 클릭하여 게시글과 첨부된 파일을 삭제할 수 있습니다.

### 7.4 댓글 등록 및 조회
- 로그인한 사용자는 게시글 상세 페이지 하단의 댓글 작성 폼에서 댓글을 작성하고 등록 버튼을 클릭하여 댓글을 등록합니다.
- 등록된 댓글은 게시글 상세 페이지에서 확인할 수 있습니다.

### 7.5 댓글 수정 및 삭제
- 댓글 작성자는 자신의 댓글에 대해 수정 및 삭제 버튼이 표시됩니다.
- 수정 버튼을 클릭하면 댓글 수정 모드로 전환되며, 내용을 수정하고 수정 버튼을 클릭하여 댓글을 수정합니다.
- 삭제 버튼을 클릭하면 해당 댓글이 삭제됩니다.

## 8. 에러 처리 및 예외 상황
- 로그인 실패 시 모달창을 통해 에러 메시지를 표시합니다.
- 권한이 없는 사용자가 게시글이나 댓글의 수정/삭제를 시도할 경우 모달창을 통해 경고 메시지를 표시합니다.
- 예기치 않은 에러 발생 시 적절한 에러 페이지를 표시하고, 로그를 기록합니다.
- 파일 업로드 및 삭제 시 발생할 수 있는 예외 상황을 처리합니다.

이 게시판 프로젝트는 사용자 관리, 게시글 관리, 댓글 관리, 이메일 인증, 파일 첨부 기능을 제공하며, Spring Framework와 MyBatis를 사용하여 구현되었습니다. 프론트엔드는 JSP와 Bootstrap을 활용하여 구성되었으며, 데이터베이스로는 Oracle Database를 사용하고 있습니다. 또한 CKEditor를 통해 게시글 작성 시 편리한 텍스트 편집 기능을 제공하며, JavaMail을 사용하여 이메일 인증 기능을 구현하였습니다.
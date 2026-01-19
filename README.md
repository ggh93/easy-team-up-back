# Easy Team Up - Backend

팀 협업용 실시간 칸반 보드 백엔드 API

## 기술 스택

- **Framework**: NestJS
- **Database**: PostgreSQL
- **ORM**: TypeORM
- **Authentication**: JWT (Passport)
- **Language**: TypeScript

## 주요 기능

### 인증 (Auth)

- ✅ 회원가입
- ✅ 초대 링크를 통한 회원가입
- ✅ 로그인
- ✅ JWT 기반 인증

### 팀 관리 (Teams)

- ✅ 팀 생성
- ✅ 팀 목록 조회
- ✅ 초대 코드 생성/재생성
- ✅ 초대 코드로 팀 참여
- ✅ 팀 멤버 관리 (추가/제거/권한 변경)

## 설치 및 실행

### 1. 의존성 설치

```bash
npm install
```

### 2. 환경 변수 설정

`.env.example` 파일을 `.env`로 복사하고 값을 설정합니다:

```bash
cp .env.example .env
```

`.env` 파일 수정:

```env
PORT=3000
NODE_ENV=development

DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=your_password
DB_DATABASE=easy_team_up

JWT_SECRET=your-super-secret-jwt-key-change-this
JWT_EXPIRATION=7d
```

### 3. PostgreSQL 데이터베이스 생성

```bash
# PostgreSQL 접속
psql -U postgres

# 데이터베이스 생성
CREATE DATABASE easy_team_up;

# 종료
\q
```

### 4. 서버 실행

```bash
# 개발 모드
npm run start:dev

# 프로덕션 빌드
npm run build
npm run start:prod
```

서버가 실행되면: `http://localhost:3000`

## 데이터베이스 스키마

### Users

- id (UUID, PK)
- email (string, unique)
- password (string, hashed)
- username (string)
- profileImage (string, nullable)
- isActive (boolean)
- createdAt (timestamp)
- updatedAt (timestamp)

### Teams

- id (UUID, PK)
- name (string)
- description (text, nullable)
- ownerId (UUID, FK → Users)
- inviteCode (string, unique)
- isPublic (boolean)
- createdAt (timestamp)
- updatedAt (timestamp)

### TeamMembers

- id (UUID, PK)
- teamId (UUID, FK → Teams)
- userId (UUID, FK → Users)
- role (enum: owner, admin, member)
- joinedAt (timestamp)

## 권한 시스템

- **OWNER**: 팀 생성자, 모든 권한
- **ADMIN**: 멤버 관리, 초대 코드 생성
- **MEMBER**: 일반 멤버

## 개발 계획

- [ ] 보드(Board) 기능
- [ ] 리스트(List) 기능
- [ ] 카드(Card) 기능
- [ ] 실시간 동기화 (Socket.io)
- [ ] 댓글 기능
- [ ] 파일 첨부 기능

## 라이센스

MIT

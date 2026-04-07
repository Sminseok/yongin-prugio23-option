# 세대 옵션 조회 웹앱

엑셀 `옵션현황` 시트를 기반으로 세대별 옵션을 조회하는 배포용 Flask 웹앱입니다.

## 포함 기능
- 동 / 호수 조회
- 빠른 검색 (`2002-201`, `2002201`)
- 모바일 반응형 UI
- 관리자 로그인
- 관리자 엑셀 업로드로 전체 데이터 갱신
- 업로드 이력 관리
- SQLite 저장

## 폴더 구조
```bash
option_webapp/
├─ app.py
├─ data.db              # 최초 실행 시 생성 또는 seed.xlsx로 초기화
├─ seed.xlsx            # 최초 데이터 시드 파일
├─ requirements.txt
├─ .env.example
├─ uploads/
├─ static/
│  └─ style.css
└─ templates/
   ├─ base.html
   ├─ index.html
   ├─ admin.html
   └─ admin_login.html
```

## 실행 방법
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

환경변수 설정:
```bash
export SECRET_KEY="your-secret-key"
export ADMIN_PASSWORD="change-this-password"
export PORT=5000
```

실행:
```bash
python app.py
```

브라우저:
- 조회 화면: `http://localhost:5000`
- 관리자 화면: `http://localhost:5000/admin`

## 엑셀 업로드 규칙
- 파일 형식: `.xlsx`
- 필수 시트명: `옵션현황`
- 필수 컬럼:
  - 동, 층, 라인, 호수, 평형
  - 현관중문, 발코니확장, 쿡탑, 전기오븐, 식기세척기
  - 욕실 타일, 냉장고장, 욕실 복합환풍기, 붙박이장, 시스템에어컨
  - 시스템 청정환기, 조명특화, 84B 드레스룸, 복도벽, 벽지, 마루
  - 침실1 드레스룸, 침실1 드레스룸 제습기, 현관창고, 신발장
  - 주방벽, 상판, 주방수전, 주방 특화조명기구, 주방TV, 주방 팬트리
  - 주방가구, 샤워부스, 욕실 수전, 욕조 마감

## 운영 배포 예시
### Render
- New Web Service 생성
- Python 환경 선택
- Build Command: `pip install -r requirements.txt`
- Start Command: `gunicorn app:app`
- 환경변수에 `SECRET_KEY`, `ADMIN_PASSWORD` 등록

### Railway
- GitHub에 업로드 후 새 프로젝트 연결
- Start Command: `gunicorn app:app`
- 환경변수 등록

## 권장 개선 사항
- 관리자 계정 다중화
- 업로드 전 컬럼 매핑 화면
- 변경 이력 비교 기능
- 세대별 PDF 출력
- 사용자 접속 로그

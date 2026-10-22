# gg1th_rngd_lab

FuriosaAI **RNGD** NPU 실습 저장소입니다.
이 문서는 실습을 시작하기 전에 필요한 **환경 셋팅** 절차를 다룹니다.
https://furiosa.ai/rngd
https://developer.furiosa.ai/latest/en/get_started/furiosa_llm.html
---

## 1. 실습 환경

| 항목 | 버전 / 내용 |
|---|---|
| NPU | FuriosaAI RNGD |
| OS | Ubuntu 22.04 (Linux 6.8) |
| Python | 3.12 (`.python-version`) |
| 패키지 관리자 | [uv](https://docs.astral.sh/uv/) 0.13 이상 |
| furiosa-llm | v2026.4.0 |
| furiosa-smi | 2026.1.1 |

> `furiosa-llm`, `furiosa-smi`는 실습 서버에 시스템 전역으로 미리 설치되어 있습니다.
> (`/usr/local/bin/furiosa-llm`, `/usr/bin/furiosa-smi`)

### 1-1. Furiosa RNGD 위한 실습환경 구성
노션 문서 참고
```
https://app.notion.com/p/RNGD_SSH_uv_-fff1c1324de582768e6a81605dd5418a?source=copy_link
```
동일한 내용 저장되어 있음 : docs/RNGD_SSH_uv_init_.pdf

---

## 2. github 연결 및 저장소 clone
### 2-1. github 연결
노션문서 참고
```
https://app.notion.com/p/github-7141c1324de583b0a5de0110c6521d5b?source=copy_link
```
### 2-2. github 저장소 clone
```bash
cd ~
git clone git@github.com:magpia000/gg1th_rngd_lab.git rngd-lab
cd rngd-lab
```
---

## 3. Python 가상환경 구성
### 3-1. 가상환경 만들기
```
uv init --bare --python 3.12 --pin-python 
```

### 3-2. 의존성 설치
`pyproject.toml`과 `uv.lock`에 정의된 의존성으로 `.venv`를 생성합니다.

```bash
uv sync
```

설치되는 주요 패키지

| 패키지 | 용도 |
|---|---|
| `httpx`, `requests` | furiosa-llm API 서버 호출 |
| `numpy`, `pandas` | 결과 데이터 처리 |

### 3-3. 가상환경 활성화
선택 사항입니다. `uv run`을 쓰면 생략할 수 있습니다.

```bash
source .venv/bin/activate
```

---

## 4. 환경 확인

### 4-1. Python 환경

```bash
uv run python check_env.py
```

출력 예시

```
=== RNGD 실습환경 확인 ===
사용자: std2
홈 디렉터리: /home/std2
Python 버전: 3.12.x
Python 실행 경로: /home/std2/rngd-lab/.venv/bin/python
프로젝트 위치: /home/std2/rngd-lab
```

`Python 실행 경로`가 프로젝트의 `.venv`를 가리키는지 확인합니다.

### 4-2. NPU 장치

```bash
furiosa-smi info
```

```
+------+--------+-------------------+---------+---------+--------------+
| Arch | Device | Firmware          | Temp.   | Power   | PCI-BDF      |
+------+--------+-------------------+---------+---------+--------------+
| rngd | npu7   | 2026.4.0, 93d67f3 | 33.90°C | 38.00 W | 0000:c4:00.0 |
+------+--------+-------------------+---------+---------+--------------+
```

할당된 RNGD 장치가 보이면 정상입니다. 실시간 사용량은 다음으로 확인합니다.

```bash
watch -n 1 furiosa-smi status
```

### 4-3. furiosa-llm

```bash
furiosa-llm version
```

---

## 5. 디렉터리 구조

```
rngd-lab/
├── README.md
├── pyproject.toml        # 프로젝트 의존성
├── uv.lock               # 의존성 잠금 파일
├── .python-version       # Python 3.12
├── check_env.py          # 실습 환경 확인 스크립트
└── day1_npu_chat_test/   # Day 1 실습
```

---

## 6. 실습

> 실습 내용은 추후 추가 예정입니다.

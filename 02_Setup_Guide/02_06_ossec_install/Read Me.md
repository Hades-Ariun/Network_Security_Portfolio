# OSSEC 설치 가이드

이 문서는 OSSEC HIDS 3.7.0 버전을 Ubuntu 서버에 수동 설치하고, GNS3 + VirtualBox 환경과 연동하는 과정을 포트폴리오 목적으로 정리한 문서입니다.  
각 단계는 캡처 이미지와 함께 설치 절차를 쉽게 이해할 수 있도록 설명되어 있습니다.

---

## 📌 설치 개요

- **운영체제:** Ubuntu 22.04 Minimal (GNS3 VirtualBox 기반)  
- **설치 대상:** OSSEC HIDS 3.7.0 (Server 모드)  
- **설치 방식:** GitHub tarball 직접 다운로드 및 수동 설치  
- **활용 목적:** 호스트 기반 침입 탐지 시스템(HIDS) 구성 및 로그 수집 테스트  

---

## 📷 설치 및 설정 과정

### 1. 기본 VM 복제 및 부팅

- `ossec_01_vm_clone.png`  
  Snort3 설치 시 사용했던 "Default_Install" Ubuntu VM을 복제하여 이름을 `OSSEC`으로 지정  

- `ossec_02_vm_boot.png`  
  복제된 가상 머신 부팅 후 로그인 완료 화면  

---

### 2. 시스템 업데이트 및 패키지 설치

- `ossec_03_update_upgrade.png`  
  아래 명령어로 시스템을 최신 상태로 업데이트  
  `sudo apt update && sudo apt upgrade -y`

- `ossec_04_install_dependencies.png`
  OSSEC 설치를 위한 필수 의존성 패키지 설치
  `sudo apt install -y build-essential make zlib1g-dev libpcre2-dev libevent-dev libssl-dev libz-dev libsystemd-dev libsqlite3-dev inotify-tools wget curl unzip`

---

### 3. OSSEC 소스 다운로드 및 압축 해제

- `ossec_05_download_ossec_tarball.png`
  `cd /tmp`로 디렉터리 이동 후
  `wget https://github.com/ossec/ossec-hids/archive/refs/tags/3.7.0.tar.gz` 명령어로 OSSEC tarball 다운로드

- `ossec_06_extract_tarball.png`
  3.7.0.tar.gz 압축 해제 및 설치 디렉터리 이동
  `tar -xvzf 3.7.0.tar.gz`
  `cd ./ossec-hids-3.7.0`

---

### 4. OSSEC 설치 마법사 실행

- `ossec_07_run_installer.png`
  설치 스크립트 실행
  `sudo ./install.sh`


- `ossec_08_select_language.png`
  언어 선택: `en` 입력 후 Enter

- `ossec_09_select_type.png`
  설치 유형 선택: `server` 입력 후 Enter

- `ossec_10_choose_install_path.png`
  설치 경로는 기본값 /var/ossec 유지 → Enter

- `ossec_11_email_notification_prompt.png`
  이메일 알림 설정: `n` 입력

- `ossec_12_integrity_check_prompt.png`
  무결성 검사 데몬 실행: `y` 입력

- `ossec_13_rootkit_detection_prompt.png`
  루트킷 탐지 기능 활성화: `y` 입력

- `ossec_14_active_response_prompt.png`
  Active Response 기능 사용: `y` 입력

- `ossec_15_firewall_response_prompt.png`
  방화벽 자동 차단 기능 활성화: `y` 입력

- `ossec_16_whitelist_prompt.png`
  화이트리스트 IP 추가: `n` 입력

- `ossec_17_remote_syslog_prompt.png`
  외부 syslog 전송 기능: `n` 입력

---

### 5. 설치 완료 및 서비스 확인

- `ossec_18_install_complete.png`
  설치 완료 후 서비스 시작 및 상태 확인
  `sudo systemctl start ossec`
  `sudo systemctl status ossec`

---

### 6. GNS3에 OSSEC VM 연동
- `ossec_19_gns3_vm.png`
  GNS3 → Edit → Preferences → VirtualBox → VirtualBox VMs → New → OSSEC 등록 → Apply → OK

- `ossec_20_virtualbox_vm.png`
  GNS3 프로젝트에 OSSEC-1 배치 후 우클릭 → Start로 VirtualBox 자동 실행 확인


---

## ✅ 설치 완료 및 준비 상태

- OSSEC HIDS Server 설치 및 기본 데몬 정상 작동
- GNS3 연동 환경 구성 완료로 향후 공격/로그 테스트 환경에 활용 가능

--- 

## 📎 참고 링크

- OSSEC GitHub: [https://github.com/ossec/ossec-hids](https://github.com/ossec/ossec-hids)
- OSSEC 공식 문서: [https://www.ossec.net/docs/](https://www.ossec.net/docs/)
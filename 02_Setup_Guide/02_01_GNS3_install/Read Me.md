# GNS3 설치 및 설정 가이드

이 문서는 GNS3 설치부터 VirtualBox 기반 GNS3 VM 연동까지의 전 과정을 포트폴리오 목적으로 정리한 문서입니다.  
각 단계는 캡처 이미지와 함께 상세 설명을 포함하고 있습니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)
- **가상화 도구:** VirtualBox
- **설치 도구:** GNS3
- **활용 목적:** 보안 네트워크 포트폴리오 (pfSense, ASAv 등 테스트 구성)

---

## 📷 설치 및 설정 과정

### 1. GNS3 다운로드

- `gns3_01_download_page.png`  
  [https://gns3.com](https://gns3.com) 접속 → "Free Download" 클릭 → Windows 선택  
  > ※ 회원가입 필요

### 2. 설치 마법사 실행

- `gns3_02_installer_start.png`  
  설치 시작 → "Next" → 약관 동의 "I Agree"

- `gns3_03_start_menu.png`  
  Start Menu 폴더 이름은 기본값(GNS3) 유지 후 "Next"

- `gns3_04_components_selection.png`  
  WebClient, GNS3 VM 등은 추후 수동 설치 가능 → 기본값으로 "Next"

- `gns3_05_install_path.png`  
  설치 경로는 기본값으로 "Next"

- `gns3_06_installing_progress.png`  
  설치 진행 중 화면

---

### 3. Npcap 설치

- `gns3_07-1_Npcap_Install.png`  
  "I Agree" 후 설치

- `gns3_07-2_Npcap_Options.png`  
  모든 옵션은 체크 해제  
  - 보안 목적이 아닌 테스트용이므로 제한 미설정

---

### 4. 부가 프로그램 설치 (선택 사항)

- `gns3_08_Wireshark_install.png`  
  Wireshark 자동 설치

- `gns3_09_traceNG.png`  
  TraceNG 설치 요청은 "Cancel"

- `gns3_10_Solar-putty.png`  
  Solar-Putty 설치 요청은 "Cancel"

---

### 5. 설치 완료 및 초기 설정

- `gns3_11_install_complete.png`  
  설치 완료

- `gns3_12_Solarwinds_Setup.png`  
  Solarwinds 설치 창에서 "No" 선택 후 "Next"

- `gns3_13-1_Setup_Wizard.png`  
  "Run appliances in a virtual machine" 체크  
  "Don't show this again" 체크 → "Next"

- `gns3_13-2_Setup_Wizard.png`  
  Server 설정 화면은 기본값 그대로 "Next"

- `gns3_13-3_Setup_Wizard.png`  
  VMware 미설치로 인한 에러 → "OK" 후 "Cancel"

---

## 🖥 GNS3 + VirtualBox 연동

### 6. GNS3 첫 실행 및 VM 설정

- `gns3_14_first_launch.png`  
  GNS3 첫 실행 화면

- `gns3_15-1_virtualbox_setup.png`  
  Edit > Preferences 또는 Ctrl + Shift + P 진입

- `gns3_15-2_virtualbox_setup.png`  
  GNS3 VM 탭 → virtualization engine: **VirtualBox** 선택  
  → Downloaded here 링크 클릭 → GNS3 VM.ova 다운로드 및 압축 해제

- `gns3_15-3_virtualbox_setup.png`  
  VirtualBox > 파일 > 가상 시스템 가져오기

- `gns3_15-4_virtualbox_setup.png`  
  GNS3 VM.ova 파일 선택 → "다음"

- `gns3_15-5_virtualbox_setup.png`  
  MAC 주소 정책만 “모든 네트워크 어댑터의 새 MAC 주소 생성” 선택 → 나머지 Default

- `gns3_15-6_virtualbox_setup.png`  
  가상 시스템 가져오기 진행 중 화면

---

### 7. VirtualBox 설정

- `gns3_15-7_virtualbox_setup.png`  
  도구 > "만들기" → 호스트 전용 어댑터 생성  
  DHCP 서버 활성화 체크

- `gns3_15-8_virtualbox_setup.png`  
  GNS3 VM 선택 후 "설정"

- `gns3_15-9_virtualbox_setup.png`  
  [시스템] - 마더보드:  
  - 메모리: 8192MB  
  - 부팅순서: 하드디스크 > 광디스크 (둘 다 체크)

- `gns3_15-10_virtualbox_setup.png`  
  [시스템] - 프로세서:  
  - CPU : 2개  
  - PAE/NX 활성화

- `gns3_15-11_virtualbox_setup.png`  
  [네트워크] - 어댑터 1:  
  - 연결 방식: 호스트 전용 어댑터  
  - 생성한 어댑터 선택

- `gns3_15-12_virtualbox_setup.png`  
  [네트워크] - 어댑터 2:  
  - 연결 방식: NAT

---

### 8. GNS3에서 GNS3 VM 연동 확인

- `gns3_15-13_virtualbox_setup.png`  
  GNS3로 돌아와 GNS3 VM 설정  
  - "Refresh" 클릭 → VM 자동 인식  
  - "Enable the GNS3 VM" 체크 → "Apply"

- `gns3_15-14_virtualbox_setup.png`  
  VirtualBox에서 GNS3 VM 자동 실행 확인

- `gns3_15-15_virtualbox_setup.png`  
  GNS3 내부 "Servers Summary"에서 GNS3 VM이 녹색으로 활성화

---

### 9. 프로젝트 생성 및 장비 배치

- `gns3_15-16_virtualbox_setup.png`  
  File > New Blank Project →  
  프로젝트 이름: `Network_Security_Portfolio` 입력 → OK

- `gns3_15-17_virtualbox_setup.png`  
  장비 배치 시 "Please choose a server" 창  
  → "GNS3 VM" 선택

- `gns3_15-18_virtualbox_setup.png`  
  장비가 녹색불로 정상 배치되었음을 확인

---

## ✅ 설치 및 연동 완료

- GNS3 설치 및 VirtualBox 연동 정상 완료
- 새 프로젝트 및 장비 배치까지 테스트 성공
- pfSense, ASAv 등 장비 연동 준비 완료

---

## 📎 참고 링크

- 공식 사이트: [https://gns3.com](https://gns3.com)
- OVA 다운로드가 되지 않을 경우 수동 다운로드 필요
- 각 설정 단계는 포트폴리오 보고용으로 보안성과 실용성 기준에 따라 구성됨

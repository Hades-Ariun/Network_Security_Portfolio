# 📘 pfSense 설치 가이드 (VirtualBox 기반)

이 문서는 pfSense 2.7.0을 VirtualBox에 설치한 후, GNS3에 연동하여 네트워크 시뮬레이션 환경을 구축하는 전 과정을 포트폴리오 목적으로 정리한 문서입니다.
각 단계는 캡처 이미지와 함께 상세 설명을 포함하고 있습니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)  
- **가상화 도구:** VirtualBox 
- **설치 대상:** pfSense 2.7.0 
- **활용 목적:** 보안 네트워크 포트폴리오 내 방화벽 구성 및 테스트

---

## 📷 설치 및 설정 과정

### 1. pfSense ISO 다운로드

- `pfsense_01_download_page.png`
[https://archive.org/details/pfsense-ce-2.7.0-release-amd64_202308](https://archive.org/details/pfsense-ce-2.7.0-release-amd64_202308) 접속 → ISO IMAGE 다운로드

- `pfsense_02_download_progress.png`
  ISO 이미지 다운로드 진행 화면

---

### 2. VirtualBox에 pfSense VM 생성

- `pfsense_03_virtualbox_new_vm.png`
  VirtualBox → 머신 → 새로 만들기 →

  이름: pfSense

  종류: BSD

  버전: FreeBSD (64-bit)

  그 외 : Default값 유지

  → 다음

- `pfsense_04_vm_memory_cpu.png`
  메모리: 2048MB

  CPU: 2개
  
  → 다음

- `pfsense_05_vm_disk_config.png`
  가상 하드 디스크 → 지금 새 가상 하드디스크 만들기 → 용량: 20GB → 다음

- `pfsense_06_vm_complete.png`
  VM 생성 요약 확인 → 완료

### 3. VM 하드웨어 설정 조정

- `pfsense_07-01_vm_settings.png`
  VirtualBox → pfSense → 설정 → 시스템 → 마더보드:

  메모리: 2048MB

  부팅 순서: 하드디스크, 광디스크 순 정렬 후 체크

- `pfsense_07-02_vm_settings.png`
  시스템 → 프로세서:

  CPU 2개

  "PAE/NX 활성화" 체크

- `pfsense_07-03_vm_settings.png`
  네트워크 → 어댑터 1:

  "네트워크 어댑터 활성화" 체크

  "다음에 연결됨 : 어댑터에 브리지" 선택

- `pfsense_07-04_vm_settings.png`
  네트워크 → 어댑터 2:

  "네트워크 어댑터 활성화" 체크

  "다음에 연결됨 : 내부 네트워크" 선택

  이름: intnet (기본값 사용)

- `pfsense_07-05_vm_settings.png`
  저장소 → "비어있음" 선택 → 속성 → 광학드라이브 우측 디스크 아이콘 클릭 → 디스크 파일 선택 →
  1번 단계에서 다운로드 받은 pfSense ISO 파일 선택

  

### 4. pfSense 설치

- `pfsense_08_vm_boot_iso.png`
  VM 실행 후 부팅 확인

- `pfsense_09_vm_Licenses.png`
  라이센스 화면 → Accept 선택

- `pfsense_10_installer_menu.png`
  설치 메뉴 → "Install" 선택 → OK

- `pfsense_11_Partitioning.png`
  파티션 방식 선택: "Auto (ZFS) Guided Root-on-ZFS" 선택 → OK

- `pfsense_12_ZFS_Configuration1.png`
  설치 진행 선택: "Install Proceed with Installation" 선택 → OK

- `pfsense_13_ZFS_Configuration2.png`
  장치 유형: "stripe (No Redundancy)" 선택 → OK

- `pfsense_14_ZFS_Configuration3.png`
  디스크 선택: "ada0 : VBOX HARDDISK"를 '스페이스바(Space Bar)' 이용하여 체크 후 OK

- `pfsense_15_ZFS_configuration4.png`
  기존 디스크 내용 삭제 : 방향키로 "YES" 선택 → 'Enter'로 설치 진행

- `pfsense_16_installing_progress.png`
  설치 진행 화면

- `pfsense_17_reboot_prompt.png`
  설치 완료 후 "Reboot" 선택 → 'Enter'

### 5. pfSense 부팅 확인

- `pfsense_18_post_boot_config.png`
  부팅 완료 후 콘솔 메뉴 진입 화면

- `pfsense_19_virtualbox_vm_shutdown.png`
  GNS3 연동을 위해 pfSense 종료 → '전원 꺼짐' 상태 확인

### 6. GNS3에 pfSense 연동

- `pfsense_20-1_gns3_virtualbox_preferences.png`
  GNS3 → Edit → Preferences → VirtualBox VMs → New →

  "Run this VirtualBox VM on my local computer" 선택 → Next

- `pfsense_20-2_gns3_virtualbox_preferences.png`
  VM list : pfSense 선택 → Finish

- `pfsense_20-3_gns3_virtualbox_preferences.png`
  Apply → OK 클릭하여 등록 완료

### 7. GNS3 프로젝트에서 pfSense 사용

- `pfsense_21_gns3_add_virtualbox_vm.png`
  GNS3 프로젝트에 pfSense-1 배치

- `pfsense_22_gns3_pfsense_configuration.png`
  pfSense-1 더블 클릭 → Network 탭

  Adapters : 2

  "Allow GNS3 to use any configured VirtualBox adapter" 체크 → Apply → OK

- `pfsense_23_virtualbox_pfSense_console_menu.png`
  pfSense-1 우클릭 → Start
  → VirtualBox에서 pfSense 실행 확인

---

## ✅ 설치 및 연동 완료

- pfSense ISO 기반 설치 완료
- VirtualBox에서 네트워크 구성 및 ZFS 기반 파티셔닝 적용
- GNS3 연동 성공, 테스트 프로젝트에서 장비 정상 작동 확인

## 📎 참고 링크

- pfSense ISO 다운로드:[https://archive.org/details/pfsense-ce-2.7.0-release-amd64_202308](https://archive.org/details/pfsense-ce-2.7.0-release-amd64_202308)
- GNS3 공식:[https://gns3.com](https://gns3.com)
- pfSense 공식 문서:[https://docs.netgate.com](https://docs.netgate.com)
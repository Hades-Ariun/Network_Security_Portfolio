# Snort3 설치 및 GNS3 연동 가이드

Ubuntu Server 환경에서 침입 탐지 시스템인 **Snort3**를 설치하고, GNS3와 연동하여 네트워크 트래픽 분석 실습 환경을 구축하는 과정을 설명합니다. 각 단계별로 캡처 이미지를 포함하여 설치 및 설정 과정을 쉽게 따라 할 수 있도록 구성하였습니다.

---

## 📌 설치 개요

- **운영체제:** Ubuntu Server 24.04 (VirtualBox)
- **사용 도구:** VirtualBox, GNS3
- **설치 대상:** Snort3 (IDS/IPS)
- **활용 목적:** 보안 침입 탐지 및 네트워크 트래픽 분석 실습

---

## 🛠️ 설치 및 설정 과정

### 1. Ubuntu ISO 다운로드

- `snort_01_download_ubuntu.png`  
  Ubuntu 공식 사이트에서 서버용 ISO 파일을 다운로드합니다.

- `snort_02_download_progress.png`  
  다운로드 진행 상황을 확인합니다.

---

### 2. VirtualBox에서 Snort3용 VM 생성

- `snort_03_virtualbox_new_vm.png`  
  새 가상 머신을 생성하고 Ubuntu (64-bit)로 설정합니다.

- `snort_04_vm_memory_cpu.png`  
  메모리는 2048MB, CPU는 2개로 설정합니다.

- `snort_05_vm_disk_config.png`  
  디스크 용량은 25GB로 구성합니다.

- `snort_06_vm_complete.png`  
  가상 머신 생성이 완료된 화면입니다.

---

### 3. VM 설정 변경 (부팅 및 네트워크)

- `snort_07-01_vm_settings.png`  
  부팅 순서를 CD/DVD → 하드디스크 순으로 설정합니다.

- `snort_07-02_vm_settings.png`  
  프로세서 설정에서 "PAE/NX"를 활성화합니다.

- `snort_07-03_vm_settings.png`  
  ISO 파일을 CD 드라이브에 마운트합니다.

- `snort_07-04_vm_settings.png`  
  네트워크 어댑터를 브리지 모드로 설정하고, 무작위 모드는 "모두 허용"으로 지정합니다.

---

### 4. Ubuntu Server 설치

- `snort_08_vm_install_menu.png`  
  설치 메뉴에서 "Install Ubuntu Server"를 선택합니다.

- `snort_09_vm_Rangueage.png` ~ `snort_21_vm_featured_server_snaps.png`  
  언어, 키보드, 네트워크, 사용자 계정, 디스크 파티션, OpenSSH 설치 등 전체 설치 과정을 진행합니다.

- `snort_22_vm_installing_progress.png`  
  설치 진행 중 화면입니다.

- `snort_23_vm_install_complete.png`  
  설치 완료 후 재부팅을 진행합니다.

- `snort_24_ubuntu_login_prompt.png`  
  설치가 완료되어 로그인 프롬프트가 나타난 모습입니다.

---

### 5. 초기 업데이트 및 스냅샷 생성

- `snort_25_update_upgrade.png`  
  `sudo apt update && sudo apt upgrade -y` 명령어를 통해 시스템을 최신 상태로 업데이트합니다.

- `snort_26_snapshot.png`  
  초기 상태를 기록하기 위해 VirtualBox에서 스냅샷을 생성합니다.

- `snort_27_replication.png`  
  동일한 환경 구성을 위해 VM을 복제합니다.

---

### 6. Snort3 설치에 필요한 도구 설치

- `snort_28_install_dependencies.png`  
  Snort3 설치에 필요한 필수 패키지를 설치합니다.

- `snort_29_install_git.png`  
  Git을 설치합니다.

---

### 7. libdaq 설치

- `snort_30-01_install_libdaq.png`  
  GitHub에서 libdaq 소스를 클론합니다.

- `snort_30-02_install_libdaq.png`  
  `bootstrap` 스크립트를 실행합니다.

- `snort_30-03_install_libdaq.png`  
  `configure`를 통해 빌드 설정을 진행합니다.

- `snort_30-04_install_libdaq.png`  
  `make`를 통해 컴파일합니다.

- `snort_30-05_install_libdaq.png`  
  `make install`을 통해 설치를 완료합니다.

---

### 8. wget 및 gperftools 설치

- `snort_31_install_wget.png`  
  wget을 설치합니다.

- `snort_32-01_install_gperftools.png` ~ `snort_32-05_install_gperftools.png`
  gperftools를 다운로드하고 빌드 및 설치합니다.

---

### 9. unzip 설치

- `snort_33_install_unzip.png`  
  unzip 패키지를 설치합니다.

---

### 10. Snort3 소스 빌드 및 설치

- `snort_34-01_install_snort.png` ~ `snort_34_06_install_snort.png`  
  Snort3 소스를 다운로드하고 빌드 및 설치합니다.  
  마지막으로 `ldconfig`를 실행하여 라이브러리를 적용합니다.

---

### 11. Snort3 설치 확인

- `snort_35_snort_version_check.png`  
  `snort -V` 명령어를 통해 Snort3 설치가 정상적으로 완료되었는지 확인합니다.

---

### 12. GNS3와 연동

- `snort_36_gns3_vm.png`  
  GNS3에서 Snort3가 설치된 VirtualBox VM을 불러옵니다.

- `snort_37_virtualbox_vm.png`  
  GNS3 프로젝트에 Snort3 VM을 배치하여 테스트합니다.

---

## ✅ 설치 완료 및 준비 상태

- Snort3 설치 및 환경 변수 구성 완료
- GNS3와 연동 완료 상태로 IDS/IPS 실습 진행 준비 완료

---

## 📎 참고 링크

- Snort3 공식 문서: [https://docs.snort.org](https://docs.snort.org)
- Snort3 GitHub: [https://github.com/snort3/snort3](https://github.com/snort3/snort3)
- libdaq GitHub: [https://github.com/snort3/libdaq](https://github.com/snort3/libdaq)
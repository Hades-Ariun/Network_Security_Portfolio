# Zabbix 설치 및 GNS3 연동 가이드 (Ubuntu Server 24.04 기반)

IT 인프라 모니터링 시스템인 **Zabbix**를 **Ubuntu Server 24.04**에 설치하고, GNS3와 연동하여 실습 환경을 구축하는 과정을 단계별로 안내합니다.
본 가이드는 ISO 다운로드부터 VirtualBox 설정, Zabbix 설치, 그리고 GNS3 연동까지 포함되어 있습니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)
- **가상화 도구:** VirtualBox
- **설치 대상:** Zabbix 7.0 (Ubuntu Server 24.04)
- **활용 목적:** 모니터링 시스템 구축 및 GNS3 연동 실습

---

## 💻 설치 및 설정 과정

### 1️⃣ Ubuntu Server ISO 다운로드

- `zabbix_01_download_ubuntu.png`
 Ubuntu 공식 사이트에서 Server install ISO 파일을 다운로드합니다.
 링크: [https://releases.ubuntu.com/noble/](https://releases.ubuntu.com/noble/)

- `zabbix_02_download_progress.png`
 ISO 파일 다운로드 진행 중 화면입니다.

 ---

 ### 2️⃣ VirtualBox에서 Zabbix용 가상머신 생성

- `zabbix_03_virtualbox_new_vm.png`
 VirtualBox → 새로 만들기 → 이름은 `Zabbix`, 종류는 `Linux`, 버전은 `Ubuntu (64-bit)`로 설정합니다.

- `zabbix_04_vm_memory_cpu.png`
 메모리는 2048MB, CPU는 2개로 설정합니다.

- `zabbix_05_vm_disk_config.png`
 가상 하드 디스크를 새로 만들고, 디스크 크기는 20GB로 지정합니다.

- `zabbix_06_vm_complete.png`
 가상 머신 생성 완료 요약 화면입니다.

---

### 3️⃣ Zabbix VM 설정 조정

- `zabbix_07-01_vm_settings.png`
 부팅 순서를 하드디스크 → 광디스크 순으로 정렬하고 체크합니다.

- `zabbix_07-02_vm_settings.png`
 시스템 → 프로세서 → **PAE/NX 활성화** 옵션을 활성화합니다.

- `zabbix_07-03_vm_settings.png`
 저장소 → IDE 컨트롤러의 광학 드라이브에 ISO 파일을 마운트합니다.

- `zabbix_07-04_vm_settings.png`
 네트워크 어댑터는 브리지 모드로 설정하고, 어댑터 활성화도 체크합니다.

---

### 4️⃣ Ubuntu Server 설치

- `zabbix_08_vm_install_menu.png`
 설치 화면에서 `Try or install Ubuntu Server`를 선택합니다.

- `zabbix_09_vm_Rangueage.png`
 언어는 `English`로 선택합니다.

- `zabbix_10_vm_keyboard_configuration.png`
 키보드 레이아웃은 기본값인 `English (US)`로 설정하고 Done 클릭.

- `zabbix_11_vm_installation_type.png`
 `Ubuntu Server (minimized)`를 선택하고 설치를 진행합니다.

- `zabbix_12_vm_network_config.png`
 IPv4는 DHCP 자동 설정을 사용합니다.

- `zabbix_13_vm_proxy_configuration.png`
 프록시 설정은 생략하고 Done을 선택합니다.

- `zabbix_14_vm_mirror_configuration.png`
 기본 미러 서버 사용 → Done

- `zabbix_15_vm_storage_configuration.png`
 저장소 구성은 기본값으로 진행 → Done

- `zabbix_16_vm_file_system_summary.png`
 파일 시스템 요약을 확인하고 진행합니다.

- `zabbix_17_vm_destructive_action.png`
 디스크 포맷 경고 화면에서 Continue를 선택합니다.

- `zabbix_18_vm_user_account.png`
 사용자 계정은 `test`, 비밀번호는 `1234`로 설정합니다.

- `zabbix_19_vm_ubuntu_pro.png`
 Ubuntu Pro 설치는 건너뜁니다 (`Skip for now` 선택).

- `zabbix_20_vm_software_selection.png`
 소프트웨어 선택 화면에서 `Install OpenSSH server`만 선택합니다.

- `zabbix_21_vm_featured_server_snaps.png`
 스냅 패키지는 아무것도 선택하지 않고 Done을 클릭합니다.

- `zabbix_22_vm_installing_progress.png`
 Ubuntu 설치가 진행 중인 화면입니다.

- `zabbix_23_vm_install_complete.png`
 설치 완료 후 `Reboot Now`를 선택하여 재부팅합니다.

- `zabbix_24_ubuntu_login_prompt.png`
 부팅 완료 후 Ubuntu 로그인 프롬프트 화면입니다.

---

### 5️⃣ Zabbix 설치

- `zabbix_25_repo_download.png`
 Zabbix 공식 저장소 .deb 파일 다운로드:
 `sudo wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_7.0-1+ubuntu24.04_all.deb`

- `zabbix_26_dpkg_install.png`
 저장소 설치:
 `sudo dpkg -i zabbix-release_7.0-1+ubuntu24.04_all.deb`

- `zabbix_27_apt_update.png`
 패키지 목록 업데이트:
 `sudo apt update`

- `zabbix_28_dependency_install.png`
 Zabbix 관련 패키지 일괄 설치:
 `sudo apt install -y zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent2 php-mysql php-gd php-bcmath php-net-socket mariadb-server php php-fpm`

- `zabbix_29_apt_upgrade.png`
 시스템 패키지 업그레이드:
 `sudo apt upgrade -y`

---

### 6️⃣ GNS3 연동 테스트

- `zabbix_30_gns3_vm.png`
 GNS3 설정에서 VirtualBox VM을 추가하고, 리스트에서 Zabbix 선택 → Finish → Apply → OK

- `zabbix_31_gns3.png`
 GNS3 프로젝트에 Zabbix-1을 추가하고 우클릭 → Start하여 VirtualBox와의 연동이 정상적으로 되는지 확인합니다.

---

## ✅ 설치 완료 및 준비 상태

- Ubuntu Server 24.04 기반 Zabbix 7.0 설치 완료
- Apache, PHP, MariaDB 연동 및 패키지 구성 완료
- VirtualBox 가상 머신 정상 구동
- GNS3와 연동 완료된 상태로 실습 환경 준비 완료

---

## 📎 참고 링크

- Ubuntu Server ISO 다운로드:
 [https://releases.ubuntu.com/noble/](https://releases.ubuntu.com/noble/)
- Zabbix 공식 저장소:
 [https://www.zabbix.com/download](https://www.zabbix.com/download)
- GNS3 공식 웹사이트:
 [https://gns3.com](https://gns3.com)
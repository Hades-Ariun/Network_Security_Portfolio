# Suricata 설치 가이드 (Rocky Linux 9.5 기반)

보안 네트워크 환경에서 침입 탐지 및 분석을 위한 **Suricata** 설치 가이드입니다.  
본 문서는 **Rocky Linux 9.5 Minimal**을 VirtualBox에 설치한 후, Suricata를 구성하고 GNS3와 연동하는 초기 설치 과정까지 다룹니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)  
- **가상화 도구:** VirtualBox  
- **설치 대상:** Suricata (Rocky Linux 9.5 Minimal)  
- **활용 목적:** GNS3 보안 실습 환경에서 IDS/IPS 구성

---

## 💻 설치 및 설정 과정

### 1️⃣ Rocky Linux ISO 다운로드

- `suricata_01_download_rocky.png`  
  Rocky Linux 공식 사이트의 Vault 경로에서 9.5 버전 minimal ISO 파일을 다운로드합니다.  
  링크: [https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/](https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/)

---

### 2️⃣ VirtualBox에서 Suricata용 가상머신 생성

- `suricata_02_virtualbox_new_vm.png`  
  VirtualBox에서 새 머신 생성 시 이름은 `suricata`, 종류는 `Linux`, 버전은 `Red Hat (64-bit)`로 설정합니다.

- `suricata_03_vm_memory_cpu.png`  
  메모리는 2048MB, CPU는 2개로 설정합니다.

- `suricata_04_vm_disk_config.png`  
  가상 디스크는 10GB로 새로 생성합니다.

- `suricata_05_vm_complete.png`  
  VM 생성 요약 화면을 확인하고 완료를 클릭합니다.

---

### 3️⃣ Suricata VM 설정 조정

- `suricata_06-01_vm_settings.png`  
  부팅 순서는 하드디스크 → 광디스크 순으로 설정하고 체크합니다.

- `suricata_06-02_vm_settings.png`  
  시스템 → 프로세서에서 **PAE/NX 활성화** 옵션을 체크합니다.

- `suricata_06-03_vm_settings.png`  
  저장소 → IDE 컨트롤러 → 비어있음 클릭 → ISO 파일을 마운트합니다.

- `suricata_06-04_vm_settings.png`  
  네트워크 어댑터는 브리지 모드로 설정하고 무작위 모드는 "모두 허용"으로 변경합니다.

---

### 4️⃣ Rocky Linux 설치

- `suricata_07_Rocky_install_main.png`  
  Rocky Linux 설치 화면에서 `Install Rocky Linux 9.5`를 선택하여 설치를 시작합니다.

- `suricata_08_install_language.png`  
  언어는 `한국어`로 설정하고 계속 진행합니다.

- `suricata_09_install_disk.png`  
  디스크는 자동 설정으로 지정합니다.

- `suricata_10_install_root.png`  
  루트 계정 비밀번호는 테스트용으로 `1234`로 설정하고 설치를 시작합니다.

- `suricata_11_install_progress.png`  
  설치가 진행되는 화면입니다.

- `suricata_12_install_complete.png`  
  설치가 완료되면 시스템을 재부팅합니다.

- `suricata_13_first_boot_login.png`  
  재부팅 후 첫 로그인 프롬프트 화면입니다.

---

### 5️⃣ Suricata 설치

- `suricata_14_epel_install.png`  
  EPEL 저장소를 추가합니다:  
  `sudo dnf install -y epel-release`

- `suricata_15_update_system.png`  
  시스템 전체 업데이트를 수행합니다:  
  `sudo dnf update -y`

- `suricata_16_suricata_install.png`  
  Suricata 패키지를 설치합니다:  
  `sudo dnf install -y suricata`

- `suricata_17_suricata_version.png`  
  `suricata -V` 명령어로 설치와 버전을 확인합니다.

---

### 6️⃣ GNS3 연동 테스트

- `suricata_18_gns3_vm_add.png`  
  GNS3 설정에서 VirtualBox VM을 새로 등록하고 Suricata VM을 선택해 추가합니다.

- `suricata_19_gns3_project_test.png`  
  GNS3 프로젝트에 Suricata를 추가 후 실행해 VirtualBox와의 연동이 정상적으로 되는지 확인합니다.

---

## ✅ 설치 완료 및 준비 상태

- Rocky Linux 9.5 기반 Suricata 설치 완료  
- GNS3 연동을 통한 테스트 환경 구축 완료

---

## 📎 참고 링크

- Rocky Linux ISO 다운로드:  
  [https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/](https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/)  
- Suricata 공식 문서:  
  [https://docs.suricata.io](https://docs.suricata.io)  
- GNS3 공식 웹사이트:  
  [https://gns3.com](https://gns3.com)
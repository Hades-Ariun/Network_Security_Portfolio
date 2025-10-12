# Kali Linux 설치 및 GNS3 연동 가이드 (VirtualBox 기반)

모의 해킹 및 침투 테스트 도구로 널리 사용되는 **Kali Linux**를 VirtualBox에 설치하고, GNS3와 연동하여 보안 실습 환경을 구축하는 방법을 안내합니다.
본 가이드는 ISO 다운로드부터 설치, GNS3 연동까지 단계별로 구성되어 있으며, 각 단계는 스크린샷과 함께 따라하기 쉽게 정리되어 있습니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)
- **가상화 도구:** VirtualBox
- **설치 대상:** Kali Linux 2025.2 (64-bit)
- **활용 목적:** GNS3 보안 실습 환경에서 침투 테스트 실습

---

## 💻 설치 및 설정 과정

### 1️⃣ Kali ISO 다운로드

- `kali_01_official_download_page.png`
 Kali 공식 홈페이지에서 설치용 ISO 파일을 다운로드합니다.
 링크: [https://www.kali.org/get-kali/#kali-installer-images](https://www.kali.org/get-kali/#kali-installer-images)

- `kali_02_installer_iso_download.png`
 `kali-linux-2025.2-installer-amd64.iso` 다운로드 진행 중 화면입니다.

---

### 2️⃣ VirtualBox에서 Kali용 가상머신 생성

- `kali_03_create_vm_start.png`
 VirtualBox에서 새 머신 생성 시 이름은 `Kali`, 종류는 `Linux`, 버전은 `Debian (64-bit)`로 설정합니다.

- `kali_04_set_memory.png`
 메모리는 4096MB, CPU는 2개로 설정합니다.

- `kali_05_create_disk.png`
 가상 하드디스크는 새로 생성하고, 디스크 크기는 40GB로 지정합니다.

---

### 3️⃣ Kali VM 설정 조정

- `kali_06_attach_iso_1.png`
 부팅 순서는 하드디스크 → 광디스크 순으로 설정합니다.

- `kali_06_attach_iso_2.png`
 시스템 → 프로세서에서 **PAE/NX** 활성화 옵션을 체크합니다.

- `kali_06_attach_iso_3.png`
 저장소 → IDE 컨트롤러 → 광학 드라이브에 ISO 파일을 마운트합니다.

- `kali_06_attach_iso_4.png`
 네트워크 어댑터는 브리지 모드로 설정하고, 어댑터 활성화도 체크합니다.

---

### 4️⃣ Kali Linux 설치

- `kali_07_boot_menu.png`
 Kali 부팅 화면에서 Graphical install을 선택합니다.

- `kali_08_language_select.png`
 언어는 한국어를 선택하고 계속 진행합니다.

- `kali_09_location_select.png`
 지역은 대한민국을 선택합니다.

- `kali_10_keyboard_layout.png`
 키보드 레이아웃은 한국어를 선택합니다.

- `kali_11_install.png`
 설치가 진행 중인 화면입니다.

- `kali_12_hostname.png`
 호스트네임은 kali로 설정합니다.

- `kali_13_domain.png`
 도메인 이름은 비워둡니다.

- `kali_14_fullname.png`
 사용자 전체 이름은 `test`로 입력합니다.

- `kali_15_username.png`
 사용자 이름은 `test`로 입력합니다.

- `kali_16_password.png`
 비밀번호는 `1234`로 설정합니다.

- `kali_17_partition_method.png`
 디스크 파티션 방법은 자동 - 디스크 전체 사용을 선택합니다.

- `kali_18_disk_select.png`
 사용할 디스크를 선택합니다.

- `kali_19_partition_scheme.png`
 파티션 구성은 모두 한 파티션에 설치를 선택합니다.

- `kali_20_finish_partitioning.png`
 파티션 나누기 완료 후 디스크에 변경 사항 쓰기를 진행합니다.

- `kali_21_write_changes_confirm.png`
 디스크에 변경 사항을 적용합니다.

- `kali_22_software_selection.png`
 아래 항목을 체크한 후 계속 진행합니다:

 `Xfce (Kali's default desktop environment)`

 `top 10 -- the 10 most popular tools`
 (기타 항목은 선택하지 않아도 됩니다)

- `kali_23_install_progress.png`
 소프트웨어 설치가 진행 중인 화면입니다.

- `kali_24_grub_prompt.png`
GRUB 부트로더 설치 여부 → 예 선택

- `kali_25_grub_device.png`
 GRUB 설치 대상 → /dev/sda 선택

- `kali_26_install_complete.png`
 설치가 완료되면 시스템을 재시작합니다.

---

### 5️⃣ Kali 첫 실행

- `kali_27_login_screen.png`
 설치 후 Kali 로그인 화면이 표시됩니다.

- `kali_28_desktop_screen.png`
 로그인 후 Kali의 기본 바탕화면 화면입니다.

---

### 6️⃣ GNS3 연동 테스트

- `kali_29_gns3_vm.png`
 GNS3 → Preferences → VirtualBox → VirtualBox VMs → New
 `Run this VirtualBox VM on my local computer` 선택 후, VM 리스트에서 Kali 선택 → Finish → Apply → OK

- `kali_30_virtualbox_vm.png`
 GNS3 프로젝트에 Kali VM을 추가하고 우클릭 → Start 실행하여 VirtualBox와의 연동이 정상적으로 되는지 확인합니다.

---

## ✅ 설치 완료 및 준비 상태

- Kali Linux 2025.2 기반 설치 완료
- 기본 도구 및 Xfce 데스크탑 환경 구성
- VirtualBox 가상 머신 정상 실행
- GNS3 연동을 통한 보안 실습 환경 구축 완료

---

## 📎 참고 링크

- Kali Linux 공식 다운로드:
 [https://www.kali.org/get-kali/#kali-installer-images](https://www.kali.org/get-kali/#kali-installer-images)
- GNS3 공식 웹사이트:
 [https://gns3.com](https://gns3.com)
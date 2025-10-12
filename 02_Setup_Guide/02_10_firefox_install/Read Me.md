# Firefox QEMU 이미지 설치 가이드 (GNS3 연동용)

TinyCore Linux 기반의 **Firefox** 이미지를 GNS3에 **QEMU VM**으로 등록하고 테스트하는 과정을 설명합니다.
본 문서는 SourceForge에서 제공하는 .img 파일을 기반으로 하며, GNS3에서 GUI 환경을 테스트하는 목적에 적합합니다.

---

## 📌 설치 개요

- **운영체제:** TinyCore Linux (Firefox 포함)
- **사용 이미지:** linux-tinycore-linux-6.4-firefox-33.1.1-2.img
- **가상화 도구:** GNS3 (QEMU 기반)
- **활용 목적:** 포트폴리오용 네트워크 테스트 — ping 응답 확인, HTTP/Telnet 접속 테스트, 방화벽 룰(허용/차단) 동작 검증 등

---

## 💻 설치 및 설정 과정

### 1️⃣ QEMU Firefox 이미지 다운로드

- `01_open_sourceforge_page.png`
 Firefox 설치 사이트로 접속하여 linux-tinycore-linux-6.4-firefox-33.1.1-2.img를 다운로드합니다.
 링크: [https://sourceforge.net/projects/gns-3/files/Qemu%20Appliances/](https://sourceforge.net/projects/gns-3/files/Qemu%20Appliances/)

- `02_download_button_click.png`
 이미지 파일 다운로드 진행 화면

---

### 2️⃣ GNS3에서 QEMU VM 등록 (GNS3 VM에서 실행)

- `03_open_gns3_preferences.png`
 GNS3 → Edit → Preferences → QEMU → Qemu VMs → New → Server type: Run this Qemu VM on the GNS3 VM 선택 → Next

- `04_input_vm_name.png`
 Name: `Firefox` → Next

- `05_select_qemu_binary.png`
 QEMU binary 선택 화면 → 기본(Default) 값 사용 → Next

- `06_select_console_type.png`
 Console type 선택 → `vnc` 선택 → Next

- `07_select_img_file.png`
 1단계에서 다운로드한 *.img 파일 지정 → Finish → Apply → OK

---

### 3️⃣ GNS3 프로젝트에서 Firefox VM 실행

- `08_gns3_project_test.png`
 새 GNS3 프로젝트 생성 후, Firefox QEMU VM을 프로젝트에 배치 → 우클릭 → Start → 정상적으로 GUI가 실행되는지 확인

---

## ✅ 설치 완료 및 준비 상태

- Firefox 이미지가 GNS3에 QEMU VM으로 정상 등록됨
- 프로젝트에서 GUI 브라우저 테스트 가능
- 다른 QEMU 기반 어플라이언스와도 동일 방식으로 연동 가능

---

## 📎 참고 링크

- GNS3 QEMU Appliances:
 [https://sourceforge.net/projects/gns-3/files/Qemu%20Appliances/](https://sourceforge.net/projects/gns-3/files/Qemu%20Appliances/)
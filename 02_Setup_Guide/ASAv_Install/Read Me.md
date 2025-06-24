# ASAv 설치 가이드

이 문서는 ASAv 842 버전을 GNS3 QEMU VM으로 설정하고 부팅하는 과정을 포트폴리오 목적으로 정리한 문서입니다.  
각 단계는 캡처 이미지와 함께 상세 설명을 포함하고 있습니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)  
- **가상화 도구:** GNS3 VM (QEMU)  
- **설치 대상:** Cisco ASAv 842  
- **활용 목적:** 보안 네트워크 포트폴리오 내 방화벽 테스트 구성  

---

## 📷 설치 및 설정 과정

### 1. ASA842.zip 다운로드 페이지 접속

- `asav_01_download_page.png`  
  [http://www.mediafire.com/download.php?l010dd0c1nayf0d](http://www.mediafire.com/download.php?l010dd0c1nayf0d) 접속 후 ASA842.zip 다운로드 

### 2. ASA842.zip 다운로드 진행

- `asav_02_download_progress.png`  
  ASA842.zip 다운로드 진행

### 3. 압축 해제

- `asav_03_extracted_files.png`  
  ASA842.zip을 압축해제하여 `asa842-initrd.gz`와 `asa842-vmlinuz` 파일 준비

---

### 4. GNS3 QEMU VM 템플릿 추가

- `asav_04_gns3_add_new_template.png`  
  GNS3 > Edit > Preferences > QEMU > QEMU VMs > New 클릭  
  "Run this Qemu VM on the GNS3 VM" 체크 → Next 클릭  

- `asav_05_qemu_vm_config_1.png`  
  Name에 `ASA` 등 입력 후 "This is a legacy ASA VM" 체크 → Next 클릭  

- `asav_05_qemu_vm_config_2.png`  
  Legacy ASA VM 경고화면 확인 → OK 클릭  

- `asav_05_qemu_vm_config_3.png`  
  QEMU binary : `/bin/qemu-system-x86_64 (v8.0.4)` 선택  
  RAM : 1024MB 선택 
  → Next 클릭  

- `asav_05_qemu_vm_config_4.png`  
  Console type을 Telnet으로 선택 → Next 클릭  

- `asav_05_qemu_vm_config_5.png`  
  Disk image에서 New Image 체크 후 빈칸 상태로 진행 → Next 클릭  

- `asav_05_qemu_vm_config_6.png`  
  Linux boot specific settings에서 New Image 클릭 후  
  3번 단계에서 압축 해제했던 파일 지정  
  - Initial RAM disk (initrd): `asa842-initrd.gz`  
  - Kernel image (vmlinuz): `asa842-vmlinuz`  
  설정 → Finish 클릭  

---

### 5. 템플릿 적용 및 확인

- `asav_06_qemu_vm_config_final.png`  
  QEMU VM Templates 화면에서 Apply 클릭 → OK 클릭  

---

### 6. 프로젝트에 ASA VM 배치 및 실행

- `asav_07_project_place_vm.png`  
  프로젝트에 `ASA-1` 배치 후 우클릭 → Start 클릭하여 가동  

- `asav_08_vm_boot_console.png`  
  `ASA-1` 더블 클릭하여 PuTTY로 접속 후 부팅 확인 

---

### 7. ASA 로그인 및 전역모드 진입가능 확인

- `asav_09_asav_login_prompt.png`  
  부팅 완료 후 전역 모드 진입
  - `enable` 명령어 입력  
  - 패스워드는 설정하지 않았기 때문에 `Password:` 프롬프트에서 그냥 Enter 입력  
  - 전역 모드 진입 완료  

---

## ✅ 설치 완료 및 준비 상태

- ASAv QEMU VM 정상 부팅 및 접속 확인  
- 보안 네트워크 포트폴리오 테스트 환경 구축 완료  

---

## 📎 참고 링크

- ASA842 다운로드: [http://www.mediafire.com/download.php?l010dd0c1nayf0d](http://www.mediafire.com/download.php?l010dd0c1nayf0d)  
- GNS3 공식: [https://gns3.com](https://gns3.com)  

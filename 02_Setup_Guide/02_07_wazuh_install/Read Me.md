# Wazuh 설치 및 GNS3 연동 가이드 (Rocky Linux 9.5 기반)

보안 운영 및 로그 관리 통합 플랫폼인 **Wazuh**를 Rocky Linux 9.5 환경에 설치하고, GNS3와 연동하여 보안 이벤트 모니터링 실습 환경을 구성하는 과정을 설명합니다.
본 문서는 VirtualBox에 Rocky Linux를 설치하고, **Wazuh**를 단일 서버 모드(All-in-One)로 구성한 후 GNS3와 연동하는 절차를 다룹니다.

---

## 📌 설치 개요

- **운영체제:** Windows 11 (Host)
- **가상화 도구:** VirtualBox
- **설치 대상:** Wazuh (Rocky Linux 9.5 Minimal)
- **활용 목적:** GNS3 보안 실습 환경에서 SIEM 구성 및 보안 이벤트 시각화

---

## 💻 설치 및 설정 과정

## 1️⃣ Rocky Linux ISO 다운로드

- `wazuh_01_download_rocky.png`
 Rocky Linux 공식 사이트의 Vault 경로에서 9.5 버전 minimal ISO 파일을 다운로드합니다.
 링크: https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/Rocky-9.5-x86_64-minimal.iso

 ---

 ### 2️⃣ VirtualBox에서 Wazuh용 가상머신 생성

- `wazuh_02_virtualbox_new_vm.png`
 VirtualBox에서 새 머신 생성 시 이름은 `Wazuh`, 종류는 `Linux`, 버전은 `Red Hat (64-bit)`로 설정합니다.

- `wazuh_03_vm_memory_cpu.png`
 메모리는 4096MB, CPU는 2개로 설정합니다.

- `wazuh_04_vm_disk_config.png`
 가상 디스크는 30GB로 새로 생성합니다.

- `wazuh_05_vm_complete.png`
 VM 생성 요약 화면을 확인하고 완료를 클릭합니다.

 ---

 ### 3️⃣ Wazuh VM 설정 조정

- `wazuh_06-01_vm_settings.png`
 부팅 순서를 하드디스크 → 광디스크 순으로 설정하고 체크합니다.

- `wazuh_06-02_vm_settings.png`
 시스템 → 프로세서에서 **PAE/NX 활성화** 옵션을 체크합니다.

- `wazuh_06-03_vm_settings.png`
 저장소 → IDE 컨트롤러 → 비어있음 클릭 → ISO 파일을 마운트합니다.

- `wazuh_06-04_vm_settings.png`
 네트워크 어댑터는 브리지 모드로 설정하고, 어댑터 활성화도 체크합니다.

 ---

 ### 4️⃣ Rocky Linux 설치

- `wazuh_07_Rocky_install_main.png`
 Rocky Linux 설치 화면에서 `Install Rocky Linux 9.5`를 선택하여 설치를 시작합니다.

- `wazuh_08_install_language.png`
 언어는 `한국어`로 설정하고 계속 진행합니다.

- `wazuh_09_install_disk.png`
 디스크는 자동 설정으로 지정합니다.

- `wazuh_10_install_root.png`
 루트 계정 비밀번호는 테스트용으로 `1234`로 설정하고 설치를 시작합니다.

- `wazuh_11_install_progress.png`
 설치가 진행되는 화면입니다.

- `wazuh_12_install_complete.png`
 설치가 완료되면 시스템을 재부팅합니다.

- `wazuh_13_first_boot_login.png`
 재부팅 후 첫 로그인 프롬프트 화면입니다.

 ---

 ### 5️⃣ Wazuh 설치 스크립트 실행

- `wazuh_14_download_script.png`
 설치 스크립트를 다운로드합니다:
 `curl -sO https://packages.wazuh.com/4.8/wazuh-install.sh`


- `wazuh_15_chmod_script.png`
 실행 권한을 부여합니다:
 `chmod +x wazuh-install.sh`


- `wazuh_16_install_start.png`
 설치를 시작합니다 (All-in-One 모드):
 `sudo ./wazuh-install.sh --all-in-one --ignore-check`


- `wazuh_17_install_progress.png`
 설치 진행 중 화면입니다.

- `wazuh_18_install_complete.png`
 설치가 완료된 화면입니다.

 ---

### 6️⃣ Wazuh 서비스 상태 확인 및 방화벽 설정

- `wazuh_19_wazuh_active.png`
 다음 명령어로 주요 서비스가 활성 상태인지 확인하고 부팅 시 자동 실행 설정을 합니다:

 `sudo systemctl status wazuh-manager`
 `sudo systemctl status wazuh-indexer`
 `sudo systemctl status wazuh-dashboard`
 `sudo systemctl status filebeat`

 `sudo systemctl enable wazuh-manager`
 `sudo systemctl enable wazuh-indexer`
 `sudo systemctl enable wazuh-dashboard`
 `sudo systemctl enable filebeat`


- `wazuh_20_firewall_add.png`
 HTTPS 서비스를 방화벽에 허용합니다:
 `sudo firewall-cmd --permanent --add-service=https`


- `wazuh_21_firewall_reload.png`
 방화벽 설정을 반영합니다:
 `sudo firewall-cmd --reload`

 ---

### 7️⃣ Wazuh Dashboard 접속

- `wazuh_22_web_dashboard.png`
 웹 브라우저에서 다음 주소로 접속합니다:
 `https://<서버IP>:443`

- `wazuh_23_web_login.png`
 로그인 정보:
 아이디: `admin`
 비밀번호: 설치 완료 시 출력된 초기 비밀번호 입력
 로그인 후 Wazuh 대시보드를 확인할 수 있습니다.

 ---

### 8️⃣ GNS3 연동 테스트

- `wazuh_24_gns3_vm_add.png`
 GNS3 → Edit → Preferences → VirtualBox → VirtualBox VMs → New
 `Run this VirtualBox VM on my local computer` 선택 후, VM 리스트에서 Wazuh 선택 → Finish

- `wazuh_25_gns3_project_test.png`
 GNS3 프로젝트에 Wazuh VM을 추가하고 우클릭 → Start 실행하여 VirtualBox와의 연동이 정상적으로 이루어지는지 확인합니다.

 ---

 ## ✅ 설치 완료 및 준비 상태

- Rocky Linux 9.5 기반 Wazuh 설치 완료
- All-in-One 모드로 Manager, Indexer, Dashboard 구성
- 방화벽 및 서비스 설정 완료
- GNS3와 연동을 통한 보안 실습 환경 구축 완료

---

## 📎 참고 링크

- Wazuh 공식 문서:
 [https://documentation.wazuh.com](https://documentation.wazuh.com) 
- Rocky Linux ISO 다운로드:
 [https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/](https://dl.rockylinux.org/vault/rocky/9.5/isos/x86_64/)
- GNS3 공식 웹사이트:
[https://gns3.com](https://gns3.com)
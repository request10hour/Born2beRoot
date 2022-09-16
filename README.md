# Born2beRoot

## Project overview
1. How a virtual machine work
[가상 머신이란? | VMware 용어집 | KR](https://www.vmware.com/kr/topics/glossary/content/virtual-machine.html)
**가상 머신이란?**
**가상 머신**(또는 게스트)은 호스트라고 하는 컴퓨팅 환경에서 생성됩니다. 하나의 호스트에 여러 가상 머신이 동시에 존재할 수 있습니다. 가상 머신을 구성하는 주요 파일에는 로그 파일, NVRAM(비휘발성 RAM) 설정 파일, 가상 디스크 파일, 구성 파일 등이 있습니다.
**가상 머신 정의**
가상 머신은 물리적 컴퓨터와 동일한 기능을 제공하는 소프트웨어 컴퓨터입니다. 가상 머신은 물리적 컴퓨터처럼 애플리케이션과 운영 체제를 실행합니다. 그러나 가상 머신은 물리적 컴퓨터에서 실행되고 물리적 컴퓨터처럼 작동하는 컴퓨터 파일입니다. 다시 말해 가상 머신은 별도의 컴퓨터 시스템처럼 작동합니다.
[하이퍼바이저란? | VMware 용어집 | KR](https://www.vmware.com/kr/topics/glossary/content/hypervisor.html)
**하이퍼바이저란?**
가상 머신 모니터라고도 하는  **하이퍼바이저**는 가상 머신(VM)을 생성하고 실행하는 프로세스입니다. 하이퍼바이저는 메모리 및 처리와 같은 단일 호스트 컴퓨터의 리소스를 가상으로 공유하여 호스트 컴퓨터가 여러 게스트 가상 머신을 지원할 수 있도록 합니다.

2. Their choice of operating system.
`head -n 2 /etc/os-release` 명령어로 확인
Debian을 선택함 확인
3. The basic differences between CentOS and Debian.
**아키텍처** - AArch64/ARM64, i386 ...등의 유명한 아키텍처는 양쪽 모두 지원
CentOS 7은 POWER9,
Debian은 MIPSel, MIPS64el, s390x
**패키지 관리** - CentOS는 YUM/DNF를 사용하고,
Debian은 dpkg/APT를 사용한다.
**파일 시스템** - CentOS에선 ZFS 파일시스템 미지원...큰 차이는 없다.
**커널** -  2021년 기준 자료여서 달라졌을지도 모르지만...데비안이 보다 최신 커널을 사용한다
**업그레이드** - CentOS는 마이너 업데이트 가능 (  7 -> 7.8, 7.9 ) 메이저 업데이트 불가능 ( 7 -> 8 )
Debian은 메이저 업데이트 가능
**지원** - Debian이 커뮤니티 지원이 많아서 초보자가 쓰기 좋다? (제대로 번역한건지 확실하지않음)
4. The purpose of virtual machines.
[가상 머신이란? | VMware 용어집 | KR](https://www.vmware.com/kr/topics/glossary/content/virtual-machine.html)
가상 머신은 바이러스에 감염된 데이터에 액세스하고 운영 체제를 테스트하는 등, 호스트 환경에서 수행하기에 위험한 특정 작업을 수행하기 위해 생성됩니다. 가상 머신은 다른 시스템에서 sandbox화되므로, 가상 머신 내의 소프트웨어는 호스트 컴퓨터를 변조할 수 없습니다. 가상 머신은 서버 가상화 등의 다른 목적으로도 사용할 수 있습니다.
5. Debian: the difference between aptitude and apt, and what APPArmor is.
Debian의 기본 패키지 관리자는 **dpkg**이다. 한 가지 프로그램을 설치하려면 딸려오는 종속성 목록이 함께 제공되는데, 이걸 모두 수동으로 설치하는 방법이 있다.
**APT**(고급 패키지 도구)를 사용하면 프로그램의 모든 종속성을 자동으로 설치해준다.
**Aptitude**는 비교적 종속성 제어에 유용하다. 사용자가 프로그램 설치시 종속성을 선택할 수 있다...?<br>
**APPArmor**
AppArmor는 MAC(필수 액세스 제어) 보안을 제공한다. 시스템 관리자는 프로세스가 수행하는 작업을 제한할 수 있다. enforce-mode / complain-mode 두가지 프로필로 작동한다.
"enforce-mode" - 작업 자체를 제한, 금지
"complain-mode" - 작업 허용, complain 메시지 표시

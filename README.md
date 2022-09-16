# Born2beRoot

## Project overview
1. How a virtual machine work<br>
[가상 머신이란? | VMware 용어집 | KR](https://www.vmware.com/kr/topics/glossary/content/virtual-machine.html)<br>
**가상 머신이란?**<br>
**가상 머신**(또는 게스트)은 호스트라고 하는 컴퓨팅 환경에서 생성됩니다. 하나의 호스트에 여러 가상 머신이 동시에 존재할 수 있습니다. 가상 머신을 구성하는 주요 파일에는 로그 파일, NVRAM(비휘발성 RAM) 설정 파일, 가상 디스크 파일, 구성 파일 등이 있습니다.<br>
**가상 머신 정의**<br>
가상 머신은 물리적 컴퓨터와 동일한 기능을 제공하는 소프트웨어 컴퓨터입니다. 가상 머신은 물리적 컴퓨터처럼 애플리케이션과 운영 체제를 실행합니다. 그러나 가상 머신은 물리적 컴퓨터에서 실행되고 물리적 컴퓨터처럼 작동하는 컴퓨터 파일입니다. 다시 말해 가상 머신은 별도의 컴퓨터 시스템처럼 작동합니다.<br>
[하이퍼바이저란? | VMware 용어집 | KR](https://www.vmware.com/kr/topics/glossary/content/hypervisor.html)<br>
**하이퍼바이저란?**<br>
가상 머신 모니터라고도 하는  **하이퍼바이저**는 가상 머신(VM)을 생성하고 실행하는 프로세스입니다. 하이퍼바이저는 메모리 및 처리와 같은 단일 호스트 컴퓨터의 리소스를 가상으로 공유하여 호스트 컴퓨터가 여러 게스트 가상 머신을 지원할 수 있도록 합니다.

2. Their choice of operating system.<br>
`head -n 2 /etc/os-release` 명령어로 확인<br>
Debian을 선택함 확인
3. The basic differences between CentOS and Debian.<br>
**아키텍처** - AArch64/ARM64, i386 ...등의 유명한 아키텍처는 양쪽 모두 지원<br>
CentOS 7은 POWER9, Debian은 MIPSel, MIPS64el, s390x<br>
**패키지 관리** - CentOS는 YUM/DNF를 사용하고, Debian은 dpkg/APT를 사용한다.<br>
**파일 시스템** - CentOS에선 ZFS 파일시스템 미지원...큰 차이는 없다.<br>
**커널** -  2021년 기준 자료여서 달라졌을지도 모르지만...데비안이 보다 최신 커널을 사용한다<br>
**업그레이드** - CentOS는 마이너 업데이트 가능 (  7 -> 7.8, 7.9 ) 메이저 업데이트 불가능 ( 7 -> 8 )<br>
Debian은 메이저 업데이트 가능<br>
**지원** - Debian이 커뮤니티 지원이 많아서 초보자가 쓰기 좋다? (제대로 번역한건지 확실하지않음)<br>
4. The purpose of virtual machines.<br>
[가상 머신이란? | VMware 용어집 | KR](https://www.vmware.com/kr/topics/glossary/content/virtual-machine.html)<br>
가상 머신은 바이러스에 감염된 데이터에 액세스하고 운영 체제를 테스트하는 등, 호스트 환경에서 수행하기에 위험한 특정 작업을 수행하기 위해 생성됩니다. 가상 머신은 다른 시스템에서 sandbox화되므로, 가상 머신 내의 소프트웨어는 호스트 컴퓨터를 변조할 수 없습니다. 가상 머신은 서버 가상화 등의 다른 목적으로도 사용할 수 있습니다.
5. Debian: the difference between aptitude and apt, and what APPArmor is.<br>
Debian의 기본 패키지 관리자는 **dpkg**이다. 한 가지 프로그램을 설치하려면 딸려오는 종속성 목록이 함께 제공되는데, 이걸 모두 수동으로 설치하는 방법이 있다.<br>
**APT**(고급 패키지 도구)를 사용하면 프로그램의 모든 종속성을 자동으로 설치해준다.<br>
**Aptitude**는 비교적 종속성 제어에 유용하다. 사용자가 프로그램 설치시 종속성을 선택할 수 있다...?<br>
**APPArmor**
AppArmor는 MAC(필수 액세스 제어) 보안을 제공한다. 시스템 관리자는 프로세스가 수행하는 작업을 제한할 수 있다. enforce-mode / complain-mode 두가지 프로필로 작동한다.<br>
"enforce-mode" - 작업 자체를 제한, 금지<br>
"complain-mode" - 작업 허용, complain 메시지 표시<br>

## Simple setup
A password will be requested before attempting to connect to this machine. This user must not be root.
1. Check that the UFW service is started.<br>
`sudo ufw status`<br>
4242포트로 열려있는지 확인
2. Check that the SSH service is started.<br>
`sudo systemctl status ssh`<br>
active 상태인지 확인, 4242포트로 listening인지 확인
3. 	Check that the chosen operating system is Debian or CentOS.<br>
`cat /etc/os-release`<br>
Debian에서 구동중인지 확인

## User
The subject requests that a user with the login of the student being evaluated is present on the virtual machine. Check that it has been added and that it belongs to the sudo and user42 groups.<br>
`sudo adduser <username> <group = sudo, user42>`<br>미리 해놨어야하고 `groups`로 확인하면 sudo 및 user42그룹에 속해있는지 확인가능
1. First, create a new user.<br>
`cut -d ':' -f1 /etc/passwd`<br>
유저목록 확인<br>
`sudo adduser <username>`<br>
"adduser \<username>"을 하면 username이름의 유저 및 그룹이 자동으로 생성됨. 비번만 입력하고 나머지 응답은 엔터로 스킵<br>
`cut -d ":" -f1 /etc/passwd`<br>
유저 생성됨 확인
2. Assign it a password of your choice.<br>
**1번에서 함.**<br>
adduser를 하면 비번까지 일사천리로 되고, useradd를 하면 비번을 `sudo passwd <username>`으로 따로 설정해줘야 함. 비번설정안하면 해당 유저로 로그인안됨...
3. Normally there should be one or two modified files.<br>
`sudo vim /etc/login.defs`<br>
`sudo vim /etc/security/pwquality.conf`<br>
위의 두가지 파일을 수정했을것임
	```vim
	# /etc/login.defs

	PASS_MAX_DAYS 30
	PASS_MIN_DAYS 2
	PASS_WARN_AGE 7
	```
	```vim
	# /etc/security/pwquality

	defok = 7
	minlen = 10
	dcredit = -1
	ucredit = -1
	maxrepeat = 3
	gecoscheck = 1
	usercheck = 1
	enforce_for_root
	```
4. 	Create a group named evaluating in front of you and assign it to this user.<br>
`sudo addgroup evaluating`<br>
'evaluating' 그룹을 추가<br>
`cut -d ":" -f1 /etc/group`<br>
그룹 목록 확인<br>
`sudo adduser <username> evaluating`<br>
user를 'evaluating' 그룹에 추가<br>
~~`sudo deluser <username> <group>`<br>
user를 그룹에서 제외~~
5. Check that this user belongs to the evaluating group.<br>
user로 로그인해서 `groups` 명령어 치면 됨

(무언가 확인하다가 출력되는 내용이 너무 길면 명령어 뒤에 ` | less` 를 붙이자)

## Hostname and partitions
1. The hostname is .login42<br>
`hostname`
2. Modify this hostname by replacing the login with yours, then restart the machine.<br>
변경 : `(sudo) hostname <hostname>` <br>
확인 : `hostname`
3. 	Restore the machine to the original hostname.<br>
변경 : `(sudo) hostname <login42>` <br>
확인 : `hostname`
4. 	How to view the partitions for this virtual machine. <br>
`lsblk` - list block devices
5. How LVM works and what it is all about.<br>
**LVM(논리 볼륨 관리자)** - 파티션이 하나의 물리 저장 장치 내부에 국한되어지지 않아서 용량을 유연하게 사용 가능하게 해줌<br>
**PV(물리 볼륨)** - 물리적 저장 장치. HDD, USB... 등<br>
**VG(볼륨 그룹)** - PV를 묶어서 만든 가상 스토리지 디스크<br>
**LV(논리 볼륨)** - 가상 스토리지 디스크인 VG 내부에 생성된 파티션<br>
- LVM : PV를 묶어서 VG를 만들고 LV로 나누어 사용

## SUDO
1.

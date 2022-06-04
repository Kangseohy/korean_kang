___
### top명령어
top(table of processes)은 현재 CPU의 사용량, 메모리 사용률 등을 확인해줍니다. 
리눅스 서버의 성능과 어떤 프로세스가 CPU를 많이 잡아먹고 있는지 확인가능하다.

top 명령어 출력 결과

* 출력 결과의 맨 윗단

현재 서버의시간, 켜져있는 시간, 유저, load average, Tasks(프로세스 개수)

CPU |설명
---|---|
%us | user에서 사용하고 있는 CPU 비중
%sy | 시스템에서 사용중인 CPU 비중
%id | 유휴 상태인 CPU 비중
%wa | I/O 요청을 처리하지 못한 상태의 CPU idle 상태 비중

KiB Mem, Swap은 각 메모리의 상태 정보를 나타냄

* 출력 결과의 아랫단

프로세스 상태 정보 | 설명
---|---|
PID | 프로세스 ID|
USER | 프로세스를 실행시킨 사용자 ID
PRI | 프로세스의 우선순위|
NI | 일의 nice value **nice value가 낮으면 우선순위가 높다.**
VIRT | 가상 메모리 사용량
RES | 현재 페이지가 상주하고 있는 크기
SHR | 분할된 페이지, 프로세스에 의해 사용된 메모리를 나눈 메모리 총합
S | 프로세스 상태 EX)sleeping, running, swapped out process, zombies
%CPU | 프로세스가 사용하는 CPU 사용율
%MEM | 프로세스가 사용하는 메모리 사용율
COMMAND | 실행된 명령어

* top을 실행 하기 전의 옵션

옵션 |설명
---|---|
-b | 찰나의 정보를 확인하기 위해서|
-n | top의 실행 주기를 설정

* top 실행 후 명령어

top 실행 후 명령어 | 설명|
---|---|
shift+m | 메모리 사용률(내림차순)|
shift+t | 프로세스가 작동중인 시간 순대로|
shift+p | CPU 사용률(내림차순)|
k | kill k를 입력하고 PID의 번호를 씀 signal은 9임|
a | 메모리 사용량에 따라 정렬해줌
f | sort field 선택화면 q를 누르면 RES순으로 정렬해줌
b | Batch모드
1 | CPU 코어별 사용량을 보여줌

___

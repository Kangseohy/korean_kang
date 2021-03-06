___
20213009 컴퓨터공학과 강서현
### top명령어

* top설명 
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

* ps와 top차이점

1) ps는 ps를 한 시점부터 proc에서 검색한 cpu 사용량을 출력해줌
2) top은 proc에서 일정 주기로 합산해서 cpu 사용량을 나타냄
___

### ps

* ps 설명
**ps** 현재 실행중인 프로세스의 목록을 보는 명령어다. 

* ps옵션

ps옵션 | 설명
---|---|
-e | 실행중인 모든 프로세스 정보를 출력|
-f | 프로세스에 대한 자세한 정보 출력(PPID확인 가능)|
-u [사용자 이름]| 특정 사용자에 대한 모든 프로세스의 정보를 출력|
-p pid | pid로 지정한 프로세스의 정보를 출력|
u | 프로세스의 소유자 이름, CPU 사용량, 메모리 사용량 등등 상세정보 출력|
a | 터미널에서 실행한 프로세스 정보 출력|
x | 실행중인 모든 프로세스 정보 출력|

***ps를 옵션없이 쳐보기***

>PID(프로세스 번호), TTY(터미널 번호), TIME(해당프로세스가 실행한 CPU양), CMD(프로세스가 실행중인 명령)순이다.

***ps를 옵션 -f와 함꼐치면 더 상세한 정보를 출력해주는데 PPID도 출력해줌***

>옵션없이 쳐봤던 것에서 -f 했을 때 추가된 것은
>UID(프로세스를 실행한 사용자 ID), PPID(부모프로세스번호), C(CPU사용량퍼센트), STIME(프로세스 시작시간) 등이 추가로 출력된다.
___

### jobs

* jobs설명

>다음의 프로세스 목록을 출력해주는 명령
>백그라운드로 실행중인 프로세스, 현재 중지된 프로세스 

* 사용법

> ***jobs [option] [작업번호]***

* 옵션

옵션 | 설명
---|---|
-l | 프로세스 그룹 ID를 state 필드 앞에 출력|
-n | 프로세스 그룹 중 대표 프로세스 ID를 출력|
-p | 각 프로세스 ID에 대해 한 행씩 출력|
command | 지정한 명령어 실행|

* jobs로 출력되는 백그라운드 작업의 상태값

상태값 | 설명|
---|---|
Running| 작업이 계속 진행중|
Done | 작업이 완료되어 0 반환|
Done(code)|작업이 종료되었으며 0이 아닌 코드 반환|
Stopped| 작업 일시 중단|
___

### kill

* kil설명
>프로세스에 특정한 시그널(signal)을 보내는 명령. ***옵션없이 실행***하면 프로세스에 종료신호(15, TERM, SIGTERM)을 보냄. 보통 중지 시킬 수 없는 프로세스를 종료시키고자 할 때 

* 사용법
>***kill [option] [signal] [PID 또는 %job번호]*** 

* 옵션

옵션|설명
---|---|
-l|시그널 종류 출력|
-s signal|시그널 이름 지정|

* 사용예시

kill 523
>설명: PID가 523인 프로세스에 기본 시그널 15를 보냄 kill -15 523, kill -TERM 523, kill -s SIGTERM 523와 같음

kill -9 723 747 758
>설명: PID가 723, 747, 758인 프로세스를 ***강제 종료***, kill -KILL PID, kill -SIGKILL PID와 같음

kill -l 10119
>설명: PID가 10119인 프로세스 ***재시작***

kill 1
>설명: ***작업 번호***가 1인 프로세스 종료
___

### vim에서 매크로 사용법 (q,@)

***매크로 실행하는 법***
1) 명령모드에서 q[Name]을 입력하면 아래 기록중 이라고 뜬다. [Name]에 들어갈 것은 아무거나 한글자 정해서 입력하면 된다. 예를 들어 o을 쳤다고 하자 그럼 qo를 입력하여 시작한 것이다.
2) 그럼 매크로가 시작된것이고 매크로를 실행시켰을 때 어떤 동작을 실행할지를 바로 이단계에서 만들어 놓아야 한다. 만드는 동안 실수를 했다면 :u로 작업 되돌리기를 해가면서 하면 된다.
3) 위에서 다 만들었다면 매크로가 끝났다는 의미로 q를 입력하면 o라는 매크로가 완성된다.
4) 이제 등록된 매크로를 실행시키는 단계이다. 방법은 @[Name]이다. 여기서는 [Name]을 o로 설정했기에 @o하면 아까 했던 2번에서 만든 일련의 동작을 자동으로 실행해준다. 그러나 @[Name]은 매크로를 한번만 실행해준다.
5) 만약 매크로를 실행하는데에 있어서 여러번 실행하고 싶다면 [숫자]@[Name]을 해줘야한다. 이렇게하면 숫자에 들어간 만큼 매크로를 실행하게 된다. 예를들어서 16@o라고 치면 2번에서 만든 동작을 16번 실행해준다.

---

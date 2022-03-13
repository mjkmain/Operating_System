# 한밭대학교 운영체제 (임경태 교수) Linux 명령어 실습 

### 
```bash
$ [입력] #주석(설명)

>> [출력 결과]
```
#
### 1. pwd 
(**P**rint **W**orking **D**irectory)
### 현재 위치한 디렉토리 확인

```bash
$ pwd

>> /home/username
```
#
### 2. mkdir [directory name]
(**M**a**k**e **dir**ectory)
```bash
$ mkdir test1 #test1이라는 디렉토리 생성
```
###
```bash
$ mkdir test1/test2 #test1이라는 디렉토리 안에 test2 디렉토리 생성
```
#
### 3. ls [option] &nbsp; &nbsp; *<options : -a(all), -l(long)>*
(**L**ist **S**egments)
```bash
$ ls #현재 작업 디렉토리 안의 내용물 이름 출력 
>> test1
```
 
###
```bash
$ ls -a #숨겨진 파일, 디렉토리도 출력
>> .  ..  .bash_history  .bash_logout  .bashrc  .gnupg  .profile  .ssh  test1
```

###
```bash
$ ls -l #자세한 내용(권한, 소유자, 그룹 등) 출력
>> total 4
>> drwxr-xr-x 2 mjkmain22 mjkmain22 4096 Mar 13 08:37 test1
#[파일유형+권한] [링크 수] [소유자] [그룹] [크기] [마지막 수정 시간] [이름]
```
### 
![image](https://user-images.githubusercontent.com/72269271/158052121-968599fd-4ca5-4777-af0d-fea439bda129.png)
* 1영역 : 파일 종류 <일반 파일(-), 디렉토리(d) 등>, &nbsp; 현재는 directory이기 때문에 "d"
* 2영역 : 접근 모드 <read(r), write(w), excute(x)>
* 3영역 : 해당 파일, 디렉토리에 연결된 링크의 수 
* 4영역 : 소유자
* 5영역 : 그룹
* 6영역 : 파일, 디렉토리 크기(Byte)
* 7영역 : 최종 수정 시간
* 8영역 : 파일, 디렉토리 이름



#
### 4. cd [path]
(**C**hange **D**irectory)

- 실습 진행 하면서 pwd로 현재 위치 확인하는 것을 추천

```bash
$ cd test1 #test1 디렉토리로 이동
```

```bash
$ cd .. #이전 디렉토리로 이동
```

```bash
$ cd test1/test2 #test1 디렉토리 안에 있는 test2 디렉토리로 이동
```

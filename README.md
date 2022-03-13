## 한밭대학교 운영체제 (임경태 교수) Linux 명령어 실습 

### 
```bash
~$ [입력] #주석(설명)

>> [출력 결과]
```
- - -
# 1. 디렉토리 관련 명령어 
### 1-1. pwd 
(**P**rint **W**orking **D**irectory)
### 현재 위치한 디렉토리 확인

```bash
~$ pwd

>> /home/username
```
#
### 1-2. mkdir [option] [directory name]
(**M**a**k**e **dir**ectory)
### 디렉토리 생성

```bash
~$ mkdir test1 #test1이라는 디렉토리 생성
```
###
```bash
~$ mkdir test1/test2 #test1이라는 디렉토리 안에 test2 디렉토리 생성
```
#
### 1-3. ls [option] &nbsp; &nbsp; *<options : -a(all), -l(long)>*
(**L**ist **S**egments)
### 현재 디렉토리 내의 내용물 출력
```bash
~$ ls #현재 작업 디렉토리 안의 내용물 이름 출력 
>> test1
```
 
###
```bash
~$ ls -a #숨겨진 파일, 디렉토리도 출력
>> .  ..  .bash_history  .bash_logout  .bashrc  .gnupg  .profile  .ssh  test1
```

###
```bash
~$ ls -l #자세한 내용(권한, 소유자, 그룹 등) 출력
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

###



#
### 1-4. cd [path]
(**C**hange **D**irectory)
### 디렉토리 변경
###
- 실습 진행 하면서 pwd로 현재 위치 확인하는 것을 추천

```bash
~$ cd test1        #test1 디렉토리로 이동
```

```bash
~/test1$ cd ..     #이전 디렉토리로 이동
```

```bash
~$ cd test1/test2  #test1 디렉토리 안에 있는 test2 디렉토리로 이동
```

```bash
~/test1/test2$ cd ~ #root 디렉토리로 이동
```
#
### 1-5. rmdir [directory name]
(**R**e**m**ove **dir**ectory)
### 디렉토리 삭제
~~~bash
~$ cd test1          #test1 디렉토리로 이동
~/test1$ ls          #하위 폴더, 파일이름 출력
>> test2
~/test1$ rmdir test2 #test2 디렉토리 삭제
~/test1$ ls          #삭제된 모습 확인
~~~

#
Appendix) tree 구조 출력하기
~~~bash
~$ sudo apt-get install tree #sudo(관리자 권한)으로 tree install, 최초 1회만 하면 됨
~$ tree
>> .         #여기에서 .은 현재 디렉토리를 의미
   └── test1
~~~


#
### 1-6. mv [option] [file name] [destination] 
#### (mv [옵션] [이동 할 파일/디렉토리] [이동 될 위치])
(**m**o**v**e)
### 파일/디렉토리 이동

~~~bash
~$ mkdir test3
~$ ls
>> test1 test3

~$ tree
# 현재 디렉토리 구조

# .
# ├──── test1
# └──── test3

~$ mv test3 test1 #test3 디렉토리를 test1 안으로 이동
~$ ls
>> test1

~$ cd test1
~$ ls
>> test3

~$ tree
# 이동 후 디렉토리 구조

# .
# └──── test1
#       └──── test3
~~~
#

### 1-7. cp [option] [file name] [destination] &nbsp; &nbsp; *<options : -i(interactive), -r(recursive), >*
#### (cp [옵션] [복사 할 파일/디렉토리] [복사 될 위치]
(**c**o**p**y)
### 파일/디렉토리 복사



###
~~~bash
~$ tree 

# 현재 디렉토리 구조

# .
# └──── test1
#       └──── test3

~$ mkdir test_cp
~$ tree

# .
# ├── test1
# │   └── test3
# └── test_cp

~$ cp -r test_cp test1 # option : -r (recursive) 디렉토리를 복사할 때 사용 (재귀적 복사)
                       # -r 옵션을 사용하여 test_cp라는 디렉토리를 test1 디렉토리 안에 복사
~$ tree

# .
# ├── test1
# │   ├── test3
# │   └── test_cp
# └── test_cp

~$ cp -r test_cp test1/test3 # -r 옵션을 사용하여 test_cp라는 디렉토리를 test1/test3 디렉토리 안에 복사
~$ tree

# .
# ├── test1
# │   ├── test3
# │   │   └── test_cp
# │   └── test_cp
# └── test_cp
~~~
### cp 명령어 옵션 (자주 사용하는 것)
-i : 동일한 파일이 존재하면 덮어쓸 지 묻는다.
-r : 하위 디렉토리 및 파일까지 복사한다.
-a : 파일의 속성까지 복사한다(권한 등)
- - -

# 2. 파일 관련 명령어 

~~~bash
# 파일 관련 명령어 시작하기 전에 파이썬 설치 하겠습니다.
sudo apt-get install python #sudo(관리자 권한) 사용하여 파이썬 설치, 최초 1회만 하면 됨
~~~


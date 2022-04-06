# 한밭대학교 운영체제 (임경태 교수) Linux 명령어 실습 

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
~$ sudo apt-get install python #sudo(관리자 권한) 사용하여 파이썬 설치, 최초 1회만 하면 됨
~~~

### 2-1 touch [file name]
### 빈 파일을 생성한다

~~~bash
~$ ls
>> test1 test_cp

~$ touch os_class.py
>> os_class.py test1 test_cp
~~~
#
### 2-2 vi [file name]
### 파일열기, 작성 (편집기)
~~~bash
~$ vi os_class.py
>> 편집 모드로 변경
~~~

#### 2-2-1. 편집 모드
* 초기 상태 : Normal mode  
  
* i 입력 --> insert mode (입력 모드)  

~~~python
print("Hello world")

name = "mjkim"
print(name)
~~~

* esc 입력 --> Normal mode (일반 모드, 초기 상태)  
* : 입력 --> Command mode (명령 모드)
###
* 명령 모드에서 wq 입력 (저장 후 종료)

#### 2-2-2. vi편집기로 작성한 내용 확인
~~~bash
~$ python os_class.py #python 파일을 실행시킴
>> Hello World
>> mjkim
~~~

### 2-3. cat [file name]
### 파일의 내용물 출력
~~~bash
~$ cat os_class.py
>> print("Hello World")
>>
>> name = "mjkim"
>> print(name)
~~~
###
- - -
- - -
- - -
# 과제
### "디렉토리 구조" 는 트리 형식을 의미합니다.
###
1. 현재 위치를 확인한다. 현재 위치가 home/[username] 이 아니면 home/[username]으로 이동한다. 여기서 [username]은 각자의 구글 아이디이다.
2. 실습을 위한 디렉토리를 만든다. 먼저 home/[username]에 os_assignment 디렉토리를 만들고 이동한다. 앞으로의 모든 실습은 이 디렉토리 안에서 진행한다.
3. 3주차 실습이니 week3라는 디렉토리를 만들고 week3로 이동한다. 
4. os_assignment 디렉토리 안에 week4, week5, week6 디렉토리를 동시에 만든다. os_assignment **디렉토리 구조**를 출력한다. 
~~~bash
#hint - 동시에 여러 디렉토리 만들기
~$ mkdir a b c
~$ ls
>> a b c
~~~
5. 현재 위치를 이동하지 않고 week3 디렉토리 안에 tmp/test 디렉토리를 만든 후 **디렉토리 구조**를 출력한다.

* ***hint : mkdir -p 옵션 구글링***

6. test디렉토리로 한 번에 이동한 후 현재 위치를 출력한다.
7. test디렉토리에 학번.py 파일을 생성한 후 test 디렉토리의 목록을 출력한다. (파일 이름 예시 : 20181111.py) 
8. 생성된 python파일에 편집기를 사용하여 다음의 내용을 추가한다.
~~~python
id = 20181111 #본인 학번
name = "yourname" #본인 이름

print(id, name)
~~~

9. 만들어진 학번.py 파일을 python으로 실행시킨다.
10. 만들어진 학번.py 파일의 내용물을 출력한다.
11. os_assignment로 다시 이동하여 디렉토리의 권한, 소유자, 그룹 등을 출력한다.
12. os_assignment의 최종 디렉토리 구조를 출력한다.

#### 최종 디렉토리 구조 
![image](https://user-images.githubusercontent.com/72269271/158065258-5e7b5eac-97b3-4271-9d9c-8163979af007.png)

- - -

#
# grep 명령어
### 옵션
#### -a : grep는 바이너리 형식의 파일을 처리할 수 없기 때문에 binary파일을 텍스트파일처럼 처리할 수 있게 해주는 옵션
#### -b : 패턴과 일치하는 줄의 시작점을 출력
#### -c : 패턴과 일치하는 줄의 개수를 출력
#### -h : 여러 개의 파일을 검색 시 출력하는 파일의 이름이 붙는 것을 방지
#### -i : 검색할 때 대소문자를 구분하지 않음
#### -n : 패턴과 일치하는 줄의 번호와 내용을 같이 출력
#### -v : 패턴과 일치하지 않는 줄을 출력
#### -w : 패턴과 한 단어로 일치해야 출력
#### -x : 패턴과 한 줄로 일치해야 출력
#### -l : 주어진 패턴과 일치하는 패턴이 있는 파일의 이름만 출력한 

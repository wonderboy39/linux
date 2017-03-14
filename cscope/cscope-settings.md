#cscope 사용법  
##1. 기본 설정  
#####1) cscope 설치  
만약 설치되어 있지 않다면  
```{.bash}
$ apt-get install cscope  
```

#####2) cscope빌드 스크립트(mkcscope.sh)생성  
cscope.files를 생성할 프로젝트의 root디렉터리에 mkcscope.sh를 생성  
```{.bash}
$ cd jlt620trunk  
$ vim mkcscope.sh  
```

아래의 내용을 입력한다.  
```{.bash}
find . \( -name '*.c' -o -name '*.cpp' -o -name '*.cc' -o -name '*.h' -o -name '*.h' -o -name '*    .s' -o -name '*.S' \) -print > cscope.files

cscope -i cscope.files  
```

스크립트의 권한을 755로 변경  
```{.bash}
$ chmod 755 mkcscope.sh  
```

#####3) vimrc의 내용 변경  
```{bash}
csprg=/usr/bin/cscope
set csto=0(숫자 0)
set cst
set nocsverb

if filereadable("./cscope.out")
	cs add cscope.out
else
	cs add /usr/src/linux/cscope.out
endif
set csverb
```

#####4) CSCOPE 사용
```{.bash}
$ cscope -d
```

##2. 고급 설정
#####1) CSCOPE 옵션들
-b : tells Cscope to just build the database, and not launch the CSCOPE GUI.  
-q : causes an additional "inverted index" file to be created, which makes searches run much faster for large database.  
-k : CSCOPE의 kernel모드 - it will not look in /usr/include for any header files that are #included in your source files (this is mainly useful when you are using Cscope with operation system and/or C Library source code, as we are here.)  

##3. 단축키들
* Ctrl + ] : directly jump to symbol  
* Ctrl + t : jump back to your original location before the search  
* Ctrl + \ : cs find 명령어와 같은 역할
  (Ctrl + \를 누른 후에 빠르게 s를 누르면 아래에 해당 커서에 대해 사용된 모든 심볼들이 나타난 Vim window가 나타난다)  

* Ctrl + @ : scs find  
* Ctrl + @ Ctrl + @ (두번 누를때 ) : vert cs find  

##4. 참고자료
https://a0gustinus.wordpress.com/2013/06/01/browsing-source-code-in-linux-vimcscope/





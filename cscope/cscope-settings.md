# cscope 사용법  
## 1. 기본 설정  
##### 1) cscope 설치  
만약 설치되어 있지 않다면  
```{.bash}
$ apt-get install cscope  
```

##### 2) cscope빌드 스크립트(mkcscope.sh)생성  
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

##### 3) vimrc의 내용 변경  
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

##### 4) CSCOPE 사용
```{.bash}
$ cscope -d
```

## 2. 고급 설정
##### 1) CSCOPE 옵션들
-b : tells Cscope to just build the database, and not launch the CSCOPE GUI.  
-q : causes an additional "inverted index" file to be created, which makes searches run much faster for large database.  
-k : CSCOPE의 kernel모드 - it will not look in /usr/include for any header files that are #included in your source files (this is mainly useful when you are using Cscope with operation system and/or C Library source code, as we are here.)  

##### 2) CSCOPE 플러그인을 설치해서 단축키등을 설정하기  
위에 정리한 내용은 작업 디렉터리 내에 cscope.files를 mkcsope.sh를 통해 생성하고나서 프로젝트의 최상위 디렉터리에서만 사용할 수 있는 방법이다. csope의 단축키들을 사용해서 여타 다른 IDE처럼 함수 정의부분, 호출하는 함수찾기 등을 사용하기 위해서는 cscope 플러그인을 다운받아서 따로 설정해야 한다.

######cscope 플러그인 설정
###### - cscope vim plugin 다운로드, 설정
~/.vim/plugin 디렉터리로 진입후 wget명령을 통해 cscope플러그인 다운로드
```{.bash}
$ cd ~/.vim/plugin/
$ wget http://cscope.sourceforge.net/cscope_maps.vim
--2017-03-16 14:07:47--  http://cscope.sourceforge.net/cscope_maps.vim
Resolving cscope.sourceforge.net... 216.34.181.96
Connecting to cscope.sourceforge.net|216.34.181.96|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7336 (7.2K) [text/plain]
Saving to: `cscope_maps.vim'

100%[==========================================================================>] 7,336       --.-K/s   in 0s

2017-03-16 14:07:48 (265 MB/s) - `cscope_maps.vim' saved [7336/7336]
```
###### - ~/.vimrc설정
아래의 내용을 ~/.vimrc에 추가해준다. 위에서 추가해준 내용과 달라진 점은 CSCOPE_DB환경변수를 추가해주었다는 점, 현재 작업중인 디렉터리의 경로를 추가해주었다는 점이다. 작업 디렉터리가 추가될 때마다 cs add [프로젝트 경로]를 통해 추가해주면 된다. 그 외의 고급 설정들은 차후 정리해나가야 겠다. 쿨럭.....
```{.bash}
"cscope
cs add ~/svn/fdd/telstra/jlt620trunk/cscope.out

if filereadable("./cscope.out")
	cs add cscope.out
	cs add $CSCOPE_DB
else
	cs /home/jayden/svn/jan_2017/jlt620trunk/cscope.out
endif
set csverb
```

## 3. 단축키들
* Ctrl + ] : directly jump to symbol  
* Ctrl + t : jump back to your original location before the search  
* Ctrl + \ : cs find 명령어와 같은 역할
  (Ctrl + \를 누른 후에 빠르게 s를 누르면 아래에 해당 커서에 대해 사용된 모든 심볼들이 나타난 Vim window가 나타난다)  

* Ctrl + @ : scs find  
* Ctrl + @ Ctrl + @ (두번 누를때 ) : vert cs find  

## 4. 참고자료
튜토리얼, 정말 간단한 과정들만을 추려서 설명해놓은 곳  
https://a0gustinus.wordpress.com/2013/06/01/browsing-source-code-in-linux-vimcscope/
  
KLDP 자료. 단축키, 세부설정등에 대해 정리되어 있다.  
http://wiki.kldp.org/wiki.php/VimCscopeTutorial

CSCOPE TUTORIAL  
https://courses.cs.washington.edu/courses/cse451/14wi/tutorials/tutorial_cscope.html

CSCOPE PLUGIN URL  
http://cscope.sourceforge.net/cscope_maps.vim







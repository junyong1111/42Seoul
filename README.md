# La piscine
## 1. Shell

### C Piscine Shell 00

<!--
<details>
<summary> C Piscine Shell 00  </summary>
<div markdown="1">

</div>
</details>
----------------------
-->

<details>
<summary> Shell 00  </summary>
<div markdown="1">


1. **Exercise 00**

- **cat명령어를 사용하여 지정된 파일에 내용을 확인**
    - e 옵션을 주면 개행 여부도 확인이 가능하다
2. **Exercise 01**

    - **ls명령어로 현재 경로에 있는 폴더 및 파일을 확인하고 정보를 수정**
        - l 옵션 : 퍼미션(권한)정보, 소유권, 소유그룹, 파일(폴더)용량, 생성날짜, 파일(폴더)이름
        
        --# 파일의 경우 퍼미션(권한)정보 앞에 '-'로 표시가 되며 폴더의 경우 'd'로 표시가 된다.  
        --# chmod 명령어로 퍼미션 정보를 수정이 가능하다 4:read, 2:write, 1:execute
        
3. **Exercise 02**

    - **폴더 및 파일을 만들어 해당 파일 및 폴더와 하드링크, 소프트(심볼릭)링크를 연결**
        - 하드링크
            - 바로가기와 비슷하지만 파일이 아닌 원본 파일이 가르키는 파일시스템 데이터를 가르키며 원본이 삭제되어도 유지가 된다는 특징이 존재한다.
            - 하드링크는 원본과 i-node 번호가 같고 링크 개수가 증가
            - 사용법
                
                ```bash
                ln 원본파일 하드링크파일
                ```
                
        - 소프트링크
            - 바로가기라고 생각하면 된다. 원본이 삭제되면 하드링크와 달리 사용이 불가능하다.
            - 소프트링크는 원본과 i-node 번호가 다르고 링크 개수도 증가하지 않는다.
            - 사용법
                
                ```bash
                ln -s 원본파일 하드링크파일
                ```
                
        
        —# touch -t 옵션을 사용하면 파일에 시간 수정이 가능 (년원일시간)
        
        ```bash
        touch -t 202301011212 파일명
        ```
    

    
        —# touch -h -t 옵션을 사용하면 심볼릭 파일에도 적용 가능
        
        ```bash
        touch -h -t 202301011212 파일명
        ```
        
4. **Exercise 03**

- **ssh-keygen 프로그램을 사용하여 공개키와 개인키 생성**
    - Key 생성 방법
        
        ```bash
        cd ~/.ssh #-- ssh 정보가 저장되어 있는 디렉토리로 이동
        ssh-keygen #-- 기본적으로 내장된 keygen 프로그램을 이용하여 개인키와 공용키 발급
        ls #-- 해당 명령어로 .pub 공용키 내용 확인
        ```
        
    - 공개키는 git 저장소에 등록하고 개인키는 자신이 보관 한다.
    - 개인키를 통해 ssh 접속 후 개인키와 매칭되는 공개키를 이용하여 저장소에 접근이 가능.

5. **Exercise 04**

- l**s 명령에서 여러가지 옵션을 사용**
    - -t : 출력 결과를 파일의 수정시간으로 정렬
    - -m : 파일을 ‘,’로 구분함
    - -p : 폴더를 ‘/’로 구분함
    - 현재 경로에 있는 파일 및 디렉토리를 파일 수정시간으로 정렬하고 파일을  ‘,’로 구분하며 폴더는 ‘/’로 구분하는 방법
        
        ```bash
        ls -tmp
        ```
        
    
6. **Exercise 05**

- **git log 명령어를 이용하여 커밋 log 확인**
    - -n : n개만큼의 커밋 로그 확인 가능
    - —pretty =”{foramt}” : 특정 format을 지정하여 출력
        
        —# 포멧 종류
        
        - %H : 커밋 ID만을 보여줌
        - %h : 축약된 형태의 커밋 ID만을 보여줌
        - %an : 저자 이메일
        - %cd : 커밋 날짜

```bash
git log -5 --pretty ="%H"
//# 최근 5개의 커밋 ID만을 보여줌
```

7. **Exercise 06**

- **git ls files 명령어를 이용하여 현재 작업공간에 있는 파일들 확인**
    - —others 옵션 : Staging에 올라가지 않은 파일도 확인.
    - —ignore 옵션 : git ignore에 올라간 목록을 확인, 단독으로 사용이 불가능
        - —exclude-standard 옵션을 사용 (git ignore파일의 규칙을 따르며, 표준 git ignore를 추가한다.)

```bash
git ls files --others --ignore --exclude-standard
```

8. **Exercise 07**

- **두 파일간의 차이점과 수정내용을 패치 적용**
    - 문장이 들어 있는 a파일과 수정 사항이 들어있는 .diff파일을 patch 명령어를 사용하여 그 결과를 b 파일에 저장

```bash
patch a sw.diff -o b
```

7. **Exercise 08**

- **find 명령어는 특정 타입의 데이터들을 찾아주는 명령어**
    - type -f : 파일타입만을 찾음
    - -name “원하는패턴” : 원하는 패턴의 이름을 찾아줌 연
        
        ```bash
        \( -name "#*#" -or -name "*~"\)
        #-- 연속적으로 사용시 괄호 안에 넣어서 -or 옵션을 주면 된다.
        #-- 리눅스에서 괄호 사용시 탈출문자 '\'를 사용하여 구분해야 함
        ```
        
    - print : 찾은 파일들을 출력
    - delete : 찾은 파일들을 삭제
    
    ```bash
    find -type f \( -name "#*#" -or -name "*~"\) -print -delete
    ```
    
8. **Exercise 09**

- **file 명령어는 지정된 파일의 타입을 확인할 수 있다.**
    - -m : 지정된 magic 파일을 이용하여 타입을 확인
    
    —# magic 파일 구조 : [바이트수][자료형][찾을문자열]반환타입형식
    
    ```bash
    41 string 42 42 file
    ```
    
    ```bash
    file -m "매직파일" "찾고자하는유형의 파일"
    ```
    
    
</div>
</details>

### C Piscine Shell 01

<details>
<summary> Shell 01  </summary>
<div markdown="1">

1. **Exercise 01**

- **print_groups : 소속된 그룹의 목록을 표시하는 id 명령어를 이용하면 사용자의 user,group정보를 확인 가능**
    - -G : 모든 그룹 ID들을 출력 가능 → 사용자 번호로 출력이 된다.
    - -n : 사용자 번호 대신 이름으로 출력
    
    —# export를 이용하여 환경변수 설정이 간능하다 
    
    ```bash
    export FT_USER=Hello
    env #-- 등록된 환경변수 정보 확인 가능
    ```
    
    출력된 ID값들을 조건에 맞게 전처리 필요 
    
    —# tr 명령어는 지정한 문자를 변환하거나 삭제하는 명령어
    
    - tr “” “,”  :  공백을 ‘,’로 치환  (tr “바꾸려는 문자”, “바꾸고 싶은 문자”)
    - tr -d ‘\n’ : -d 옵션은 해당 패턴 문자를 삭제한다는 의미 따라서 개행삭제
    
    ```bash
    id -G -n | tr "" "," | tr -d '\n'
    ```
    
2. **Exercise 02**

- **현재 폴더와 그 하위 폴더에 파일 이름이 ‘.sh’ 로 끝나는 모든 파일을 Search 후 파일 이름만 추출**
    - find 명령어를 통해 확장자가 sh인 파일을 찾고 그 찾은 파일을 받아 basename 명령어 실행하며 {}안에 데이터가 전달된다.
    
    —# basename : 해당 파일의 경로는 제외하고 오직 파일의 이름만을 가져옴
    
    ```bash
    find . -type -f -name '*.sh' -exec basename {} \;
    ```
    
    —# cut 명령어를 이용하여 원하는 데이터 전처리 가능 
    
    - -d : 원하는 패턴에 맞게 데이터 분할이 가능하며 -f 옵션으로 원하는 필드 추출 가능
    
    ```bash
    cit -d '.' -f 1
    #-- 마침표로 필드를 구분하며 그 중 1번째 필드를 가져오며 필드 번호의 시작은 0이 아닌 1
    ```
    
3. **Exercise 03**

- **현재 폴더와 그 하위 폴더에 파일 및 폴더의 개수를 확인**
    - find 명령어를 이용 하여 현재 모든 파일 및 폴더를 추출
    
    —# wc 명령어는 word count의 약자로 파일안에 정보뿐 아니라 파일 수 계산에서도 사용 가능
    
    - - l : 현재 word의 행의 개수를 알려준다. 파일 정보들의 행의 개수이기 때문에 결국 파일의 개수라는 의미
    - 위 명령어를 통해 나온 결과값의 앞의 공백을 모두 제거 → sed ‘s/ //g’
    
    —# sed 
    
    ```bash
    find . -type -f | wc -l | sed 's/ //g'
    ```
    
4. **Exercise 04**

- **컴퓨터의 MAC 주소 확인**
    
    —# MAC주소란 : 하드웨어 주소라고도 하며 IP와 달리 고정된 주소이다.
    
    - ip 주소 : 도로명, 주소, 이름 등 언제든지 변경이 가능하다.
    - MAC 주소 : 주민번호와 같이 한 번 생성되면 변경이 불가능한 고정된 값이며 하드웨어 주소라고도 한다.
        - MAC주소 ⇒  ehter
    - ifconfig : 컴퓨터에  있는 인터넷(네트워크) 관련된 정보 확인 가능
    - grep -w “text” : 원하는 text만 추출하며 -w 옵션이 있으면 정확히 일치해야만 추출
    - cut -d “ “ -f 2 : 추출된 정보들을 스페이스를 기준으로 필드를 나누고 그 중 2번째 필드 추출
    
    ```bash
    ifconfig | grep -w "ether" | cut -d " " -f 2
    ```
    
5. **Exercise 05**

- **컴퓨터의 MAC 주소 확인**
    
    —# MAC주소란 : 하드웨어 주소라고도 하며 IP와 달리 고정된 주소이다.
    
    - ip 주소 : 도로명, 주소, 이름 등 언제든지 변경이 가능하다.
    - MAC 주소 : 주민번호와 같이 한 번 생성되면 변경이 불가능한 고정된 값이며 하드웨어 주소라고도 한다.
        - MAC주소 ⇒  ehter
    - ifconfig : 컴퓨터에  있는 인터넷(네트워크) 관련된 정보 확인 가능
    - grep -w “text” : 원하는 text만 추출하며 -w 옵션이 있으면 정확히 일치해야만 추출
    - cut -d “ “ -f 2 : 추출된 정보들을 스페이스를 기준으로 필드를 나누고 그 중 2번째 필드 추출
    
    ```bash
    ifconfig | grep -w "ether" | cut -d " " -f 2
    ```
    
6. **Exercise 06**

- **파일 생성 규칙을 무시한 채 파일을 만드는 과제 (파일 생성 규칙 → 특수문자 사용금지)**
- 42이라는 문자열만 포함하는 크기가 2바이트인 파일 생생
    
    —# 리눅스에서 특수문자는 각각 다른  특수한 기능들이 있다 여기서 단순히 문자라는 걸 알려주려면 특수문자앞에 ‘\’ (백슬래쉬)를 넣어 일반 문자라는 표시를 해줘야 한다.
    
    - 이스케이프 문자를 사용하여 각각의 특수문자를 단순한 문자열로 인식
    - echo -n “원하는데이터” > “파일명” :  원하는데이터로 파일을 만드는데 개행은 제거
    
    ```bash
    echo -n 42 > \"\\\?\$\*\'\MaRViN\'\*\$\?\\\"
    ```
    
7. **Exercise 07**

- **ls -l 명령어의 첫 번째 행부터 시작하여 한 줄 걸러 보여주는 명령어 작성**
    
    —# awk : 데이터를 조작하고 리포트를 생성하기 위한 언어로 다양한 데이터 전처리가 가능하게 도와줌
    
    —# NR : The number of record so far (현재 라인 번호) → cat -n 으로 라인번호 확인 가능
    
    ```bash
    awk 'NR%2!=0' 
    #-- 현재 라인넘버를 몫이 0이 아니면 즉 혹수의 경우는 출력
    ```
    
8. **Exercise 08**

- **cat/etc/passwd 명령어의 출력 결과를 가공하여 출력**
    
    **—# 요구조건** 
    
    1. 주석 삭제
    2. 2번째 행부터 짝수 행만 출력
    3. 각 로그인 정보를 반전하고 알파벳 역순으로 정렬
    4. 환경변수1, 환경변수2를 포함한 그 사이값
    5. 각 로그인은 ‘,’로 구분하며 마지막은 ‘.’로 치환
    - 주석 삭제 ⇒ grep -v ‘^#’  : -v 옵션은 해당 패턴을 제외함
        - 주석은 #으로 시작
    - 2번째 행부터 짝수 ⇒ ex06 과 같음 awk ‘NR%2==0 을 사용
    - 각 로그인 문자열을 반전, 알파벳 역순으로 정렬
        - cut -d ‘:’ -f 1 :  “:” 를 기준으로 필드를 나누며 그 중 1번 필드를 가져옴
        - rev : 문자열 반전
        - sort -r : 알파벳 역순으로 정렬
    - 환경변수1, 환경변수2를 포함한 그 사이값
        
        —# sed -n 시작점 종료지점p: 원하는 시작 인덱스부터 종료 인덱스까지 추출 후 출력 
        
        ```bash
        sed -n ${변수명}, ${변수명}p
        ```
        
    - 각 로그인은 ‘,’로 구분하며 마지막은 ‘.’로 치환
        - 각 로그인은 ‘,’로 구분 → tr ‘\n’ ‘,’ 명령어로 개행을 ‘,’로 구분
        - sed ‘s/,/, /g’ → 기존 변경했던 ‘,’를 ‘, ‘로 치환 (공백 추가)
    - 마지막 ‘,’대신 ‘.’ 사용 → sed ‘s/..$/./g’ 이용하여 마지막 텍스트 ;.;로 치환
    
    —# $은 맨 마지막이라는 의미이며 ..은 맨 마지막부터 2칸 변경 하겠다는 뜻
    
    ```bash
    cat /etc/passwd | grep -v '^#' | awk 'NR%2==0' | cut -d ':' -f 1 | rev | sort -r | sed -n ${FT_LINE1},${FT_LINE2}p | tr '\n' ',' | sed 's/,/, /g' | sed 's/..$/./g' | tr -d "\n"
    ```
    

9. **Exercise 09**

- 주어진 조건에 맞는 진수 변환 후 그 값을 연산하고 또 다른 조건을 밑으로 하는 문자로 출**력**
    
    **—# 요구조건** 
    
    1. “’\"?! “을 밑으로 하는 5진수 NUMBER 1
    2. “mrdoc” 을 밑으로 하는 5진수 NUMBER 2
    3. 위 두 변수를 더하기 연산 
    4. 결과값을 “gtaio luSnemf”을 밑으로 하는 13진수 결과로 출력
    5. 
    - 주석 삭제 ⇒ grep -v ‘^#’  : -v 옵션은 해당 패턴을 제외함
        - 주석은 #으로 시작
    - 2번째 행부터 짝수 ⇒ ex06 과 같음 awk ‘NR%2==0 을 사용
    - 각 로그인 문자열을 반전, 알파벳 역순으로 정렬
        - cut -d ‘:’ -f 1 :  “:” 를 기준으로 필드를 나누며 그 중 1번 필드를 가져옴
        - rev : 문자열 반전
        - sort -r : 알파벳 역순으로 정렬
    - 환경변수1, 환경변수2를 포함한 그 사이값
        
        —# sed -n 시작점 종료지점p: 원하는 시작 인덱스부터 종료 인덱스까지 추출 후 출력 
        
        ```bash
        sed -n ${변수명}, ${변수명}p
        ```
        
    - 각 로그인은 ‘,’로 구분하며 마지막은 ‘.’로 치환
        - 각 로그인은 ‘,’로 구분 → tr ‘\n’ ‘,’ 명령어로 개행을 ‘,’로 구분
        - sed ‘s/,/, /g’ → 기존 변경했던 ‘,’를 ‘, ‘로 치환 (공백 추가)
    - 마지막 ‘,’대신 ‘.’ 사용 → sed ‘s/..$/./g’ 이용하여 마지막 텍스트 ;.;로 치환
    
    —# $은 맨 마지막이라는 의미이며 ..은 맨 마지막부터 2칸 변경 하겠다는 뜻
    
    ```bash
    cat /etc/passwd | grep -v '^#' | awk 'NR%2==0' | cut -d ':' -f 1 | rev | sort -r | sed -n ${FT_LINE1},${FT_LINE2}p | tr '\n' ',' | sed 's/,/, /g' | sed 's/..$/./g' | tr -d "\n"
    ```

</div>
</details>


## 2. C언어

### C Piscine C 00

<details>
<summary> C 00  </summary>
<div markdown="1">


1. **Exercise 00**

- **함수에 인자로 전달받은 값을 write를 이용하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
    
    void    ft_putchar(char c)
     18 {
     19     write(1, &c, 1);
     20 }
    ```
    
    2번째 인자로 받은 값 1글자를 표준 출력(화면에 보이게) 
    
2. **Exercise 01**

- **알파벳 소문자를 오름차순으로 정렬하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_print_alphabet(void);
     16 
     17 void    ft_print_alphabet(void)
     18 {
     19     write(1, "abcdefghijklnmopqrstuvwxyz", 26);
     20 }
    ```
    
    변수를 사용하지 않고 문자열을 바로 입력해도 상관없다.
    

3. **Exercise 02**

- **알파벳 소문자를 내림차순로 정렬하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_print_reverse_alphabet(void);
     16 
     17 void    ft_print_reverse_alphabet(void)
     18 {
     19     write(1, "zyxwvutsrqpomnlkjihgfedcba", 26);
     20 }
    ```
    
    변수를 사용하지 않고 문자열을 바로 입력해도 상관없다.
    
4. **Exercise 03**

- **모든 숫자를 오름차순으로 정렬하여 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_print_number(void);
     16 
     17 void    ft_print_number(void)
     18 {
     19     write(1, "0123456789", 10);
     20 }
    ```
    
    변수를 사용하지 않고 문자열을 바로 입력해도 상관없다.
    
5. **Exercise 04**

- **입력받은 숫자가 음수인지 양수인지 구분하고 상황에 맞게 출력(조건문 필요)**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
     14 
     15 void    ft_is_negative(int n);
     16 
     17 void    ft_is_negative(int n)
     18 {
     19     if (n < 0)
     20     {
     21         write(1, 'N', 1);
     22     }
     23     else
     24     {
     25         write(1, 'P', 1);
     26     }
     27 }
    ```
    
6. **Exercise 05**

- **세자릿수의 모두 다른 조합을 오름차순으로 출력**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
    
    void	ft_print_comb(void);
    /*
    int main(){
    
    	ft_print_comb();
    	return 0;
    }
    */
    
    void	ft_print_comb(void)
    {
    	char	i;
    	char	j;
    	char	k;
    
    	i = '0' - 1;
    	while (i++ < '7')
    	{
    		j = i;
    		while (j++ < '8')
    		{
    			k = j;
    			while (k++ < '9')
    			{
    				write(1, &i, 1);
    				write(1, &j, 1);
    				write(1, &k, 1);
    				if (!(i == '7' && j == '8' && k == '9'))
    					write(1, ", ", 2);
    			}
    		}
    	}
    }
    ```
    
    - 반복문을 사용하여 해결 n값이 정해져 있으므로 10 - n(3) 부터 시작하면 해결이 가능
    - 코드를 단축시키기 위해 조건문 안에 연산자를 사용
        - 이 때 i = -1 부터 시작해야 제대로 출력이 된다.
    
7. **Exercise 06**

- **두자릿수의 모든 조합을 오름차순으로 출력하는 과제**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
    
    void	ft_print_comb2(void);
    void	print_number(int n);
    
    /*
    int main(){
    	ft_print_comb2();
    	return 0;
    }
    */
    void	print_number(int n)
    {
    	char	str[2];
    
    	str[0] = '0' + n / 10;
    	str[1] = '0' + n % 10;
    	write(1, str, 2);
    }
    
    void	ft_print_comb2(void)
    {
    	int	i;
    	int	j;
    
    	i = 0;
    	while (i < 99)
    	{
    		j = i;
    		while (++j < 100)
    		{
    			print_number(i);
    			write(1, " ", 1);
    			print_number(j);
    			if (i != 98 && j != 100)
    				write(1, ", ", 2);
    		}
    		i++;
    	}
    }
    ```
    
    - 반복문을 사용하여 해결 자릿수가 2개로 고정되어 있으므로 고정값을 넣어 해결이 가능
    
8. **Exercise 07**

- **정수를 문자열로 반환하는 Integer To String 과제**
    - write : 문자열 단위로 파일에 입력하는 함수
        - 1번째 인자 : 0 → 표준 입력, 1→ 표준 출력, 2→ 표준 에러
        - 2번째 인자 : 문자열 주소
        - 3번째 인자 : 몇 바이트 즉 몇 글자 출력 할지
    
    ```c
    #include <unistd.h>
    
    void	ft_putnbr(int nb);
    int		number_len(int nb);
    int		check_minus(int number);
    void	integer_to_string(int nb);
    /*
    int main(){
    	ft_putnbr(-150);
    	return 0;
    }
    */
    
    void	integer_to_string(int nb)
    {
    	char	str[11];
    	int		len;
    	int		temp;
    
    	len = number_len(nb);
    	temp = len;
    	while (nb != 0)
    	{
    		str[len - 1] = '0' + (nb % 10);
    		nb = nb / 10;
    		len--;
    	}
    	write(1, str, temp);
    }
    
    int	check_minus(int number)
    {
    	if (number < 0)
    	{
    		return (1);
    	}
    	else
    		return (0);
    }
    
    int	number_len(int nb)
    {
    	int	len;
    	int	temp;
    
    	len = 0;
    	if (check_minus(nb) == 1)
    	{
    		nb = nb * -1;
    	}
    	temp = nb;
    	while (temp != 0)
    	{
    		len ++;
    		temp = temp / 10;
    	}
    	return (len);
    }
    
    void	ft_putnbr(int nb)
    {
    	int		len;
    	int		check;
    	char	*str;
    
    	str = NULL;
    	len = number_len(nb);
    	if (nb == -2147483648)
    	{
    		write(1, "-", 1);
    		write(1, "2147483648", 10);
    		return ;
    	}
    	if (nb == 0)
    	{
    		write(1, "0", 1);
    		return ;
    	}
    	check = check_minus(nb);
    	if (check == 1)
    	{
    		nb = nb * -1;
    		write(1, "-", 1);
    	}
    	integer_to_string(nb);
    }
    ```
    
    - 주의해야 할 점 음수 최댓값 오버플로
    - 0 예외 처리
    - 길이와 음수를 확인 후 하나씩 char 배열에 담아서 출력해주면 된다.
    
9. **Exercise 08**

- **n값을 입력받아 가능한 조합을 오름차순으로 정렬하여 출력하는 과제**
    - 백트랙킹 알고리즘 사용
    
    ```c
    #include <unistd.h>
    
    void	ft_print_combn(int n);
    int		is_possible(int pre, int curr);
    void	back_tracking(char arr[], int pre, int idx, int node);
    void	print_number(char arr[], int idx);
    /*
    int main(){
        ft_print_combn(3);
        return 0;
    }
    */
    
    int	is_possible(int pre, int curr)
    {
    	if (pre < curr)
    		return (1);
    	else
    		return (0);
    }
    
    void	print_number(char arr[], int idx)
    {
    	write(1, arr, idx);
    	if (10 - idx + '0' != arr[0])
    		write(1, ", ", 2);
    }
    
    void	back_tracking(char arr[], int pre, int idx, int node)
    {
    	int	i;
    
    	i = 0;
    	if (node == 0)
    	{
    		print_number(arr, idx);
    		return ;
    	}
    	while (i < 10)
    	{
    		if (is_possible(pre, i) == 1)
    		{
    			arr[idx] = '0' + i;
    			back_tracking(arr, i, idx + 1, node - 1);
    		}
    		i++;
    	}
    }
    
    void	ft_print_combn(int n)
    {
    	char	arr[10];
    	int		i;
    	int		idx;
    
    	if (n > 10 || n < 0)
    		return ;
    	i = 0;
    	while (i < 10)
    	{
    		idx = 0;
    		arr[idx] = '0' + i;
    		back_tracking(arr, i, idx + 1, n -1);
    		i++;
    	}
    }
    ```
    
    - 상태공간 트리를 이용
    - 조건 : 현재값은 무조건 이전값보다 커야함
    - 가능하다면 높이를 1줄이고 다시 백트랙킹 시작
    - 모든 트랙킹이 완료되었다면 저장되었던 값 출력
    
    
</div>
</details>

### C Piscine C 01

<details>
<summary> C 01 </summary>
<div markdown="1">
    
1. **Exercise 00**

- **포인터를 이용하여 해당 변수에 주소값을 참조하여 값 변경**
    
    ```c
    #include <unistd.h>
    
    void	ft_ft(int *nbr);
    
    void	ft_ft(int *nbr)
    {
    	*nbr = 42;
    }
    ```
    
    - 주소값에 있는 데이터를 변경해야 하므로 * 연산 사용
    
1. **Exercise 01**

- **포인터를 이용하여 해당 변수에 주소값을 참조하여 값 변경 (8중 포인터)**
    
    ```c
    #include <unistd.h>
    
    void	ft_ultimate_ft(int *********nbr);
    /*
    int main()
    {
    	int p = 10;
    	int *ptr = &p;
    	int **ptr2 = &ptr;
    	int ***ptr3 = &ptr2;
    	int ****ptr4 = &ptr3;
    	int *****ptr5 = &ptr4;
    	int ******ptr6 = &ptr5;
    	int *******ptr7 = &ptr6;
    	int ********ptr8 = &ptr7;
    	ft_ultimate_ft(&ptr8);
    	return 0;
    }
    */
    
    void	ft_ultimate_ft(int *********nbr)
    {
    	*********nbr = 42;
    }
    ```
    
    - 주소값에 있는 데이터를 변경해야 하므로 * 연산 사용
    
1. **Exercise 02**

- 2개의 **포인터를 이용하여 해당 변수에 주소값을 참조하여 값 변경**
    
    ```c
    #include <unistd.h>
    
    void	ft_swap(int *a, int *b);
    /*
    int main()
    {
    	int a = 10;
    	int b = 20;
    	ft_swap(&a, &b);
    	return 0;
    }
    */
    
    void	ft_swap(int *a, int *b)
    {
    	int	temp;
    
    	temp = *a;
    	*a = *b;
    	*b = temp;
    }
    ```
    
1. **Exercise 03**

- **인자로 들어온** **포인터 해당 변수에 주소값을 참조하여 값 변경**
    
    ```c
    #include <unistd.h>
    
    void	ft_div_mod(int a, int b, int *div, int *mod);
    /*
    int main()
    {
    	int a = 10;
    	int b = 2;
    	int div = 0;
    	int mod = 0;
    	ft_div_mod(a, b, &div, &mod);
    	return 0;
    }
    */
    
    void	ft_div_mod(int a, int b, int *div, int *mod)
    {
    	*div = a / b;
    	*mod = a % b;
    }
    ```
    
1. **Exercise 04**

- **2개의 포인터를 이용하여 해당 변수에 주소값을 참조하여 값 변경**
    
    ```c
    #include <unistd.h>
    
    void	ft_ultimate_div_mod(int *a, int *b);
    /*
    int main()
    {
    	int a = 10;
    	int b = 5;
    
    	ft_ultimate_div_mod(&a,&b);
    	return 0;
    }
    */
    
    void	ft_ultimate_div_mod(int *a, int *b)
    {
    	int	temp_a;
    	int	temp_b;
    
    	temp_a = *a;
    	temp_b = *b;
    	*a = temp_a / temp_b;
    	*b = temp_a % temp_b;
    }
    ```
    
1. **Exercise 05**

- **write 함수를 이용하여 문자열 출력**
    
    ```c
    #include <unistd.h>
    
    void	ft_putstr(char *str);
    int		str_len(char *str);
    /*
    int main()
    {
    	char *str;
    
    	str = "Hello World";
    	ft_putstr(str);
    
    	return 0;
    }
    */
    
    int	str_len(char *str)
    {
    	int		len;
    	char	*temp;
    
    	temp = str;
    	len = 0;
    	while (*temp != 0)
    	{
    		len++;
    		temp++;
    	}
    	return (len);
    }
    
    void	ft_putstr(char *str)
    {
    	int	len;
    
    	len = str_len(str);
    	write(1, str, len);
    }
    ```
    
1. **Exercise 06**

- **인자로 들어온 문자열의 길이를 재는 함수 작성**
    
    ```c
    #include <unistd.h>
    
    int	ft_strlen(char *str);
    /*
    int main()
    {	
    	char *str = "Hello World";
    	int len = ft_strlen(str);
    	write(1, str, len);
    	return 0;
    }
    */
    
    int	ft_strlen(char *str)
    {
    	char	*temp;
    	int		len;
    
    	len = 0;
    	temp = str;
    	while (*temp != 0)
    	{
    		len++;
    		temp++;
    	}
    	return (len);
    }
    ```
    
1. **Exercise 07**

- **인자로 들어온  문자열의 앞 뒤를 바꾸는 함수 작성**
    
    ```c
    #include <unistd.h>
    
    void	ft_rev_int_tab(int *tab, int size);
    /*
    int main()
    {
    	int arr[5];
    	int *ptr;
    	ptr = arr;
    	int size = 5;
    	for(int i=0; i<size; i++)
    	{
    		*ptr = i+1;
    		ptr++;
    	}
    	ptr = arr;
    	ft_rev_int_tab(ptr, size);
    	
    	return 0;
    }
    */
    
    void	ft_rev_int_tab(int *tab, int size)
    {
    	int	i;
    	int	temp;
    
    	i = 0;
    	temp = 0;
    	while (i < size / 2)
    	{
    		temp = *(tab + size - i -1);
    		*(tab + size - i -1) = *(tab + i);
    		*(tab + i) = temp;
    		i++;
    	}
    }
    ```
    
1. **Exercise 08**

- 1차원 배열의 원소들을 오름차순으로 정렬
    
    ```c
    #include <unistd.h>
    
    void	ft_sort_int_tab(int *tab, int size);
    void	find_min_value_swap(int *arr, int size, int key, int idx);
    void	swap_value(int *arr, int a, int b);
    /*
    int main()
    {
    	int arr[5];
    	int *ptr = arr;
    	int size = 5;
    	for(int i=0; i<size; i++)
    	{
    		arr[i] = 100 - i ; 
    	}
    	ptr = arr;
    	ft_sort_int_tab(arr, size);
    	ptr = arr;
    
    	for(int i=0; i<size; i++)
    	{
    		printf("%d", *(arr+i));
    	}
    	return 0;
    }
    */
    
    void	swap_value(int *arr, int a, int b)
    {
    	int	temp;
    
    	temp = *(arr + a);
    	*(arr + a) = *(arr + b);
    	*(arr + b) = temp;
    }
    
    void	find_min_value_swap(int *arr, int size, int key, int idx)
    {
    	int	min_idx;
    	int	pre_idx;
    
    	pre_idx = idx -1;
    	min_idx = pre_idx;
    	while (size - idx)
    	{
    		if (key > *(arr + idx))
    		{
    			key = *(arr + idx);
    			min_idx = idx;
    		}
    		idx++;
    	}
    	swap_value(arr, pre_idx, min_idx);
    }
    
    void	ft_sort_int_tab(int *tab, int size)
    {
    	int	len;
    	int	idx;
    	int	key;
    
    	idx = 0;
    	len = size -1;
    	while (len--)
    	{
    		key = *(tab + idx);
    		find_min_value_swap(tab, size, key, idx + 1);
    		idx++;
    	}
    }
    ```

</div>
</details>

### C Piscine C 02

<details>
<summary> C 02  </summary>
<div markdown="1">

1. **Exercise 00**

- **string.h에 포함되어 있는 strcpy 함수 구현**
    - **strcpy :  (목적지 문자열, 소스 문자열)**
        - **소스문자열에 있는 문자열을 목적지 문자열에 복사하는 함수**
    
    ```c
    char	*ft_strcpy(char *dest, char *src);
    /*
    int main()
    {
    	char *str = "Hello World";
    	char cp_str[15] = "World Hello!!";
    
    	ft_strcpy(cp_str, str);
    	printf("%s",cp_str);
    }
    */
    
    char	*ft_strcpy(char *dest, char *src)
    {
    	int		i;
    
    	i = 0;
    	while (src[i] != '\0')
    	{
    		dest[i] = src[i];
    		i++;
    	}
    	dest[i] = '\0';
    	return (dest);
    }
    ```
    
    - 소스문자열의 끝까지 반복문 진행
    - 목적지 문자열에 소스 문자열을 하나씩 대입
    - 마지막 목적지 문자열 반환
    
    —#  해당 함수는 NULL을 보장하지 않기 때문에 NULL을 제거해도 상관없음
    
1. **Exercise 01**

- **string.h에 포함되어 있는 strncpy 함수 구현**
    - **strcpy :  (목적지 문자열, 소스 문자열, 크기)**
        - **소스문자열에 있는 문자열을 목적지 문자열에 주어진 크기만큼 복사하는 함수**
    
    ```c
    char	*ft_strncpy(char *dest, char *src, unsigned int n);
    /*
    int main()
    {
    	char src[7] = "hello ";
    	//char dest[12];
    	char dest[12] = "HELLO WORLD";
    
    	ft_strncpy(dest, src, 1);
    	printf("%s\n", dest);
    	return 0;
    }
    */
    
    char	*ft_strncpy(char *dest, char *src, unsigned int n)
    {
    	unsigned int	i;
    	int				check ;
    
    	check = 0;
    	i = 0;
    	while (i < n)
    	{
    		if (src[i] == '\0')
    		{
    			check = 1;
    			break ;
    		}
    		dest[i] = src[i];
    		i++;
    	}
    	if (check == 1)
    		while (i < n)
    			dest[i++] = '\0';
    	return (dest);
    }
    ```
    
    - 주어진 횟수만큼 반복문을 진행
        - 진행도중 소스문자열이 끝나면 중단 후 확인
    - 반복문을 돌면서 소스문자열에 있는 문자를 목적지 문자열에 하나씩 대입
    - 만약 소스문자열이 짧아서 먼저 끝난경우 나머지 크기만큼 목적지 문자열에 NULL값 대입
    - 목적지 문자열 리턴
    
1. **Exercise 02**

- **해당 문자열이 알파벳만 포함되어 있는지 확인하는 함수 작성**
    
    ```c
    int	ft_str_is_alpha(char *str);
    /*
    int main()
    {
    	char str[10] = "";
    	printf("%d\n", ft_str_is_alpha(str));
    	return 0;
    }
    */
    
    int	ft_str_is_alpha(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	if (*temp == 0)
    		return (1);
    	while (*temp != 0)
    	{
    		if ((*temp >= 'a' && *temp <= 'z') || (*temp >= 'A' && *temp <= 'Z'))
    			temp++;
    		else
    			return (0);
    	}
    	return (1);
    }
    ```
    
    - 알파벳이 포함되어 있지 않은 경우는 멈추고 알파벳이 포함되어 있는 경우에는 전진
1. **Exercise 03**

- **해당 문자열이 숫자만 포함되어 있는지 확인하는 함수 작성**
    
    ```c
    int	ft_str_is_numeric(char *str);
    /*
    int main()
    {
    	char str[10] = "13123010";
    	printf("%d\n", ft_str_is_alpha(str));
    
    	return 0;
    }
    */
    
    int	ft_str_is_numeric(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	while (*temp != 0)
    	{
    		if (*temp >= '0' && *temp <= '9')
    		{
    			temp++;
    		}
    		else
    			return (0);
    	}
    	return (1);
    }
    ```
    
    - 숫자가 포함되어 있지 않은 경우는 멈추고  숫자가 포함되어 있다면 전진
1. **Exercise 04**

- **해당 문자열이 소문자 알파벳만 포함되어 있는지 확인하는 함수 작성**
    
    ```c
    int	ft_str_is_lowercase(char *str);
    
    /*
    int main()
    {	
    	//char str[10] = "dasdasd0";
    	char str = 0;
    	printf("%d\n", ft_str_is_lowercase(&str));
    	return 0;
    }
    */
    
    int	ft_str_is_lowercase(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	if (*temp == 0)
    		return (1);
    	while (*temp != 0)
    	{
    		if (*temp >= 'a' && *temp <= 'z')
    			temp++;
    		else
    			return (0);
    	}
    	return (1);
    }
    ```
    
    - 소문자 이외의 문자가 들어오면 중단 소문자가 들어오면 전진
1. **Exercise 05**

- **해당 문자열이 대문자 알파벳만 포함되어 있는지 확인하는 함수 작성**
    
    ```c
    int	ft_str_is_uppercase(char *str);
    /*
    int main()
    {
    	char str[10] = "ABCDEFG";
    	printf("%d\n", ft_str_is_uppercase(str));
    
    	return 0;
    }
    */
    
    int	ft_str_is_uppercase(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	if (*temp == 0)
    		return (1);
    	while (*temp != 0)
    	{
    		if (*temp >= 'A' && *temp <= 'Z')
    		{
    			temp++;
    		}
    		else
    			return (0);
    	}
    	return (1);
    }
    ```
    
    - 대문자 이외의 문자가 들어오면 중단 대문자가 들어오면 전진
1. **Exercise 06**

- **해당 문자열이 출력 가능한 문자만 포함되어 있는지 확인하는 함수 작성**
    
    ```c
    int	ft_str_is_printable(char *str);
    /*
    int main()
    {
    	char str[10] = "dada";
    	char ch ;
    	ch = 128;
    	printf("%d\n", ft_str_is_printable(&ch));
    	printf("%d\n", ft_str_is_printable(str));
    	return 0;
    }
    */
    
    int	ft_str_is_printable(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	if (*temp == 0)
    		return (1);
    	while (*temp != 0)
    	{
    		if (*temp >= 32 && *temp <= 126)
    			temp++;
    		else
    			return (0);
    	}
    	return (1);
    }
    ```
    
    - 아스키코드 표를 참조해보면 출력 가능한 문자열은 32~126인걸 확인할 수 있음
    - 그 외의 값이 들어오면 종료
1. **Exercise 07**

- **해당 문자열의 알파벳을 모두 대문자로 바꾸는 함수 작성**
    
    ```c
    char	*ft_strupcase(char *str);
    /*
    int main()
    {
    	char str[15] = "hello world!!";
    	printf("%s\n", ft_strupcase(str));
    	return 0;
    }	
    */
    
    char	*ft_strupcase(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	while (*temp != 0)
    	{
    		if (*temp >= 'a' && *temp <= 'z')
    		{
    			*temp = *temp - 32;
    		}
    		temp++;
    	}
    	temp = str;
    	return (temp);
    }
    ```
    
    - 해당 글자가 대문자라면 해당 글자에서 - 32(아스키표 참조)를 하면 소문자로 변경 가능
1. **Exercise 08**

- **해당 문자열의 알파벳을 모두 소문자로 바꾸는 함수 작성**
    
    ```c
    char	*ft_strlowcase(char *str);
    
    /*
    int main()
    {
    
    	char str[15] = "HELLO WORLD!!";
    	printf("%s\n", ft_strlowcase(str));
    	return 0;
    }
    */
    
    char	*ft_strlowcase(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	while (*temp != 0)
    	{
    		if (*temp >= 'A' && *temp <= 'Z')
    			*temp = *temp + 32;
    		temp ++;
    	}
    	temp = str;
    	return (temp);
    }
    ```
    
    - 해당 글자가 소문자라면 해당 글자에서  + 32(아스키표 참조)를 하면 대문자로 변경 가능

1.  **Exercise 09**

- 각 단어의 첫 번째 글자를 대문자로 바꾸고 나머지 글자는 소문자로 바꾸는 함수 작성
    
    ```c
    char	*ft_strcapitalize(char *str);
    int		check_word(char ch);
    int		check_lower_alpha(char ch);
    
    int	check_lower_alpha(char ch)
    {
    	if (ch >= 'a' && ch <= 'z')
    		return (1);
    	else
    		return (0);
    }
    
    int	check_word(char ch)
    {
    	if (ch >= 48 && ch <= 57)
    		return (1);
    	if ((ch >= 'A' && ch <= 'Z') || (ch >= 'a' && ch <= 'z'))
    		return (1);
    	else
    		return (0);
    }
    
    char	*ft_strcapitalize(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	if (*temp != 0 && (*temp >= 'a' && *temp <= 'z'))
    	{
    		*temp = *temp - 32;
    		temp++;
    	}
    	while (*temp != 0)
    	{
    		if (*temp >= 'A' && *temp <= 'Z')
    			*temp = *temp + 32;
    		if (check_word(*(temp -1)) == 0 && check_lower_alpha(*temp) == 1)
    			*temp = *temp - 32;
    		temp++;
    	}
    	temp = str;
    	return (str);
    }
    ```
    
    - 해당 문자가 숫자 또는 알파벳인지 확인 하는 함수
    - 해당 문자가 소문자인지만 확인하는 함수
    - 1번째 문자는 예외처리 후 시작
    - 만약 자신의 앞의 글자가 문자가 아니며 자신이 소문자라면 그 문자를 대문자로 변경
    
1.  **Exercise 10**

- string.h파일에 있는 strlcpy 함수 작성
    
    ```c
    unsigned int	ft_strlcpy(char *dest, char *src, unsigned int size);
    /*
    int main()
    {
    	char str[8] = "World!!";
    	char dest[6] = "hello";
    	int size = 8;
    	int len = ft_strlcpy(dest, str, size);
    	printf("Str is %s And StrLen is %d\n", dest, len);
    	return 0;
    }
    */
    
    unsigned int	ft_strlcpy(char *dest, char *src, unsigned int size)
    {
    	unsigned int	i;
    	int				len;
    
    	len = 0;
    	while (src[len] != 0)
    		len ++;
    	if (size == 0)
    		return (len);
    	i = 0;
    	while (i < size -1 && src[i])
    	{
    		dest[i] = src[i];
    		i++;
    	}
    	dest[i] = '\0';
    	return (len);
    }
    ```
    
    - 기존 strncpy와의 차이점은 마지막에 NULL값을 보장해준다는 점이다.

12.  **Exercise 11**

- 출력가능한 문자열을 출력하며 출력할 수 없는 문자는 역 슬래쉬 뒤에 16진법 형태로 출력하는 함수 작성
    
    ```c
    #include <unistd.h>
    
    void	ft_putstr_non_printable(char *str);
    int		is_printable(unsigned char ch);
    void	print_unprintable(unsigned char ch);
    /*
    int main()
    {
    	char * str = "Coucou\ntu vas bien ?";
    	ft_putstr_non_printable(str);
    	return 0;
    }
    */
    
    int	is_printable(unsigned char ch)
    {
    	if (ch >= 32 && ch <= 126)
    		return (1);
    	else
    		return (0);
    }
    
    void	print_unprintable(unsigned char ch)
    {
    	char	*base;
    	int		i;
    
    	i = ch;
    	base = "0123456789abcdef";
    	write(1, &base[ch / 16], 1);
    	write(1, &base[ch % 16], 1);
    }
    
    void	ft_putstr_non_printable(char *str)
    {
    	char	*temp;
    
    	temp = str;
    	while (*temp != 0)
    	{
    		if (is_printable(*temp) == 1)
    		{
    			write(1, temp, 1);
    		}
    		else
    		{
    			write(1, "\\", 1);
    			print_unprintable((unsigned char)*temp);
    		}
    		temp++;
    	}
    }
    ```
    
    - 해당 문자가 출력이 가능하다면 그냥 출력
    - 해당 문자가 출력이 불가능하다면 해당 문자열의 값을 16진법 베이스로 나누기 연산 진행

</div>
</details>

### C Piscine C 03


<details>
<summary> C 03  </summary>
<div markdown="1">

1. **Exercise 00**

- **string.h에 포함되어 있는 strcmp 함수 구현**
    - **strcmp :  (비교할 문자열1, 비교할 문자열 2)**
        - 2개의 문자열을 비교하여 그 차이값(아스키코드)를 반환해주는 함수
    
    ```c
    
    int	ft_strcmp(char *s1, char *s2);
    /*
    int main()
    {
    	char s1[10] = "Hello";
    	char s2[3] = "lo";
    
    	printf("My Function Answer is %d\n", ft_strcmp(s1, s2));
    	printf("C Function Answer is %d\n", strcmp(s1, s2));
    	
    	return 0;
    }
    */
    
    int	ft_strcmp(char *s1, char *s2)
    {
    	int	i;
    
    	i = 0;
    	while (s1[i] != 0 || s2[i] != 0)
    	{
    		if (s1[i] == s2[i])
    		{
    			i++;
    		}
    		else
    			break ;
    	}
    	return ((unsigned char)s1[i] - (unsigned char)s2[i]);
    }
    ```
    
    - 두 개의 문자열중 하나라도 끝날때까지 반복 진행
    - 두 개의 문자가 다르다면불필요한 연산을 멈추고 그 차이값을 반환
    
    —# 주의해야할 점 : s1문자열뿐 아니라 s2문자열이 먼저 끝나는 상황도 조심해야 함
    
2. **Exercise 01**

- **string.h에 포함되어 있는 strnmp 함수 구현**
    - **strncmp :  (비교할 문자열1, 비교할 문자열 2, 크기)**
        - 2개의 문자열을 **주어진 크기**만큼 비교하여 그 차이값(아스키코드)를 반환해주는 함수
    
    ```c
    int	ft_strncmp(char *s1, char *s2, unsigned int n);
    /*
    int main()
    {
    	char s1[15] = "Hello World!!";
    	char s2[15] = "Hello Word!!";
    //	char s1[15] = "Heo !!";
    //	char s2[15] = "Hello Word!!";
    	int n = 3;
    	printf("%d\n", ft_strncmp(s1, s2, n));
    	printf("%d\n", strncmp(s1,s2,n));
    	return 0;
    }
    */
    
    int	ft_strncmp(char *s1, char *s2, unsigned int n)
    {
    	unsigned int	i;
    
    	if (n == 0)
    		return (0);
    	i = 0;
    	while (i < n)
    	{
    		if (!(s1[i] && s2[i]))
    			return ((unsigned char)s1[i] -(unsigned char)s2[i]);
    		if (s1[i] == s2[i])
    			i++;
    		else
    		{
    			i++;
    			break ;
    		}
    	}
    	return (((unsigned char)s1[i -1] - (unsigned char)s2[i -1]));
    }
    ```
    
    - 주어진 크기를 넘어가지 않도록 반복진행
    - **만약 크기가 0이라면 비교할 것이 없으므로 0을 반환**
        - 주어진 크기보다 2개의 문자열의 길이가 더 작고 그 2개의 문자열이 동일한 경우 의미 없는 반복이 지속될 수 있으니 2개의 문자열 모두 비어있다면 반복을 중단
        
        → ex) str1[10] = “ab, str2[10] = “ab”, size = 1000의 경우 의미없는 반복이 수행
        
        → ex) str1[10] = “ab”, str2[10] = “abcde”, size = 1000의 경우 null문자와 ‘c’를 비교하므로 자동으로 break에 걸림
        
    
    —# 주의할 점 : 주어진 크기가 문자열보다 짧을 경우 이를 확인할 수 있어야 함
    
3. **Exercise 02**

- **string.h에 포함되어 있는 strcat 함수 구현**
    - **strcat :  (목적지 문자열 , 소스 문자열 )**
        - **소스문자열을 목적지 문자열 뒤에 붙이는 함수**
    
    ```c
    char	*ft_strcat(char *dest, char *src);
    /*
    int main()
    {
    	char dest[20] = "Hello";
    	char src[20] = " World!!";
    	
    	char dest2[20] = "Hello";
    	char src2[20] = " World!!";
    	printf("my Function Answer : %s\n", ft_strcat(dest, src));
    	printf("C Function Answer : %s\n", strcat(dest2, src2));
    	return 0;
    }
    */
    
    char	*ft_strcat(char *dest, char *src)
    {
    	char	*temp;
    
    	temp = dest;
    	while (*temp != 0)
    		temp++;
    	while (*src != 0)
    	{
    		*temp = *src;
    		temp++;
    		src++;
    	}
    	*temp = '\0';
    	temp = dest;
    	return (temp);
    }
    ```
    
    - 주어진 문자열을 임시 변수에 저장 후 컨트롤
    - 목적지 문자열에 소스 문자열을 더해야하므로 목적지 문자열을 NULL문자까지  가야함
    - 이후 목적지 문자열에 소스 문자열을 하나씩 대입시켜줌
    - 문자열의 마지막은 NULL문자가 들어가야하므로 NULL삽입
    - 임시 변수를 다시 목적지의 첫 주소로 초기화 해주고 반환
    
4. **Exercise 03**

- **string.h에 포함되어 있는 strncat 함수 구현**
    - **strncat :  (목적지 문자열, 소스 문자열, 크기)**
        - 소스문자열을 목적지 문자열에 **주어진 크기**만큼 복사하는 함수
    
    ```c
    
    char	*ft_strncat(char *dest, char *src, unsigned int nb);
    /*
    int main()
    {
    	char dest1[20] = "Hello";
    	char src1[20] = " World";
    
    	char dest2[20] = "Hello";
    	char src2[20] = " World";
    	
    	int n = 15;
    
    	printf("My Func is %s\n", ft_strncat(dest1, src1, n));
    	printf("C  Func is %s\n", strncat(dest2, src2, n));
    
    	return 0;
    }
    */
    
    char	*ft_strncat(char *dest, char *src, unsigned int nb)
    {
    	char				*temp;
    	unsigned int		i;
    
    	i = 0;
    	temp = dest;
    	if (nb == 0)
    		return (dest);
    	while (*temp != 0)
    		temp++;
    	while (i < nb && *(src + i))
    		*temp++ = *(src + i++);
    	*temp = '\0';
    	temp = dest;
    	return (temp);
    }
    ```
    
    - 복사할 크기가 0이라면 예외처리 ( 마지막 while문으로 인해 굳이 할 필요는 없지만 불필요한 연산을 막기위해)
    - 임시 변수에 목적지 문자열에 주소를 담고 NULL까지 포인터 전진
    - 주어진 크기만큼 갔거나 더이상 복사할 소스문자열이 없는 경우 멈춤
        - **소~~스문자열의 부족**으로 **인한 중단** 시 **나머지 부분은 공백**으로 채워주어야 한다.~~
    - **마지막 문자 공백 추가**
    
5. **Exercise 04**

- **string에 있는 특정 문자열을 찾는 함수 구현**
    - **strstr :  (문자열, 문자패턴)**
        - **주어진 문자열에서 특정 문자패턴을 찾아서 문자열의 첫번째 인덱스를 반환**
    
    ```c
    char	*ft_strstr(char *str, char *to_find);
    int		find_string(char *str, char *to_find, int i, int j);
    /*
    int main()
    {
    
    	char	*string1 = "needle in a haystack";
    	char	*string2 = "haystack";
    	printf("My Func Answer is : %s\n", ft_strstr(string1, string2));
    	char	*string_1 = "needle in a haystack";
    	char	*string_2 = "haystack";
    	printf("C  Func Answer is : %s\n", strstr(string_1, string_2));
    	return 0;
    }
    */
    
    int	find_string(char *str, char *to_find, int i, int j)
    {
    	int	check;
    
    	check = 1;
    	while (to_find[j] != 0)
    	{
    		if (*(str + i + j) == to_find[j])
    		{
    			j++;
    			check = 1;
    		}
    		else
    		{
    			check = 0;
    			break ;
    		}
    	}
    	return (check);
    }
    
    char	*ft_strstr(char *str, char *to_find)
    {
    	int	i;
    	int	check;
    
    	if (*to_find == 0)
    		return (str);
    	i = 0;
    	while (*(str + i) != 0)
    	{
    		check = 0;
    		if (*(str + i) == to_find[0])
    			check = find_string(str, to_find, i, 1);
    		if (check == 1)
    			return (str + i);
    		i++;
    	}
    	return (0);
    }
    ```
    
    - 주어진 문자패턴이 NULL인 경우 본래 문자를 반환
    - 문자열을 하나씩 탐색시작
        - 탐색한 문자열이 문자패턴의 첫글자와 일치한다면 find_string함수 실행
    - find_string(문자열, 문자패턴, 탐색한 문자열의 패턴 시작, 0);
        - 문자패턴이 0부터 시작이고 이미 일치했다는 사실을 알고있으므로 1증가한 상태에서부터 문자패턴 탐색 시작
            - i : 현재 문자열 과 다음 문자열의 패턴이 동일하다면 flag =1, 전진
            - 틀리다면 플래그 = 0, 중단
        - 모든 패턴을 탐색했을 때도 중단되지 않았다면 문자를 찾음
    
6. **Exercise 05**

- **string에 있는 원하는 길이만큼의 문자열을 더해주는 함수 구현**
    - **strlcat :  (목적지 문자열, 소스문자열,  크기 )**
        - 목적지 문자열에 소스문자열을 주어진 크기만큼 더해주는 함수이며 반환값은 int
        - **여기서 크기는 반드시 목적지 문자열 + 소스 문자열 + NULL문자가 포함되는 길이  이상이어야한다.**
    
    ```c
    unsigned int	ft_strlcat(char *dest, char *src, unsigned int size);
    int				str_len(char *str);
    /*
    int main()
    {
    
    	char dest[20] = "123";
    	char src[20] = "456789";
    
    	char dest1[20] = "123";
    	char src2[20] = "456789";
    
    	int size = 7;
    	printf("My F Answer is : %u \n", ft_strlcat(dest, src, size));
    	printf("My F Answer is : %s \n",dest);
    	printf("C  F Answer is : %lu \n", strlcat(dest1, src2, size));
    	printf("C  F Answer is : %s \n", dest1);
    	return 0;
    }
    */
    
    int	str_len(char *str)
    {
    	char	*temp;
    	int		len;
    
    	temp = str;
    	len = 0;
    	while (*temp != 0)
    	{
    		len++;
    		temp++;
    	}
    	return (len);
    }
    
    unsigned int	ft_strlcat(char *dest, char *src, unsigned int size)
    {
    	unsigned int	i;
    	unsigned int  dest_len;
    	unsigned int  src_len;
    
    	dest_len = str_len(dest);
    	src_len = str_len(src);
    	i = 0;
    	if (size <= dest_len)
    		return (src_len + size);
    	while (i + dest_len + 1 < size)
    	{
    		dest[dest_len + i] = src[i];
    		i++;
    	}
    	dest[dest_len + i] = '\0';
    	return (src_len + dest_len);
    }
    ```

    - 만약 주어진 크기가 목적지 문자열 조차 담지 못하는 크기가 주어진다면 아무런 행동도 하지 않고 (소스 문자열의 길이 + 크기) 반환
    - 주어진 크기가 충분하다면 목적지 문자열에 해당 소스문자열을 하나씩 대입
    
    —# 여기서 크기는 NULL문자를 보장해주기 때문에 크기는 항상 -1을 해야한다.
    
    - 마지막에는 NULL문자를 반환
        - 정상 종료 시 소스 문자열 + 목적지 문자열을 반환


</div>
</details>

### C Piscine C 04
<details>
<summary>  C 04  </summary>
<div markdown="1">

1. **Exercise 00**

- **문자열의 길이를 반환하는 함수 작성**
    - 문자열 배열을 입력받아 그 배열의 길이를 반환해주는 함수
    
    ```c
    int	ft_strlen(char *str);
    
    int	ft_strlen(char *str)
    {
    	int	len;
    
    	len = 0;
    	while (str[len] != 0)
    		len ++;
    	return (len);
    }
    ```
    
    - 문자열 한개를 입력받아 그 문자의 끝까지 갈때까지 반복문을 진행
    - 한 번 진행 시 길이를 1개씩 증가
    
2. **Exercise 01**

- 표준 출력에서 문자열을 출력하는 함수 작성
    
    ```c
    #include <unistd.h>
    
    void	ft_putstr(char *str);
    
    void	ft_putstr(char *str)
    {
    	int	len;
    
    	len = 0;
    	while (str[len] != 0)
    		len ++;
    	write(1, str, len);
    }
    ```
    
    - 위와 같이 문자열의 길이를 계산 후
    - write()함수를 이용하여 길이만큼 문자열을 출력
    
3. **Exercise 02**

- 인자로 받은 정수값을 문자열로 변환하는 함수 작성
    - int 자료형 표현 범위 전부를 표현할 수 있어야 함

```c
#include <unistd.h>

void	ft_putnbr(int nb);
int		number_len(int nb);
int		check_minus(int number);
void	integer_to_string(int nb);
/*
int main(){
	ft_putnbr(-150);
	return 0;
}
*/

void	integer_to_string(int nb)
{
	char	str[11];
	int		len;
	int		temp;

	len = number_len(nb);
	temp = len;
	while (nb != 0)
	{
		str[len - 1] = '0' + (nb % 10);
		nb = nb / 10;
		len--;
	}
	write(1, str, temp);
}

int	check_minus(int number)
{
	if (number < 0)
		return (1);
	else
		return (0);
}

int	number_len(int nb)
{
	int	len;
	int	temp;

	len = 0;
	if (check_minus(nb) == 1)
	{
		nb = nb * -1;
	}
	temp = nb;
	while (temp != 0)
	{
		len ++;
		temp = temp / 10;
	}
	return (len);
}

void	ft_putnbr(int nb)
{
	int		len;
	int		check;

	len = number_len(nb);
	if (nb == -2147483648)
	{
		write(1, "-", 1);
		write(1, "2147483648", 10);
		return ;
	}
	if (nb == 0)
	{
		write(1, "0", 1);
		return ;
	}
	check = check_minus(nb);
	if (check == 1)
	{
		nb = nb * -1;
		write(1, "-", 1);
	}
	integer_to_string(nb);
}
```

- 입력받은 값이 int자료형의 최소 범위 이거나 0인경우 예외 처리
- 이후 입력받은 값의 부호를 확인하는 check_minus함수 사용
- 절댓값을 씌우고 integer_to_string함수 실행
    - 나머지 연산을 통해 배열의 뒷부분부터 하나씩 배열에 삽입
    - 이후 출력

4. **Exercise 03**

- **string.h에 포함되어 있는 atoi 함수 구현**
    - **atoi :  (변환할 문자열)**
        - 문자열을 매개변수로 받아 int형 정수로 반환해주는 함수
            - 오버플로우는 신경쓰지 않아도 된다.
    
    ```c
    
    int		ft_atoi(char *str);
    int		check_white_space(char ch);
    char	*check_minus(char *str, int *check);
    void	check_number(char *str, int *value);
    
    void	check_number(char *str, int *value)
    {
    	while (*str >= 48 && *str <= 57)
    	{
    		*value = *(value) * 10;
    		*value = *(value) + *str -48;
    		str++;
    	}
    }
    
    char	*check_minus(char *str, int *check)
    {
    	int	cnt;
    
    	cnt = 0;
    	while (*str == '-' || *str == '+')
    	{
    		if (*str == '-')
    			cnt++;
    		str++;
    	}
    	if (cnt % 2 == 0)
    		*check = 0;
    	else
    		*check = 1;
    	return (str);
    }
    
    int	check_white_space(char ch)
    {
    	if ((ch >= 9 && ch <= 13) || ch == 32)
    		return (1);
    	return (0);
    }
    
    int	ft_atoi(char *str)
    {
    	int		check;
    	int		value;
    	char	*temp;
    
    	check = 0;
    	value = 0;
    	temp = str;
    	while (*temp != 0)
    	{
    		if (check_white_space(*temp) == 1)
    		{
    			temp++;
    			continue ;
    		}
    		if (*temp == '-' || *temp == '+' || (*temp >= '0' && *temp <= '9'))
    		temp = check_minus(temp, &check);
    		check_number(temp, &value);
    		break ;
    	}
    	if (check == 1)
    		return (value * -1);
    	return (value);
    }
    ```
    
    - 매개변수로 전달된 문자열의 공백(화이트 스페이스)들을 모두 제거
    - 이후 마이너스 개수에 따라 부호 결정
    - 숫자문자가 들어온 경우 그 아스키코드에 48을 빼줌으로 정수값 연산
    
    —# string.h에 포함된 atoi같은 경우 -연산이 중복된 경우 0처리를 해주지만 해당 과제에서는 -갯수에 따라 부호를 결정한다.
    
5. **Exercise 04**

- **정수와 base를 매개변수로 받아 해당 정수를 전달받은 base로 진법을 변환하는 함수 작성**
    - **putnbr_base :  (정수, base)**
    
    ```c
    #include <unistd.h>
    
    void	ft_putnbr_base(int nbr, char *base);
    int		check_exception(char *base, int len);
    int		check_minus(long long nb, char *base);
    int		check_base(char *base);
    void	print_base(long long nb, char *base);
    /*
    #include <stdio.h>
    
    int main()
    {
    	ft_putnbr_base(-2147483648, "0123456789");
    	printf("\n");
    	ft_putnbr_base(-2147483648, "0123456789abcdef");
    	printf("\n");
    	ft_putnbr_base(-2147483648, "jungyeki");
    	printf("\n");
    	ft_putnbr_base(-2147483648, "poneyvif");
    	printf("\n");
    	return 0;
    }
    */
    
    int	check_base(char *base)
    {
    	int	idx;
    
    	idx = 0;
    	while (base[idx])
    		idx++;
    	return (idx);
    }
    
    int	check_minus(long long nb, char *base)
    {
    	if (nb == 0)
    	{
    		write(1, &base[nb], 1);
    		return (2);
    	}
    	if (nb < 0)
    		return (1);
    	return (0);
    }
    
    void	print_base(long long nb, char *base)
    {
    	char		str[34];
    	int			idx;
    	int			len;
    	long long	tmp;
    	int			base_value;
    
    	len = 0;
    	base_value = check_base(base);
    	if (check_minus(nb, base) == 2)
    		return ;
    	if (check_minus(nb, base) == 1)
    		nb = nb * -1;
    	tmp = nb;
    	while (tmp != 0)
    	{
    		tmp = tmp / base_value;
    		len++;
    	}
    	idx = 1;
    	while (nb != 0)
    	{
    		str[len - idx++] = base[nb % base_value];
    		nb = nb / base_value;
    	}
    	write(1, str, len);
    }
    
    int	check_exception(char *base, int len)
    {
    	int	i;
    	int	j;
    
    	if (len == 0 || len == 1)
    		return (1);
    	i = 0;
    	while (i < len)
    	{
    		j = i + 1;
    		if (base[i] == '-' || base[i] == '+')
    			return (1);
    		while (j < len)
    		{
    			if (base[i] == base[j])
    				return (1);
    			j++;
    		}
    		i++;
    	}
    	return (0);
    }
    
    void	ft_putnbr_base(int nbr, char *base)
    {
    	int	len;
    
    	len = 0;
    	while (base[len])
    		len++;
    	if (check_exception(base, len) == 1)
    		return ;
    	if (nbr < 0)
    		write(1, "-", 1);
    	print_base((long long)nbr, base);
    }
    ```
    
    - 전달받은 base의 길이가 곧 몇 진법인지 알 수 있으므로 길이 확인
    - 진법 예외처리
        - base의 길이가 없거나 1인경우 예외
        - base 문자열의 ‘-’ 또는 ‘+’ 부호가 포함된 경우
        - base 문자열중 중복된 문자가 포함된 경우
    - 해당 정수가 음수라면 미리 ‘-’를 출력
    - 이 때 int 자료형의 최솟값 처리를 위해 전달받은 int → Long long으로 형변환
    - 가장 작은 진법 (2진법)으로 int 자료형을 모두 포함하려면 총 32비트가 필요하고 문자열이므로 NULL문자를 포함하기 때문에 총 33 이상의 배열 선언
    - 해당 정수를 주어진 base로 나눠준 후 문자열의 맨 뒤부터 나머지 연산으로 값을 채움
    
6. **Exercise 05**

- **위에서 작성한 atoi와 put_nbr_base를 결합**
    - atoi_base(문자열, base)
        - 전달받은 문자열을 전달받은 base로 진법 변환
    
    ```c
    
    int		ft_atoi_base(char *str, char *base);
    int		check_exception(char *base, int len);
    int		number_to_base(char *str, char	*base);
    char	*check_number_and_minus(char *str, int *check, int *value, char	*base);
    int		base_possible(char	*base, char ch);
    /*
    #include <stdio.h>
    
    int main()
    {
    	char	*str = "           24   ----++---+jungyeye0224";
    	char	*base = "0123456789abcdef";
    	printf("ft_atoi_base func answer is [%d]\n", ft_atoi_base(str, base));
    	return 0;
    }
    */
    
    int	base_possible(char	*base, char ch)
    {
    	int	idx;
    
    	idx = 0;
    	while (base[idx] != 0)
    	{
    		if (base[idx] == ch)
    			return (idx);
    		idx++;
    	}
    	return (-1);
    }
    
    int	number_to_base(char	*str, char *base)
    {
    	int	base_value;
    	int	idx;
    	int	value;
    
    	base_value = 0;
    	idx = 0;
    	value = 0;
    	while (base[base_value])
    		base_value++;
    	while (*str != 0)
    	{
    		idx = base_possible(base, *str);
    		if (idx == -1)
    			break ;
    		value = value * base_value;
    		value = value + idx;
    		str++;
    	}
    	return (value);
    }
    
    char	*check_number_and_minus(char *str, int *check, int *value, char	*base)
    {
    	int	cnt;
    
    	cnt = 0;
    	while (*str == '-' || *str == '+')
    	{
    		if (*str == '-')
    			cnt++;
    		str++;
    	}
    	if (cnt % 2 == 0)
    		*check = 0;
    	else
    		*check = 1;
    	*value = number_to_base(str, base);
    	return (str);
    }
    
    int	check_exception(char *base, int len)
    {
    	int	i;
    	int	j;
    
    	if (len == 0 || len == 1)
    		return (1);
    	i = 0;
    	while (i < len)
    	{
    		j = i + 1;
    		if (base[i] == '-' || base[i] == '+')
    			return (1);
    		if ((base[i] >= 9 && base[i] <= 13) || base[i] == 32)
    			return (1);
    		while (j < len)
    		{
    			if (base[i] == base[j])
    				return (1);
    			j++;
    		}
    		i++;
    	}
    	return (0);
    }
    
    int	ft_atoi_base(char *str, char *base)
    {
    	int		len;
    	int		check;
    	int		value;
    	char	*tmp;
    
    	len = 0;
    	check = 0;
    	value = 0;
    	tmp = str;
    	while (base[len])
    		len++;
    	if (check_exception(base, len) == 1)
    		return (0);
    	while ((*tmp >= 9 && *tmp <= 13) || *tmp == 32)
    		tmp++;
    		tmp = check_number_and_minus(tmp, &check, &value, base);
    	if (check == 1)
    		value = value * -1;
    	return (value);
    }
    ```
    
    - 위와 같은 조건에서 화이트 스페이스가 포함된 경우를 추가해서 진법 체크
    - 이후 전달받은 문자열에 공백을 모두 밀어줌
    - ‘-’부호의 개수에 따라 부호를 결정
    - 모든 문자열의 끝부터 나머지 연산을 통해 int정수값을 구해준 후 반환
    - **strlcat :  (목적지 문자열, 소스문자열,  크기 )**
        - 목적지 문자열에 소스문자열을 주어진 크기만큼 더해주는 함수이며 반환값은 int
        - **여기서 크기는 반드시 목적지 문자열 + 소스 문자열 + NULL문자가 포함되는 길이  이상이어야한다.**
    
    ```c
    unsigned int	ft_strlcat(char *dest, char *src, unsigned int size);
    int				str_len(char *str);
    /*
    int main()
    {
    
    	char dest[20] = "123";
    	char src[20] = "456789";
    
    	char dest1[20] = "123";
    	char src2[20] = "456789";
    
    	int size = 7;
    	printf("My F Answer is : %u \n", ft_strlcat(dest, src, size));
    	printf("My F Answer is : %s \n",dest);
    	printf("C  F Answer is : %lu \n", strlcat(dest1, src2, size));
    	printf("C  F Answer is : %s \n", dest1);
    	return 0;
    }
    */
    
    int	str_len(char *str)
    {
    	char	*temp;
    	int		len;
    
    	temp = str;
    	len = 0;
    	while (*temp != 0)
    	{
    		len++;
    		temp++;
    	}
    	return (len);
    }
    
    unsigned int	ft_strlcat(char *dest, char *src, unsigned int size)
    {
    	unsigned int	i;
    	unsigned int  dest_len;
    	unsigned int  src_len;
    
    	dest_len = str_len(dest);
    	src_len = str_len(src);
    	i = 0;
    	if (size <= dest_len)
    		return (src_len + size);
    	while (i + dest_len + 1 < size)
    	{
    		dest[dest_len + i] = src[i];
    		i++;
    	}
    	dest[dest_len + i] = '\0';
    	return (src_len + dest_len);
    }
    ```
    
    - 만약 주어진 크기가 목적지 문자열 조차 담지 못하는 크기가 주어진다면 아무런 행동도 하지 않고 (소스 문자열의 길이 + 크기) 반환
    - 주어진 크기가 충분하다면 목적지 문자열에 해당 소스문자열을 하나씩 대입
    
    —# 여기서 크기는 NULL문자를 보장해주기 때문에 크기는 항상 -1을 해야한다.
    
    - 마지막에는 NULL문자를 반환
        - 정상 종료 시 소스 문자열 + 목적지 문자열을 반환
        
</div>
</details>

### C Piscine C 05
<details>
<summary> C 05  </summary>
<div markdown="1">

1. **Exercise 00**

- **반복문을 사용하여 팩토리얼을 구하는 함수 작성**
    - iterative_factorial(정수)
    
    ```c
    int	ft_iterative_factorial(int nb);
    /*
    #include <stdio.h>
    
    int main()
    {
    	int nb = 6;
    	printf("%d\n", ft_iterative_factorial(nb));
    
    }
    */
    
    int	ft_iterative_factorial(int nb)
    {
    	int	ret;
    
    	ret = 1;
    	if (nb < 0)
    		return (0);
    	while (nb != 0)
    	{
    		ret = ret * nb;
    		nb--;
    	}
    	return (ret);
    }
    ```
    
    - 팩토리얼의 경우 주어진 자연수의 값을 하나씩 빼면서 곱함
    
    —# 0!은 0이 아닌 1이므로 이를 주의해야함
    
2. **Exercise 01**

- **위에서 구현한 팩토리얼 함수를 재귀로 작성**
    - recursive_factorial(정수
    
    ```c
    int	ft_recursive_factorial(int nb);
    /*
    #include <stdio.h>
    int main()
    {
    	printf("====Answer is [%d] ==============\n", ft_recursive_factorial(0));
    	return 0;
    }
    */
    
    int	ft_recursive_factorial(int nb)
    {
    	if (nb < 0)
    		return (0);
    	if (nb == 0 || nb == 1)
    		return (1);
    	return (nb * ft_recursive_factorial(nb -1));
    }
    ```
    
    - 반복문으로 구현했던것을 재귀로 구현
    
    —# 모든 반복문은 재귀로 구현이 가능하고 반대도 마찬가지로 가능하다.
    
3. **Exercise 02**

- **반복문을 사용하여 매겨변수로 주어진 정수의 제곱값을 구하는 함수 작성**
    - iterative_power(정수 N, 정수 제곱)
    
    ```c
    int	ft_iterative_power(int nb, int power);
    
    int	ft_iterative_power(int nb, int power)
    {
    	int	ret;
    
    	ret = 1;
    	if (power < 0)
    		return (0);
    	if (power == 0)
    		return (1);
    	while (power != 0)
    	{
    		ret = ret * nb;
    		power--;
    	}
    	return (ret);
    }
    ```
    
    - 주어진 제곱이 0이 될 때까지 반복문을 놀면서 주어진 n값을 곱해줌
    
    —# 어떤수의 N^0은 0이 아닌 1이다
    
4. **Exercise 03**

- **재귀를 사용하여 매겨변수로 주어진 정수의 제곱값을 구하는 함수 작성**
    - **recursive_power(int nb, int power)**
        - 위에서 구현한 함수를 재귀로 작성
    
    ```c
    int	ft_recursive_power(int nb, int power);
    /*
    #include <stdio.h>
    int main()
    {
    	printf("============= Answer is [%d] =============\n", ft_recursive_power(2,4));
    	return 0;
    }
    */
    
    int	ft_recursive_power(int nb, int power)
    {
    	if (power < 0)
    		return (0);
    	if (power == 0)
    		return (1);
    	return (nb * ft_recursive_power(nb, power -1));
    }
    ```
    
    - 음수 예외처리만 해주면 간단하게 구현가능
    
5. **Exercise 04**

- **재귀를 사용하여 주어진 매개변수의 피보나치 수열을 구해주는 함수 작성**
    - fibonacci(int index)
    
    ```c
    int	ft_fibonacci(int index);
    /*
    #include <stdio.h>
    int main()
    {
    	printf("============= Answer is [%d] ==========\n", ft_fibonacci(10));
    	return 0;
    }
    */
    
    int	ft_fibonacci(int index)
    {
    	if (index < 0)
    		return (-1);
    	if (index == 0 || index == 1)
    		return (index);
    	return (ft_fibonacci(index -1) + ft_fibonacci(index -2));
    }
    ```
    
    - 피보나치는 자기자신 -1 자기자신 -2 의 값을 가지는 수열패턴이므로 그에 맞게 처리
    
6. **Exercise 05**

- **전달받은 매개변수의 제곱근의 여부를 구하는 함수 작성**
    - **ft_sqrt(int nb)**
    
    ```c
    int	ft_sqrt(int nb);
    /*
    #include <stdio.h>
    int main()
    {
    	printf("============= Answer is [%d] ==============\n", ft_sqrt(11));
    	return 0;
    }
    */
    
    int	ft_sqrt(int nb)
    {
    	long long	i;
    
    	i = 1;
    	while (i * i <= nb)
    	{
    		if (i * i == nb)
    			return ((int)i);
    		i++;
    	}
    	return (0);
    }
    ```
    
    - 제곱근이 존재하는지 확인하려면 해당값이 어떤수의 제곱인지 확인해야함
    - 어떤수의 제곱을 구할 때 해당값이 int자료형을 넘어갈 수 있으므로 long long 으로 자료형을 지정해줘야 함

7. **Exercise 06**

- **전달받은 매개변수가 소수인지 판별하는 함수 작성**
    - **ft_is_prime(int nb)**
    
    ```c
    int	ft_is_prime(int nb);
    /*
    #include <stdio.h>
    int main()
    {
    	printf("============= Answer is [%d] ===============\n", ft_is_prime(-1));
    	printf("============= Answer is [%d] ===============\n", ft_is_prime(0));
    	printf("============= Answer is [%d] ===============\n", ft_is_prime(1));
    	printf("============= Answer is [%d] ===============\n", ft_is_prime(2));
    	printf("============= Answer is [%d] ===============\n", ft_is_prime(25));
    	printf("============= Answer is [%d] ===============\n", ft_is_prime(19));
    	return 0;
    }
    */
    
    int	ft_is_prime(int nb)
    {
    	long long	i;
    
    	if (nb <= 1)
    		return (0);
    	i = 2;
    	while (i * i <= nb)
    	{
    		if (nb % i == 0)
    			return (0);
    		i++;
    	}
    	return (1);
    }
    ```
    
    - 해당값이 소수라면 1과 자기자신을 제외한 어떤 수로도 나눠지면 안된다.
    - 여기서 제곱근 나누기를 사용하여 반복횟수를 줄여줌
    
    —# 제곱근 나누기
    
    어떤 수가 합성수(소수가 아님)인 경우 그 수는 해당 정수의 루트값의 대칭이므로 그 값을 끝까지 확인하지 않고 루트값까지만 확인하여도 소수를 판별할 수 있음
    
8. **Exercise 07**

- **전달받은 매개변수의 다음 소수가 무엇인지 판별하는 함수 작성**
    - **ft_find_next_prime(int nb)**
    
    ```c
    int	ft_is_prime(int nb);
    int	ft_find_next_prime(int nb);
    
    int	ft_find_next_prime(int nb)
    {
    	if (nb <= 1)
    		return (2);
    	while (ft_is_prime(nb) != 1)
    		nb++;
    	return (nb);
    }
    
    int	ft_is_prime(int nb)
    {
    	long long	i;
    
    	if (nb <= 1)
    		return (0);
    	i = 2;
    	while (i * i <= nb)
    	{
    		if (nb % i == 0)
    			return (0);
    		i++;
    	}
    	return (1);
    }
    ```
    
    - 위에서 사용한 소수 구하는 함수를 그대로 사용
    - 반복문을 돌면서 다음소수를 찾을 때까지 해당값을 증가
    
9. **Exercise 08**

- **10x10 퀸 퍼즐을 백트래킹을 사용하여 가능한 모든 경우의 수를 출력**
    - **ten_queens_puzzle(void)**
    - 퀸 퍼즐같은 경우 해당 index자리에 퀸이 놓아질 수 있는지에 대한 가능성을 체크하므로 1차원 배열을 사용하면 더 간단하게 해결이 가능
    
    ```c
    #include <unistd.h>
    
    int		ft_ten_queens_puzzle(void);
    int		is_possible(int *board, int idx);
    void	ten_queen(int *board, int idx, int *total);
    void	print_queen(int *board, int *total);
    int		ft_abs(int n);
    /*
    #include <stdio.h>
    
    int main()
    {
    	printf(" Total count is : [%d]\n",	ft_ten_queens_puzzle());
    	return (0);
    }
    */
    
    int	ft_abs(int n)
    {
    	if (n < 0)
    		n = n * -1;
    	return (n);
    }
    
    void	print_queen(int *board, int *total)
    {
    	int		i;
    	char	ch;
    
    	i = 0;
    	while (i < 10)
    	{
    		ch = '0' + board[i];
    		write(1, &ch, 1);
    		i++;
    	}
    	write(1, "\n", 1);
    	*total = *total +1;
    }
    
    int	is_possible(int *b, int idx)
    {
    	int	k;
    	int	promising;
    
    	k = 0;
    	promising = 1;
    	while (k < idx && promising)
    	{
    		if (b[idx] == b[k] || (ft_abs(b[idx] - b[k]) == idx - k))
    			promising = 0;
    		k ++;
    	}
    	return (promising);
    }
    
    void	ten_queen(int *board, int idx, int *total)
    {
    	int	i;
    
    	i = 0;
    	if (is_possible(board, idx))
    	{
    		if (idx == 9)
    			print_queen(board, total);
    		else if (idx < 9)
    		{
    			while (i < 10)
    			{
    				board[idx +1] = i;
    				ten_queen(board, idx +1, total);
    				i++;
    			}
    		}
    	}
    }
    
    int	ft_ten_queens_puzzle(void)
    {
    	int	board[10];
    	int	i;
    	int	total;
    
    	total = 0;
    	i = 0;
    	while (i < 10)
    		board[i++] = 0;
    	i = 0;
    	while (i < 10)
    	{
    		board[0] = i;
    		ten_queen(board, 0, &total);
    		i++;
    	}
    	return (total);
    }
    ```
    
    - 10x10 퍼즐이므로 1차원 크기가 10인 배열생성
    - 해당 보드값을 백트랙킹을 사용하여 재귀적으로 탐색
    - 가능성 체크
        - 해당 배열의 인덱스만큼 크기를 증가시키면서 만약 해당 인덱스에 이미 같은 값이 들어있다면 해당 행이 겹친다는 의미
        - X자 체크 절댓값을 사용하면 X자로 체크 가능
    - 해당 인덱스가 보드에 들어갈 수 있다면 다음으로 진행하며 만약 불가능한 경우 다시 돌아와서 탐색 시작(백트랙킹)

</div>
</details>


### C Piscine C 06
<details>
<summary> C 06  </summary>
<div markdown="1">

1. **Exercise 00**

- **실행함수에서 인자를 받아 프로그램 이름을 출력하는 파일 작성**
    
    ```c
    #include <unistd.h>
    
    int	main(int argc, char **argv)
    {
    	int	idx;
    
    	idx = 0;
    	if (argc != 1)
    		return (0);
    	while (argv[0][idx] != 0)
    		write(1, &argv[0][idx++], 1);
    	write(1, "\n", 1);
    	return (0);
    }
    ```
    
    - argc가 1이 아닌경우는 예외
    - 현재 argv에는 0번에는 프로그램이름 이후로는 들어온 문자열들이 저장되어 있음
    - 프로그램이름은 0번 인덱스에 존재하므로 0번인덱스에 있는 문자열 값을 출력
    
2. **Exercise 01**

- 실행함수에서 인자를 받아 받은 문자열을 순서대로 출력
    - 프로그램 이름은 예외 시켜야 함
    
    ```c
    #include <unistd.h>
    
    int	main(int argc, char **argv)
    {
    	int	i;
    	int	j;
    
    	i = 1;
    	while (i < argc)
    	{
    		j = 0;
    		while (argv[i][j] != 0)
    		{
    			write(1, &argv[i][j], 1);
    			j++;
    		}
    		write(1, "\n", 1);
    		i++;
    	}
    	return (0);
    }
    ```
    
    - 각각 argv 1번 인덱스부터 존재하는 문자열을 반복문을 이용하여 하나씩 출력
    
3. **Exercise 02**

- 실행함수에서 인자로 받은 문자열을 역순으로 출력
- 로그램 이름은 예외
    
    ```c
    #include <unistd.h>
    
    int	main(int argc, char **argv)
    {
    	int	i;
    	int	j;
    
    	i = argc -1;
    	while (i > 0)
    	{
    		j = 0;
    		while (argv[i][j] != 0)
    		{
    			write(1, &argv[i][j], 1);
    			j++;
    		}
    		write(1, "\n", 1);
    		i--;
    	}
    	return (0);
    }
    ```
    
    - 0번 프로그램이름은 제외해야하므로 -1 만큼 반복
    - argv에 맨 뒤 인덱스부터 반복문을 사용하여 문자열을 하나씩 출력
    
4. **Exercise 03**

- 실행함수에서 인자로 받은 문자열을 아스키코드에 맞게 정렬
- 프로그램이름은 제외해야함
    
    ```c
    #include <unistd.h>
    
    void	str_swap(char **argv, int i, int j);
    void	print_argv(int argc, char **argv);
    void	sort_ascii(int argc, char **argv);
    int		ft_strcmp(char *s1, char *s2);
    
    int	main(int argc, char **argv)
    {
    	sort_ascii(argc, argv);
    	print_argv(argc, argv);
    	return (0);
    }
    
    void	print_argv(int argc, char **argv)
    {
    	int	i;
    	int	idx;
    
    	i = 0;
    	while (++i < argc)
    	{
    		idx = 0;
    		while (argv[i][idx] != 0)
    		{
    			write(1, &argv[i][idx], 1);
    			idx++;
    		}
    		write(1, "\n", 1);
    	}
    }
    
    void	sort_ascii(int argc, char **argv)
    {
    	int	i;
    	int	j;
    
    	i = 0;
    	while (i + 2 < argc)
    	{
    		j = 2;
    		while (j < argc - i)
    		{
    			if (ft_strcmp(argv[j -1], argv[j]) > 0)
    				str_swap(argv, j -1, j);
    			j++;
    		}
    		i++;
    	}
    }
    
    void	str_swap(char **argv, int i, int j)
    {
    	char	*tmp;
    
    	tmp = argv[i];
    	argv[i] = argv[j];
    	argv[j] = tmp;
    }
    
    int	ft_strcmp(char *s1, char *s2)
    {
    	int	i;
    
    	i = 0;
    	while (s1[i] != 0 || s2[i] != 0)
    	{
    		if (s1[i] != s2[i])
    			break ;
    		i++;
    	}
    	return ((unsigned char)s1[i] - (unsigned char)s2[i]);
    }
    ```
    
    - 두 개의 문자열의 차이를 비교해주는 strcm함수를 사용하여 문자열의 차이를 계산
        - 이 때 양수이면 먼저 온 문자열의 아스키값이 더 크다는 의미
    - argv를 순회하면서 버블 정렬 진행
        - strcmp값이 양수이면 스왑 진행
    - 이후 정렬된 값들을 하나씩 출력

</div>
</details>


### C Piscine C 07
<details>
<summary> C 07  </summary>
<div markdown="1">

1. **Exercise 00**

- **string.h에 포함되어 있는 strdup 함수 구현**
    - **strdup :  (복사할 문자열)**
        - 문자열 복사에 사용하는 함수이며 strcpy와의 차이점으로는 문자열을 복사한 후 복사된 문자열을 가르키는 포인터를 반환하는 점이다.
        - strcpy의 단점을 개선한 함수이며 복사할 문자열이 복사될 문자열 공간보다 크면 복사하는 도중에 문자열이 짤린다는 단점을 포인터를 사용하여 개선한것이다.
    
    ```c
    #include <stdlib.h>
    
    char	*ft_strdup(char *src);
    int		str_len(char *str);
    /*
    #include <stdio.h>
    #include <string.h>
    int main()
    {
    	char *str = "Hello World!!";
    	char *c_func = strdup(str);
    	char *my_func = ft_strdup(str);
    
    	printf("C  Function Answer is [%s]\n", c_func);
    	printf("My Function Answer is [%s]\n", my_func);
    
    	return 0;
    }
    */
    
    int	str_len(char *str)
    {
    	int	len;
    
    	len = 0;
    	while (str[len] != 0)
    		len++;
    	return (len);
    }
    
    char	*ft_strdup(char *src)
    {
    	char	*tmp;
    	int		len;
    	int		i;
    
    	len = str_len(src);
    	tmp = (char *)malloc(sizeof(char) * len + 1);
    	if (!(tmp))
    		return (NULL);
    	i = 0;
    	while (i < len)
    	{
    		tmp[i] = src[i];
    		i++;
    	}
    	tmp[i] = '\0';
    	return (tmp);
    }
    ```
    
    - 두 개의 문자열중 하나라도 끝날때까지 반복 진행
    - 두 개의 문자가 다르다면불필요한 연산을 멈추고 그 차이값을 반환
    
    —# 주의해야할 점 : s1문자열뿐 아니라 s2문자열이 먼저 끝나는 상황도 조심해야 함
    
2. **Exercise 01**

- **1차원 배열을 동적할당 받고 초기화 한 후 그 주소값을 반환하는 함수 작성**
    - ***range(int min, int max)**
    
    ```c
    #include <stdlib.h>
    
    int	*ft_range(int min, int max);
    /*
    #include <stdio.h>
    
    int main()
    {
    	int min = 10000;
    	int max = 100;
    	int *arr = ft_range(min, max);
    	int size = max - min;
    
    	for(int i=0; i<size; i++)
    		printf("%d ", arr[i]);
    	printf("\n");
    	return 0;
    }
    */
    
    int	*ft_range(int min, int max)
    {
    	long long	size;
    	int			*arr;
    	int			idx;
    
    	if (min >= max)
    		return (NULL);
    	size = max - min;
    	arr = (int *)malloc(sizeof(int) * size);
    	if (!(arr))
    		return (NULL);
    	idx = 0;
    	while (idx < size)
    		arr[idx++] = min++;
    	return (arr);
    }
    ```
    
    - 만약 주어진 최솟값이 더 크다면 예외처리
    - 이후 최댓값 - 최솟값으로 배열의 사이즈를 계산
        - 이 때 long long으로 하면 더 안전함
    - 해당 크기의 배열을 동적 할당 만약 실패 시 널가드
    - 반복문을 돌면서 해당 배열에 값 초기화 후 주소값 반환
    
3. **Exercise 02**

- **1차원 포인터의 주소값을 전달받아 그 포인터의 주소값을 참조하여 1차원 배열 동적 할당**
    - **ultimate_range(int **range, int min, int max)**
    - 2번 함수같은 경우는 1차원 배열을 할당받아 그 주소값을 반환하는 함수였다면 해당 함수는 1차원 포인터의 주소값을 받아 1차원 포인터의 주소값을 참조하여 할당
    
    ```c
    #include <stdlib.h>
    
    int	ft_ultimate_range(int **range, int min, int max);
    
    int	ft_ultimate_range(int **range, int min, int max)
    {
    	long long	size;
    	int			idx;
    
    	if (min >= max)
    		return (0);
    	size = max - min;
    	(*range) = (int *)malloc(sizeof(int) * size);
    	if ((*range) == 0)
    		return (-1);
    	idx = -1;
    	while (++idx < size)
    		(*range)[idx] = min++;
    	return (size);
    }
    ```
    
    - 일반적인 포인터를 사용하여 주소값을 변경하는것과 마찬가지
    - 단지 포인터 1개가 더 붙었다고 생각하면 어렵지 않게 할당 가능
    
4. **Exercise 03**

- **문자열 배열이 들어있는 2차원 문자열 배열을 매개변수로 받아 해당 문자열 배열의 값들을 전달받은 구분자를 이용하여 1차원 문자열로 반환해주는 함수 작성**
    - ***strjoin(int size, char **strs, char *sep)**
    
    ```c
    #include  <stdlib.h>
    
    char	*ft_strjoin(int size, char **strs, char *sep);
    int		ft_len(char	**strs, int sep_len, int size);
    int		ft_str_len(char *str);
    /*
    #include <stdio.h>
    int main()
    {
    	char *str1 = "HELLO";
    	char *str2= "WORLD";
    	char *str3 = "42";
    	char *str4 = "SEOUL";
    	char * sep = "!__!";
    	char ** arr_str = (char **)malloc(sizeof(char *) *5 );
    	arr_str[0] = str1;
    	arr_str[1] = str2;
    	arr_str[2] = str3;
    	arr_str[3] = str4;
    	arr_str[4] = "";
    	printf("ANSWER IS [%s]\n", ft_strjoin(4, arr_str, sep));
    }
    */
    
    int	ft_str_len(char *str)
    {
    	int	len;
    
    	len = 0;
    	while (str[len] != 0)
    		len++;
    	return (len);
    }
    
    int	ft_len(char	**strs, int sep_len, int size)
    {
    	int	i;
    	int	j;
    	int	len;
    
    	i = 0;
    	len = 0;
    	while (i < size)
    	{
    		j = 0;
    		while (strs[i][j] != 0)
    		{
    			len ++;
    			j++;
    		}
    		i++;
    		if (i + 1 != size)
    			len = len + sep_len;
    	}
    	return (len);
    }
    
    char	*ft_strjoin(int size, char **strs, char *sep)
    {
    	char	*cat_str;
    	char	*str_tmp;
    	int		idx;
    	int		i;
    	int		sep_len;
    
    	sep_len = ft_str_len(sep);
    	cat_str = (char *)malloc(sizeof(char) * (ft_len(strs, sep_len, size) + 1));
    	if (!(cat_str))
    		return (NULL);
    	i = -1;
    	str_tmp = cat_str;
    	while (strs[++i] != 0 && i < size)
    	{
    		idx = 0;
    		while (strs[i][idx] != 0)
    			*str_tmp++ = strs[i][idx++];
    		idx = 0;
    		while (i + 1 != size && idx < sep_len)
    			*str_tmp++ = sep[idx++];
    	}
    	*str_tmp = '\0';
    	str_tmp = cat_str;
    	return (str_tmp);
    }
    ```
    
    - 전달 받은 2차원 문자열의 배열에 모든 문자 + 구분자 문자열이 들어갈 수 있는 공간을 할당받아야 하므로 해당 문자열의 길이를 확인
    
    —# 마지막 구분자는 포함되지 않으므로 마지막 구분자 길이는 제외해야 함
    
    - 해당 사이즈만큼 동적할당을 받은 후 할당이 안된 경우에는 널가드
    - 이후 할당받은 문자열에 값을 하나씩 옮겨담은 후 구분자 추가
    - 마지막에는 NULL문자 포함
    
    —# 동적할당을 받을 때 크기는 항상 괄호로 묶어주어야 제대로 할당이 된다.
    
5. **Exercise 04**

- **4번과제에서 진행했던 ptr_nbr_base와 atoi_base를 합친 함수 작성**
    - **convert_base(char *nbr, char *base_from, char *base_to)**
        - 지난 과제에서 했던 atoi_base를 그대로 가져와서 사용
        - 해당 과제는 파일이 2개까지 가능
    
    ```c
    //conver_base.c
    int		ft_atoi_base(char *str, char *base);
    int		check_exception(char *base);
    int		number_to_base(char *str, char	*base);
    char	*check_number_and_minus(char *str, int *check, int *value, char	*base);
    int		base_possible(char	*base, char ch);
    
    int	base_possible(char	*base, char ch)
    {
    	int	idx;
    
    	idx = 0;
    	while (base[idx] != 0)
    	{
    		if (base[idx] == ch)
    			return (idx);
    		idx++;
    	}
    	return (-1);
    }
    
    int	number_to_base(char	*str, char *base)
    {
    	int	base_value;
    	int	idx;
    	int	value;
    
    	base_value = 0;
    	idx = 0;
    	value = 0;
    	while (base[base_value])
    		base_value++;
    	while (*str != 0)
    	{
    		idx = base_possible(base, *str);
    		if (idx == -1)
    			break ;
    		value = value * base_value;
    		value = value + idx;
    		str++;
    	}
    	return (value);
    }
    
    char	*check_number_and_minus(char *str, int *check, int *value, char	*base)
    {
    	int	cnt;
    
    	cnt = 0;
    	while (*str == '-' || *str == '+')
    	{
    		if (*str == '-')
    			cnt++;
    		str++;
    	}
    	if (cnt % 2 == 0)
    		*check = 0;
    	else
    		*check = 1;
    	*value = number_to_base(str, base);
    	return (str);
    }
    
    int	check_exception(char *base)
    {
    	int	i;
    	int	j;
    	int	len;
    
    	len = 0;
    	while (base[len] != 0)
    		len++;
    	if (len == 0 || len == 1)
    		return (-1);
    	i = -1;
    	while (++i < len)
    	{
    		j = i;
    		if (base[i] == '-' || base[i] == '+')
    			return (-1);
    		if ((base[i] >= 9 && base[i] <= 13) || base[i] == 32)
    			return (-1);
    		while (++j < len)
    			if (base[i] == base[j])
    				return (-1);
    	}
    	return (len);
    }
    
    int	ft_atoi_base(char *str, char *base)
    {
    	int		len;
    	int		check;
    	int		value;
    	char	*tmp;
    
    	check = 0;
    	value = 0;
    	tmp = str;
    	len = check_exception(base);
    	if (len == -1)
    		return (0);
    	while ((*tmp >= 9 && *tmp <= 13) || *tmp == 32)
    		tmp++;
    		tmp = check_number_and_minus(tmp, &check, &value, base);
    	if (check == 1)
    		value = value * -1;
    	return (value);
    }/
    int		ft_atoi_base(char *str, char *base);
    int		check_exception(char *base);
    int		number_to_base(char *str, char	*base);
    char	*check_number_and_minus(char *str, int *check, int *value, char	*base);
    int		base_possible(char	*base, char ch);
    
    int	base_possible(char	*base, char ch)
    {
    	int	idx;
    
    	idx = 0;
    	while (base[idx] != 0)
    	{
    		if (base[idx] == ch)
    			return (idx);
    		idx++;
    	}
    	return (-1);
    }
    
    int	number_to_base(char	*str, char *base)
    {
    	int	base_value;
    	int	idx;
    	int	value;
    
    	base_value = 0;
    	idx = 0;
    	value = 0;
    	while (base[base_value])
    		base_value++;
    	while (*str != 0)
    	{
    		idx = base_possible(base, *str);
    		if (idx == -1)
    			break ;
    		value = value * base_value;
    		value = value + idx;
    		str++;
    	}
    	return (value);
    }
    
    char	*check_number_and_minus(char *str, int *check, int *value, char	*base)
    {
    	int	cnt;
    
    	cnt = 0;
    	while (*str == '-' || *str == '+')
    	{
    		if (*str == '-')
    			cnt++;
    		str++;
    	}
    	if (cnt % 2 == 0)
    		*check = 0;
    	else
    		*check = 1;
    	*value = number_to_base(str, base);
    	return (str);
    }
    
    int	check_exception(char *base)
    {
    	int	i;
    	int	j;
    	int	len;
    
    	len = 0;
    	while (base[len] != 0)
    		len++;
    	if (len == 0 || len == 1)
    		return (-1);
    	i = -1;
    	while (++i < len)
    	{
    		j = i;
    		if (base[i] == '-' || base[i] == '+')
    			return (-1);
    		if ((base[i] >= 9 && base[i] <= 13) || base[i] == 32)
    			return (-1);
    		while (++j < len)
    			if (base[i] == base[j])
    				return (-1);
    	}
    	return (len);
    }
    
    int	ft_atoi_base(char *str, char *base)
    {
    	int		len;
    	int		check;
    	int		value;
    	char	*tmp;
    
    	check = 0;
    	value = 0;
    	tmp = str;
    	len = check_exception(base);
    	if (len == -1)
    		return (0);
    	while ((*tmp >= 9 && *tmp <= 13) || *tmp == 32)
    		tmp++;
    		tmp = check_number_and_minus(tmp, &check, &value, base);
    	if (check == 1)
    		value = value * -1;
    	return (value);
    }
    ```
    
    ```c
    // convert.base2.c
    #include <stdlib.h>
    
    char	*ft_convert_base(char *nbr, char *base_from, char *base_to);
    int		check_exception(char *base);
    int		ft_atoi_base(char *str, char *base);
    char	*convert_base(long long nb, char *base, int base_value);
    int		check_len(long long nb, int base_value);
    
    int	check_len(long long nb, int base_value)
    {
    	int	len;
    
    	len = 0;
    	if (nb < 0)
    	{
    		nb = nb * -1;
    		len++;
    	}
    	while (nb != 0)
    	{
    		nb = nb / base_value;
    		len++;
    	}
    	return (len);
    }
    
    char	*convert_base(long long nb, char *base, int base_value)
    {
    	char		*str;
    	int			len;
    
    	len = check_len(nb, base_value);
    	str = (char *)malloc(sizeof(char) * 34);
    	if (!(str))
    		return (NULL);
    	if (nb == 0)
    	{
    		str[0] = base[0];
    		str[1] = '\0';
    		return (str);
    	}
    	else if (nb < 0)
    	{
    		str[0] = '-';
    		nb = nb * -1;
    	}
    	str[len] = '\0';
    	while (nb != 0)
    	{
    		str[--len] = base[nb % base_value];
    		nb = nb / base_value;
    	}
    	return (str);
    }
    
    char	*ft_convert_base(char *nbr, char *base_from, char *base_to)
    {
    	int		convert_value;
    	int		from_len;
    	int		to_len;
    	char	*tmp;
    
    	from_len = check_exception(base_from);
    	to_len = check_exception(base_to);
    	if (from_len == -1 || to_len == -1)
    		return (NULL);
    	convert_value = ft_atoi_base(nbr, base_from);
    	tmp = convert_base((long long)convert_value, base_to, to_len);
    	return (tmp);
    }
    ```
    
    - 함수 실행 시 from_base 와 to_base의 예외를 체크한 후 이상이 있는경우 함수 종료
    - 지난 과제에서 사용했던 atoi_base를 통해 입력받은 문자열을 10진수 정수로 반환
    - 반환받은 10진수 정수를 ptr_base를 이용하여 해당 진법에 맞게 변환
6. **Exercise 05**

- **1차원 문자열을 매개변수로 받아 전달받은 구분자 매개변수로 구분하여 2차원 문자열 배열에 담아 반환**
    - ****split(char *str, char *charset)**
        - 동적할당을 받는 경우 배열의 크기는 항상 괄호로 묶는 습관을 들이자.
    
    ```c
    #include <stdlib.h>
    
    char	**ft_split(char *str, char *charset);
    char	*sep_str(char *str, char *charset, int *i);
    int		arr_size(char	*str, char	*charset);
    int		sep_check(char ch, char	*charset);
    
    /*
    #include <stdio.h>
    int main()
    {
    	char	*str ="QfB8RDlcsw3Tq 3r1DHjKVDbhHhsOQF2qE";
    	char	*charset ="WHk0hrKf";
    	char	**arr_str = ft_split(str, charset);
    	int		size;
    
    	size = 0;
    	while (sep_check(str[size], charset) == 1)
    		size++;
    	for(int i = 0; i<=5 ; i++)
    		printf("[%d] : [%s]\n", i, arr_str[i]);
    	return (0);
    }
    */
    
    int	sep_check(char ch, char	*charset)
    {
    	int	i;
    
    	i = 0;
    	while (charset[i] != 0)
    	{
    		if (ch == charset[i])
    			return (1);
    		i++;
    	}
    	return (0);
    }
    
    char	*sep_str(char	*str, char	*charset, int *i)
    {
    	int		idx;
    	int		tmp;
    	char	*str_tmp;
    
    	idx = -1;
    	tmp = 0;
    	while (str[tmp] != 0)
    	{
    		if (sep_check(str[tmp], charset) != 1)
    			tmp++;
    		else
    			break ;
    	}
    	str_tmp = (char *)malloc(sizeof(char) * (tmp + 1));
    	if (!(str_tmp))
    		return (NULL);
    	*i = *i + tmp;
    	while (++idx < tmp)
    		str_tmp[idx] = str[idx];
    	str_tmp[tmp] = '\0';
    	return (str_tmp);
    }
    
    int	arr_size(char	*str, char	*charset)
    {
    	int	i;
    	int	size;
    
    	i = 0;
    	if (str[i] == 0)
    		return (0);
    	size = 1;
    	while (str[i] != 0)
    	{
    		if (sep_check(str[i], charset) == 1)
    		{
    			size ++;
    			while (sep_check(str[i], charset) == 1)
    				i++;
    		}
    		else
    			i++;
    	}
    	return (size);
    }
    
    char	**ft_split(char *str, char *charset)
    {
    	char	**str_arr;
    	int		i;
    	int		idx;
    	int		len;
    
    	i = 0;
    	idx = 0;
    	while (sep_check(str[i], charset) == 1)
    		i++;
    	len = arr_size(&str[i], charset);
    	str_arr = (char **)malloc(sizeof(char *) * (len + 1));
    	if (!(str_arr))
    		return (NULL);
    	while (idx < len)
    	{
    		str_arr[idx++] = sep_str((str + i), charset, &i);
    		if (sep_check(str[i], charset) == 1)
    		{
    			while (sep_check(str[i], charset) == 1)
    				i++;
    		}
    	}
    	str_arr[idx] = NULL;
    	return (str_arr);
    }
    ```
    
    - 2차원 배열로 반환해야 하므로 해당 1차원 문자열에 들어있는 구분자를 기준으로 사이즈 체크
        - 구분자로 시작되는 경우가 있으므로 이와 같은 경우는 미리 밀어줘서 항상 구분자가 아닌 상태로 시작할 수 있도록 셋팅
    - 구분자를 기준으로 해당 2차원 배열에 1차원 문자열을 할당해주고 다시 구분자가 아닌 문자열이 시작할 수 있도록 구분자를 밀어줌
    
    —# gcc -fsanitize=address -g3 옵션을 통해 segmentaion fault가 뜨는 부분을 정확하게 체크해야 통과할 수 있다.

</div>
</details>

### C Piscine C 08
<details>
<summary> C  08  </summary>
<div markdown="1">

</div>
</details>

<!--
<details>
<summary> C  09  </summary>
<div markdown="1">

</div>
</details>
----------------------
-->

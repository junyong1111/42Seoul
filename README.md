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
    
5. **Exercise 04**

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
    
6. **Exercise 05**

- **파일 생성 규칙을 무시한 채 파일을 만드는 과제 (파일 생성 규칙 → 특수문자 사용금지)**
- 42이라는 문자열만 포함하는 크기가 2바이트인 파일 생생
    
    —# 리눅스에서 특수문자는 각각 다른  특수한 기능들이 있다 여기서 단순히 문자라는 걸 알려주려면 특수문자앞에 ‘\’ (백슬래쉬)를 넣어 일반 문자라는 표시를 해줘야 한다.
    
    - 이스케이프 문자를 사용하여 각각의 특수문자를 단순한 문자열로 인식
    - echo -n “원하는데이터” > “파일명” :  원하는데이터로 파일을 만드는데 개행은 제거
    
    ```bash
    echo -n 42 > \"\\\?\$\*\'\MaRViN\'\*\$\?\\\"
    ```
    
7. **Exercise 06**

- **ls -l 명령어의 첫 번째 행부터 시작하여 한 줄 걸러 보여주는 명령어 작성**
    
    —# awk : 데이터를 조작하고 리포트를 생성하기 위한 언어로 다양한 데이터 전처리가 가능하게 도와줌
    
    —# NR : The number of record so far (현재 라인 번호) → cat -n 으로 라인번호 확인 가능
    
    ```bash
    awk 'NR%2!=0' 
    #-- 현재 라인넘버를 몫이 0이 아니면 즉 혹수의 경우는 출력
    ```
    
8. **Exercise 07**

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
    

9. **Exercise 08**

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
    
1. **Exercise 01**

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
    
1. **Exercise 02**

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
    
1. **Exercise 03**

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
    
1. **Exercise 04**

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
    
1. **Exercise 05**

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
<summary> C Piscine C 04  </summary>
<div markdown="1">

</div>
</details>

<details>
<summary> C Piscine Shell 00  </summary>
<div markdown="1">

</div>
</details>


<details>
<summary> C Piscine Shell 00  </summary>
<div markdown="1">

</div>
</details>

<details>
<summary> C Piscine Shell 00  </summary>
<div markdown="1">

</div>
</details>

<!--
<details>
<summary> C Piscine Shell 00  </summary>
<div markdown="1">

</div>
</details>
----------------------
-->

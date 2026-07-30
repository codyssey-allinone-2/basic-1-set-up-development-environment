# Terminal
> **Terminal & OS & Shell**
> 
> OS (Operating System)은 컴퓨터의 하드웨어(cpu, 메모리 등)를 관리하는 소프트웨어다. 
> 
> 터미널은 사용자가 os에 명령을 내릴 수 있게 해주는 UI (interface)다. 
> 
> shell은 사용자가 입력하는 명령어이자 os가 이해할 수 있는 기계어로 번역해주는 프로그램이다. 
> 
> 사용자가 명령어를 입력하면  ` 터미널 > shell > os` 방향으로 전달된다.

> **GUI & CLI**
> 
> GUI (Graphical User Interface) : 그래픽을 이용해 사용자가 직관적 인지할 수 있는 인터페이스다. 쉽게 말해 마우스로 조작할 수 있다. 
> 
> CLI (Command Line Interface) : 명령어 기반의 사용자 인터페이스를 말한다. 쉽게 말해 키보드로 조작한다. 
### 터미널에서 파일 생성/이동/삭제 명령어를 실행한다. 
1. 터미널에서 현재 위치를 확인한다. 
   ```shell
    pwd 
   ```
   ![shell1](/resources/image/shell-1.png)
2. 파일 목록을 확인한다. 
    ```shell
    ls
    ```
3. 숨겨진 파일 목록과 상세정보를 확인한다. 
   ```shell
   ls -al
    ```
   ![shell3](/resources/image/shell-3.png)
   
4. 현재 위치를 이동한다.
    ```shell
    cd /User # 절대경로 이동 
    cd .. # 상위 폴더로 이동 
    cd ./next # 하위 폴더로 이동
    ```
5. 파일을 생성한다. 
   ```shell
   touch filename 
   ```
   ![shell-4.png](/resources/image/shell-4.png)
6. 파일을 삭제한다. 
   ```shell
   rm filename
   ```
   ![shell-5.png](/resources/image/shell-5.png)
7. 파일을 복사한다. 
   ```shell
   cp originFileName copyFileName
   ```
   ![shell-6.png](/resources/image/shell-6.png)
7. 파일을 이동한다.
   ```shell
   mv originFileName targetDirectory
   ```
   ![shell-8.png](/resources/image/shell-8.png)
8. 파일의 이름을 바꾼다.
   ```shell
   mv originFileName targetFileName
   ```
   ![shell-9.png](/resources/image/shell-9.png)
9. 디렉토리를 생성한다. 
    ```shell
   mkdir directoryName
      ```
   ![shell-7.png](/resources/image/shell-7.png)
10. 디렉토리를 삭제한다. 
   ```shell
   rm -r my_folder
   ```
      - 주의사항: 
         - 폴더를 지울 때는 안에 있는 파일까지 모두 지워야 하므로 -r (recursive, 재귀적) 옵션을 붙여야 한다. 
         - 터미널에서 삭제한 파일은 휴지통으로 가지 않고 즉시 영구 삭제된다.

11. 디렉토리를 복사한다.
    ```shell
    cp -r my_folder folder_copy
     ```
12. 디렉토리를 이동하거나 이름을 바꾼다.      
      ```shell
      mv study coding_study
      ```
### 터미널에서 권한 부여/회수 명령어를 실행한다. 
1. 폴더 및 파일의 권한을 확인한다. 
![shell-10.png](/resources/image/shell-10.png)
   1. 첫 번째 글자: 종류
      - d: Directory (폴더)
      - -: 일반 파일 
      - l: Link 
   2. 나머지 9글자: 권한
 
      | 구분| 대상|  권한 | 
      | -- | -- | -- |
      |1세트 (2~4번)	|Owner (나, 소유자)|	rwx |
      |2세트 (5~7번)	|Group (우리 팀)	| r-x |
      |3세트 (8~10번)	|Others (그 외 타인)	| r-x |
   3. r, w, x의 의미

      | 기호 | 의미 |  설명 |
      | -- | -- | -- |
      | r | Read | 읽기 권한. 파일을 열어보거나 폴더 안의 목록을 볼 수 있음. |
      | w | Write | 쓰기 권한. 파일을 수정하거나 폴더 안에 파일을 만들고 지울 수 있음. |
      | x | Execute |  실행 권한. 파일을 프로그램으로 실행하거나, 폴더의 경우 그 안으로 들어갈(cd) 수 있음. |
      |- | Dash |  해당 권한이 없음. |
   2. 권한을 변경한다. 
      1. 방법1 - symbol을 사용해 권한을 변경한다.
      ```bash
      chmod [대상(Who)][연산자(Operator)][권한(Permission)] [파일/디렉토리명]
      ```
      2. 구성 요소 상세 
         1. 대상 

         |    기호    | 의미 (English) | 설명 |
         |:--------:| :--- | :--- |
         | **`u`**  | User | 파일 소유자 (Owner) |
         |  **`g`** | Group | 파일이 속한 그룹 |
         | **`o`** | Others | 소유자와 그룹을 제외한 나머지 타인 |
         | **`a`** | All | 모든 사용자 (`u`, `g`, `o` 전체) |

         2. 연산자 
   
         |  기호 | 의미 | 설명 |
         | :---: | :--- | :--- |
         | **`+`** | Add | 지정한 권한을 새로 추가함 |
         | **`-`** | Remove | 지정한 기존 권한을 제거함 |
         | **`=`** | Assign | 기존 권한을 무시하고 지정한 권한으로 덮어씀 |

         3. 권한 

        | 기호 | 의미 (English) | 설명 |
        |  :---: | :--- | :--- |
        |  **`r`** | Read | 읽기 권한 |
        |  **`w`** | Write | 쓰기 권한 |
        |  **`x`** | Execute | 실행 권한 (디렉토리의 경우 접근 권한) |

      2. 방법 2 - 숫자를 이용한다.
       ```shell
         chmod [나][그룹][타인]  [파일/디렉토리명]
       ```
      ```
       4: 읽기 (r)
       2: 쓰기 (w)
       1: 실행 (x)
       0: 권한 없음
      ```

     읽을 수 없게 권한을 변경한다.
     ```shell
     chmod 000 filename
     ```
    ![shell-11](/resources/image/shell-11.png)

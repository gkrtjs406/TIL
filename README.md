# TIL(Today I Learned)

1. git init
   - 현재 작업 중인 디렉토리를 Git으로 관리한다는 명령어 (master 붙음)
2.  git status
   - working directory에 있는 파일의 현재 상태를 알려줌
3.  git add
   - working directory에 있는 파일을 Staging Area로 올리는 명령어

4. git commit -m 'ddd'
   - staging area에 올라온 파일의 변경사항을 하나의 버전으로 저장하는 명령어

5. git log (--oneline)
   - 커밋의 내역을 조회

6. git remote add origin <주소>
   - 로컬저장소에 원격저장소를 등록, 조회, 삭제 할 수 있는 명령어
7.  git remote -v 
   - 원격 저장소 조회

8. git push origin(이름) master(브랜치이름)
   - 로컬저장소의 커밋을 원격 저장소에 업로드하는 명령어
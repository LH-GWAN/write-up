# HTTP 헤더를 이용한 Command Injection

1. 코드를 분석한 결과, 클라이언트의 IP 주소를 다음과 같이 별도의 검증 없이 셸 명령어에 삽입하고 있다. ```["/bin/bash", "-c", f"echo {user_ip}"]```
2. user_ip는 다음 코드를 통해 설정된다.
3. user_ip = request.access_route[0] if request.access_route else request.remote_addr
4. request.access_route는 일반적으로 X-Forwarded-For 헤더의 값을 참조하므로, 공격자가 해당 헤더 값을 임의로 조작할 수 있다.
5. 단순히 X-Forwarded-For: ls /를 전송하면 서버에서는 echo ls /로 실행되어 문자열만 출력된다.
6. 따라서 세미콜론(`;`)과 같은 셸 명령어 구분자를 사용하여 기존 `echo` 명령 뒤에 새로운 명령어를 삽입한다.
7. 루트 디렉터리에서 플래그 파일의 위치와 형태를 확인한 뒤, `cat /flag` 명령을 삽입하여 플래그를 획득할 수 있다.

# Timeout 예외를 이용한 관리자 KEY 유출 취약점
1. 코드 분석 결과 `/flag` 페이지에서는 POST 요청으로 전달된 `cmd_input`과 `key` 값을 검사한다. 이때 다음과 같은 조건문이 존재한다.
2. `if cmd != '' or key == KEY:`
3. 이 조건문은 `cmd` 값이 비어 있지 않거나, `key` 값이 관리자 KEY와 일치하면 실행된다.
4. 즉, 관리자 KEY를 알지 못해도 `cmd_input` 값만 전달하면 해당 분기 안으로 들어갈 수 있다.
5. 해당 분기에서는 `subprocess.check_output()`을 통해 서버에서 명령어를 실행하며, `timeout=5` 옵션이 설정되어 있다.
6. 따라서 `sleep 6`과 같이 5초를 초과하는 명령어를 입력하면 `TimeoutExpired` 예외가 발생한다.
7. 공격자는 `curl`을 이용해 `/flag`에 POST 요청을 보내고, `cmd_input=sleep 6`을 전달하여 timeout을 의도적으로 발생시킬 수 있다.
8. 이를 통해 관리자 KEY를 획득한 뒤, 다시 해당 KEY를 이용해 `/flag`에 접근하면 최종적으로 FLAG가 반환된다.

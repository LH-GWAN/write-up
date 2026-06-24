# 브루트 포싱
1. 코드를 확인해보면 alphanumeric = string.ascii_lowercase + string.digits 이런식으로 문자열을 만든다
2. 그 이후 여기서 랜덤으로 4개를 선택해 사물함 번호를 생성한다
3. 사물함 번호의 경우 문자열을 입력했을 때 해당 문자열이 랜덤으로 고른 문자열과 일치한다면 Good 을 출력한다

   if locker_num != "" and rand_str[0:len(locker_num)] == locker_num:
5. 그렇기에 문자열을 하나씩 넣어보며 맞는 문자열을 찾아간다
6. 패스워드는 100 ~ 200 사이 숫자 중 하나다
7. 직접 넣어보며 flag를 추출해낸다

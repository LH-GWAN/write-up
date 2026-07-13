# 필터링 우회 취약점

1. 플래그는 `flag.php` 파일에 위치해 있다.
2. 서버는 요청 URL을 `parse_url()`로 분석한 뒤, URL의 경로인 `$path`에 `flag.php` 문자열이 포함되어 있는지 검사한다.
3. 일반적으로 `/flag.php`로 접근하면 `$path`에 `flag.php`가 포함되므로 필터링에 걸린다.
4. 하지만 `//flag.php`로 요청하면 `parse_url()`은 `flag.php`를 경로가 아닌 호스트로 해석하여 `$path`가 비어 있게 된다.
5. 따라서 `preg_match()` 검사를 우회할 수 있으며, 웹서버는 `//flag.php`를 `/flag.php`와 같은 경로로 처리하므로 실제 `flag.php` 파일에 접근할 수 있다.



`Command PhaseScriptExcution failed with a nonzero exit code`  라는 에러가 나왔다.
에러가 나오게 된 배경에는 
1. 시뮬레이터 사용.
2. Scheme에 따라서 Release  로 Run 을 한 경우.

매우 친절하게도 Pods-ProjectName-frameworks.sh: line 132: ARCH\[@]: unbound variable 이라고 이유도 설명되어있다.
알려준 파일로 이동하였고 ARCH\[@]를 검색하였고

Xcode 12에서부터 Deprecated 된 `VALID_ARCHS`가 문제를 일으켰다.

Release에는 x86_84가 포함되어있지않았기에 시뮬레이터가 실행이 되질않았다.

해결 방법
1. `VALID_ARCHS` 에 x86_64를 추가
2. `VALID_ARCHS` 의 대안인 `EXCLUDED_ARCHS`를 사용

하지만 1번의 경우 Xcode 12에서부터 Deprecated 라고 알려줬기에 장기적으로도 교체가 필요하다.
`VALID_ARCHS` 의 대안인 `EXCLUDED_ARCHS`를 사용하기로 생각했다.

`EXCLUDED_ARCHS` 설정을 마치고  `VALID_ARCHS` 을 삭제할려고 했는데 잘 되지않았다.
`Target의 Build Settings`는 Project를 따르기 때문에 `Project Build Settings`에서 지웠다.

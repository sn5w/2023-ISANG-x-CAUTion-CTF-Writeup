# Suspicious Web

레드팀 시나리오

범인의 집 밑에서 네트워크를 도청했습니다. 수상한 ip와의 통신이 포착되어 즉시 ip에 접근해봤으나 이미 비활성화된 상태였습니다. 도청 자료는 여기 있습니다. 자료를 분석해보고 이상한 점이 있으면 알려주세요.


Made by codeblue

Writeup
--
Wireshark 로 패킷을 조사하다보면 sql injection을 통해 로그인한 HTTP Stream을 확인할 수 있었다. <br>
범인이 마지막에 그림 파일을 다운로드 받았음을 확인할 수 있는데, 해당 그림 파일을 추출하여 확인해보면 QR code가 있고 해당 QR code를 스캔해보면 flag가 나온다.

![518155694](https://user-images.githubusercontent.com/122713759/212667358-cd219d14-ef90-4dff-940d-b6f10cdef953.png)

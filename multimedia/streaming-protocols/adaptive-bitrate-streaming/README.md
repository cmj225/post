# Adaptive Bitrate Streaming

HTTP는 양방\(full-duplex\) 방식이 아니기 때문에 라이브 스트리밍을 위해서는 단점을 극복할 별도의 방식이 필요하지만, 방화벽에서 HTTP 서버로의 요청만 통과시키면 되기 때문에 방화벽의 설정이 단순해진다

요청과 응답이 1:1로 대응되므로 NAT 환경에서도 서버와 통신하는 것이 쉽다. 비단 방화벽 문제 때문이 아니라, 웹 서비스를 위한 캐시 구조를 그대로 사용할 수 있고, 기존에 구축되어 있는 CDN\(Content Delivery Network\)도 특별히 변경하지 않고 그대로 이용할 수 있다는 것이 장점이다.






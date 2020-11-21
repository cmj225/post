# av\_read\_frame\(\), avcodec\_send\_packet\(\)/avcodec\_receive\_frame\(\)

## av\_read\_frame\(\)

* 압축된 혼합 스트림에서 정수 배수 단위 프레임이 담긴 패킷을 얻어옴.
  * 비디오는 일반적으로 하나, 오디오는 여러개의 프레임 데이터가 담겨있다.
* AVFormatContext 내부에 버퍼링 된 패킷 리스트가 있는 경우 해당 패킷을 드레인하고, 없는 경우 새로 패킷을 드레인한다.
* 패킷을 파싱하는 파서가 존재하고, 필요한 경우 파싱도 진행한다.

![](../../../../.gitbook/assets/image-5-%20%281%29.png)

## avcodec\_send\_packet\(\), avcodec\_receive\_frame\(\)

* avcodec\_decode\_video2\(\), avcodec\_decode\_audio4\(\) deprecated
* avcodec\_send\_packet\(\)
  * 내부의 패킷 참조를 해제하고 새로 입력된 패킷을 참조
  * 내부 패킷을 비트스트림 필터로 전달
  * 디코딩 버퍼가 비어있으면 디코딩을 진행
* avcodec\_receive\_frame\(\)

  * 입력된 AVFrame의 레퍼런스를 정리하고 디코딩된 AVFrame을 옮겨 담는다.

![](../../../../.gitbook/assets/image-6-%20%281%29.png)




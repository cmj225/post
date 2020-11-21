---
description: allocate an AVFormatContext for an output format
---

# avformat\_alloc\_output\_context2\(\)

* **avformat\_alloc\_output\_context2\(AVFormatContext \*\*ctx, AVOutputFormat \*oformat, const char \*format\_name, const char \*filename\)**
  * ctx : 생성 완료 후 얻게 될 AVFormatContext, 실패 시 NULL
  * oformat : 생성하고자 하는 output format, 입력이 없을 시 format\_name이나 filename을 이용해 추측하여 생성
  * format\_name : 파일 컨테이너 형식, 미입력시 filename을 이용해 추정
  * filename : 출력 파일 경로 

![](../../../../.gitbook/assets/image%20%285%29.png)

![](../../../../.gitbook/assets/image-1-%20%283%29.png)




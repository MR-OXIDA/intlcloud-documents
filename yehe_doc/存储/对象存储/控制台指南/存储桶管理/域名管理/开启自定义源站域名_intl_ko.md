## 소개

본 문서에서는 사용자 정의 도메인을 버킷에 바인딩하고 사용자 정의 도메인으로 버킷 내 파일에 액세스하는 방법을 소개합니다.

>COS 콘솔에서 추가할 수 있는 사용자 정의 도메인은 최대 20개입니다. 사용자 정의 도메인 개수를 늘리려면 [문의하기](https://console.cloud.tencent.com/workorder/category)를 통해 문의하십시오.
>

##  작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다. 
2. 왼쪽 메뉴에서 [버킷 리스트]를 클릭하여 버킷 리스트 페이지로 이동합니다.
3. 도메인을 설정할 버킷을 클릭하여 버킷 설정 페이지로 이동합니다.
4. 왼쪽 메뉴에서 [도메인 및 전송 관리]>[사용자 정의 원본 서버 도메인]을 선택하고 [도메인 추가]를 클릭합니다.
5. 사용자 정의 도메인이 공업정보부에 등록되어 있고 [도메인 서비스 콘솔](https://console.cloud.tencent.com/cns/domains)에서 리졸브를 추가한 경우 [도메인] 입력란에 사용자 정의 도메인 이름을 입력하고 [저장]을 클릭하십시오. 도메인 이름을 저장 후 인증서를 업로드할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/d0c76b2e57cd6a1b6d395bd7d4d21216.png)
6. 사용자 정의 도메인에 리졸브를 추가하지 않았다면, 다음 순서에 따라 사용자 정의 도메인을 추가합니다.

  1. [도메인 서비스 콘솔](https://console.cloud.tencent.com/cns/domains)에 로그인한 뒤 왼쪽 메뉴바에서 [도메인 리졸브 리스트]를 클릭하여 전체 도메인 페이지로 이동합니다. 다시 [리졸브 추가]를 클릭하면 리졸브 추가를 위한 대화 상자가 뜹니다.
  2. 사용자 정의 도메인을 입력하고, 프로젝트 옵션을 기본 프로젝트로 선택한 후, [확인]을 클릭합니다. **특별한 경우가 아니라면 프로젝트 옵션을 기본 프로젝트로 선택합니다.**
  3. 도메인을 추가한 뒤 도메인을 클릭하여 리졸브 기록 관리 페이지로 이동합니다. [기록 추가]를 클릭하면 기록 추가를 위한 대화 상자가 뜹니다.
  4. 호스트 기록 시 안내에 따라 기록 유형은 CNAME을 선택하고, 회선 유형은 기본을 선택합니다. 기록값에는 버킷 도메인을 입력하고, TTL은 기본으로 유지합니다. 정보를 작성한 뒤 [저장]을 클릭합니다.
  5. 리졸브를 추가하면 적용되기까지 약 10분이 소요됩니다. 적용되면, 3번 순서에 따라 설정합니다.

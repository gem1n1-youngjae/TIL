## DNS란?

> - DNS 또는 Domain Name System은 사람이 읽을 수 있는 도메인 이름(ex: `www.domain.com`)을 머신이 읽을 수 있는 IP 주소(ex: `192.0.2.44`)로 변환한다.
> - 인터넷의 DNS 시스템은 이름과 숫자 간의 매핑을 관리하여 마치 전화번호부와 같은 기능을 한다.

## DNS 서비스 유형
### 신뢰할 수 있는 DNS
> - 개발자가 퍼블릭 DNS 이름을 관리하는 데 사용하는 업데이트 메커니즘을 제공하며, 이를 통해 DNS 쿼리에 응답하여 도메인 이름을 IP 주소로 변환한다.

> - 신뢰할 수 있는 DNS는 도메인에 대해 최종 권한이 있으며 재귀적 DNS 서버에 IP 주소 정보가 담긴 답을 제공할 책임이 있다.

### 재귀적 DNS

> - 보통 클라이언트는 신뢰할 수 있는 DNS 서비스에 직접 쿼리를 수행하지 않고, 해석기 또는 재귀적 DNS 서비스라고 알려진 다른 유형의 DNS 서비스에 연결하는 경우가 일반적이다.

> - 재귀적 DNS 서비스는 호텔 컨시어지와 같은 역할을 한다.

> - DNS 레코드를 소유하고 있지 않지만 사용자를 대신해서 DNS 정보를 가져올 수 있는 중간자의 역할을 한다.

> - 일정 기간 동안 캐시된 또는 저장된 DNS 레퍼런스를 가지고 있는 경우, 소스 또는 IP 정보를 제공하여 DNS 쿼리에 답을 하거나, 해당 정보를 찾기 위해 쿼리를 하나 이상의 신뢰할 수 있는 DNS 서버에 전달한다.


## DNS 동작 원리
<img src="../../img/DNS_Behavior_Principles.png">

1. 웹 브라우저에 www.naver.com을 입력하면 먼저 `Local DNS`에게 www.naver.com이라는 hostname"에 대한 IP 주소를 물어본다.
<br>
2. `Local DNS`에는 "www.naver.com에 대한 IP 주소"가 있을 수도 없을 수도 있다. 만약 있다면 `Local DNS`가 바로 PC에 IP 주소를 주고 끝난다. 본 설명에서는 `Local DNS`에 "www.naver.com에 대한 IP 주소"가 없다고 **가정**한다.
<br>
3. `Local DNS`는 "www.naver.com에 대한 IP 주소"를 찾아내기 위해 다른 DNS 서버들과 통신을 시작한다. 먼저 `Root DNS 서버`에게 www.naver.com에 대한 IP 주소를 요청한다. 이를 위해 각 `Local DNS 서버`에는 `Root DNS 서버`의 정보 (IP 주소)가 미리 설정되어 있어야 한다.
<br>
4. `Root DNS 서버`는 www.naver.com의 IP 주소를 가지고 있지 않다. 그래서 `Local DNS 서버`에게 www.naver.com에 대한 IP 주소가 없으니. 자신이 알려주는 다른 DNS 서버에게 요청을 하라고 응답을 한다. (이 다른 DNS 서버는 `com 도메인을 관리하는 DNS 서버`이다.)
<br>
5. 이제 `Local DNS 서버`는 `com 도메인을 관리하는 DNS 서버`에 다시 www.naver.com에 대한 IP 주소를 요청한다.
<br>
6. `com 도메인을 관리하는 DNS 서버`에도 해당 정보가 없다. 그래서 이 DNS 서버는 `Local DNS` www.naver.com의 IP 주소를 가지고 있지 않다. 그래서 `Local DNS 서버`에게 www.naver.com에 대한 IP 주소가 없으니. 자신이 알려주는 다른 DNS 서버에게 요청을 하라고 4번과 매우 비슷한 응답을 한다. 이 다른 `DNS 서버`는 `naver.com도메인을 관리하는 DNS 서버`이다.
<br>
7. `naver.com DNS 서버` 에는 `www.naver.com 의 IP 주소` 가 있다. 그래서 Local DNS 서버에게 "www.naver.com에 대한 IP 주소는 222.122.195.6" 라는 응답을 한다.
<br>
8. 이를 수신한 `Local DNS`는 `www.naver.com 의 IP` 주소를 캐싱을 하고 이후 다른 요청이 있을시 응답할 수 있도록 IP 주소 정보를 단말(PC)에 전달해 준다.

> Local DNS 서버가 여러 DNS 서버에 차례대로 (Root DNS 서버 -> com DNS 서버 -> `naver.com` DNS 서버) 요청하여 그 답을 찾는 과정을 Recursive Query 라고 부른다.

### 참고
<a href="https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C">도메인 네임 시스템 [위키백과]</a>

<a href="https://www.netmanias.com/ko/post/blog/5353/dns/dns-basic-operation">DNS 기본 동작 설명 [NETMANIAS]</a>

<br>
<br>
<br>
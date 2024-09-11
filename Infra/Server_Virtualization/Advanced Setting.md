### 고급 설정 (Advanced Settings)

고급 설정은 다양한 상황에서 사용될 수 있으며, 특히 고가용성(HA, High Availability)과 관련된 중요한 설정 세 가지는 다음과 같습니다:

1. **das.*** : 클러스터 레벨에서 사용되는 설정
2. **fdm.*** : FDM 호스트 레벨에서 사용되는 설정
3. **vpxd.*** : vCenter 레벨에서 사용되는 설정

### 고급 설정 구성 방법

고급 설정을 구성하는 절차는 비교적 간단하며, 대부분의 경우 다음과 같은 절차를 따릅니다:

### 클러스터 레벨 구성 방법:

1. vSphere 클라이언트에서 "Hosts and Clusters"로 이동
2. 클러스터 객체를 클릭
3. "Configure" 탭 선택
4. "vSphere Availability" 클릭
5. "vSphere HA"에서 "Edit" 클릭
6. "Advanced Options" 버튼 클릭

### FDM 호스트 레벨 구성 방법:

- SSH 세션을 통해 호스트에 접속하여 `/etc/opt/vmware/fdm/fdm.cfg` 파일을 편집

### vCenter 레벨 구성 방법:

1. vSphere 클라이언트에서 "Hosts and Clusters"로 이동
2. 적절한 vCenter 서버를 선택
3. "Configure" 탭에서 "Advanced Settings" 선택

### 자주 사용하는 고급 설정

- **das.maskCleanShutdownEnabled**: VM이 접근 불가능하고 전원이 꺼진 경우 VM 페일오버가 트리거되도록 설정하는 옵션
- **das.ignoreInsufficientHbDatastore**: 하트비트 데이터스토어 수가 설정된 수보다 적을 때 발생하는 경고를 무시하는 옵션
- **das.heartbeatDsPerHost**: 호스트당 필요한 하트비트 데이터스토어 수 설정 (기본값: 2) v
- **das.isolationaddress[x]**: 호스트가 격리 상태인지 확인하기 위한 IP 주소 설정 v
- **das.usedefaultisolationaddress**: 기본 격리 주소를 사용하지 않도록 설정
- **das.allowNetwork[x]**: VMware HA에서 사용할 네트워크를 설정하는 옵션
- **das.perHostConcurrentFailoversLimit**: 호스트당 최대 동시 VM 페일오버 수를 설정하는 옵션

고급 설정 사용을 최대한 피하는 것이 좋다고 권장합니다. 불필요한 설정은 복잡성을 증가시키고, 오히려 다운타임을 증가시킬 수 있기 때문입니다.
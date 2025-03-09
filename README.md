## 1. 과제 진행 상황

<ul>
<li>ERD cloud를 통한 ERD 작성 및 SQL 작성</li>
<li>XAMPP를 활용한 mySQL 서버 구축 및 community table 작성</li>
</ul>

## 2. 회고

1. 이번 과제에서는 ERD Cloud를 적극 활용하여 데이터베이스를 구축하였다. 이전에는 단순히 ERD를 도식화하는 용도로만 사용했지만, SQL Export 기능을 활용하면 SQL 문까지 자동 생성해준다는 점을 새롭게 알게 되었다. 이를 통해 DB 구축 과정이 훨씬 간편해졌다고 느꼈다.

2. 하지만, ERD Cloud의 UI에서는 Auto Increment(AI)를 직접 설정할 수 없었다. 따라서, ERD Cloud가 생성해 준 SQL 뼈대에 AI를 직접 추가하고, 외래 키(FK) 관리 강화를 위해 ON DELETE CASCADE 옵션을 설정하여 참조 무결성을 유지할 수 있도록 하였다.

3. Primary Key의 데이터 타입을 고민했을 때, 일반적으로 BIGINT(long type)을 사용하는 것이 일반적이라고 알고 있어 그렇게 작성하였지만, 프로젝트의 규모를 고려했을 때 INT로 한정해도 충분할 것 같다. 찾아본 결과, 데이터 타입이 클수록 인덱스 크기가 증가하고 성능 저하 가능성이 있다는 점을 확인했다. 다만, 데이터 크기가 커지면 BIGINT가 필요할 수도 있으므로, 장기적인 확장성도 함께 고려하는 것이 중요하다는 점을 깨달았다.

4. 또한, AI를 사용할 경우 분산 시스템에서 데이터 정합성 문제가 발생할 가능성이 있으며, 예측 가능한 키 값으로 인해 보안이 취약해질 수도 있다는 점을 새롭게 알게 되었다. 이를 해결하는 방법 중 하나로 UUID를 Primary Key로 사용하는 방법을 접했다.

<ul>
<li>UUID는 0에 수렴하는 낮은 확률로 키 충돌이 발생하며, AI 없이도 고유한 식별자를 생성할 수 있음</li>
<li>하지만, 128비트(16바이트) 크기로 인해 인덱스 성능이 저하될 가능성이 있으며, 정렬이 어렵다는 단점도 존재한다.</li>
<li>따라서, UUID가 무조건적인 정답이라기보다는 AI와 UUID 중 프로젝트 특성에 맞는 방식을 선택하는 것이 중요하다는 점을 알게 되었다.</li>
<li>실제로 이전에 진행한 암호화폐 매매 자동화 음성 비서 프로젝트에서 Upbit API의 user ID가 UUID였던 점을 떠올리며, UUID의 사용 이유를 더 깊이 이해하게 되었다.</li>
</ul>

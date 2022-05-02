하둡 3일차
하둡 데스크탑용 , 서버용
tty > 내가 쓰는게 pts라고 나오는것, 터미널을 다른창에서 tty를 치면 pts가 다른게 나온다
HDFS의 상세 메커니즘
- 네임노드에서 클라이언트 위치와 데이터노드 위치를 고려해서 노드 목록 제공
네임 노드 포멧은 서버를 stop한 상태에서 해야한다. 
- 실질적인 데이터는 데이터 노드에 있다


HDFS
NOSQL | HBASE
SQOOP
RDBMS
######
NoSQL은 Not Only SQL, SQL 뿐만 아니다라는 의미를 지니고있다. 
즉, SQL을 사용하는 관계형 데이터베이스가 아닌 데이터베이스를 의미한다
수평 확장 가능한 분산 시스템
Schema-less
완화된 ACID
이처럼 BASE는 ACID와는 다르게 일관성을 어느정도 포기하고 가용성을 우선시한다. 
즉, 데이터가 조금 맞지 않더라도 일단 내려준다는 뜻이다.

대규모 데이터를 처리해야 하는데 RDMS는 성장 한계가 있어서 일관성과 무결성을 버리고 더 빠른 읽기 성능과
수평 확장이 가능한 DB가 필요해서
MONGO가 탄생
https://kciter.so/posts/about-mongodb
 NoSQL은 최대한 단순하면서 많은 데이터, RDBMS는 복잡하면서 무결성이 중요한 데이터에 적합하다고 생각한다.
무결성 : 관계형 데이터베이스에서 데이터의 정확성과 일관성을 유지하고, 데이터에 결손과 부정합이 없음을 보증하는 것을 의미한다.

간단하게 말하면, 트랜잭션이란 데이터베이스의 상태를 변경하는 논리적 작업 단위입니다.


DBMS는 데이터가 새로 들어올때 스키마를 만들어줘야해서 쉽게 데이터를 접근 할 수 없기 때문에
NOSQL의 등장 >> 기존 RDBMS와 틀리고 CAP이론이란 (가용성(서비스가 계속 이루어 져야함
전원 끊겼다고 통신 X되면 안됨), 일관성(데이터가 접근할때마다 바뀌어 있으면 안된다,모든사람이 같은내용을 볼 필요 없다?(모든 사람이 read,write를 할 필요 없다)) ,확장가능성(일관성과 조금 비슷하지만
PARTITION TOLERANCE 견디는것?,네트웤으로 분리가 되어 있다.))NOSQL은 CAP이론을 모두 만족하기에 힘들다

MONGO디비를 쓰는이유 비관계형 데이터를 관리하기 위해?  보통 문서 관련 작업할때 많이 쓰인다 (카카오에서 쓰인다)
MongoDB는 Document 기반 데이터베이스다. Database > Collection > Document > Field 계층으로 이루어져 있으며 
Document는 RDBMS의 Row에 해당한다. 계층은 RDBMS와 유사하다.


비동기는 배치 일괄? 시간이 지나더라도 서비스를 봐주는것

동기는 실시간
C+P 모든노드가 함께 퍼포먼스를 내야 하는 성능형   | 구글의 BIG TABLE, HYPER TABLE, HBASE
      - 대용량 분산, 성능보장형 서비스에 적합

A + P - 비동기화된 스토어 작업에 필수적   | DYNAMO, TOKYO cabinet, apache Cassandra , oraclr Coherence
      - SNS 서비스에 적합


C + A -시스템이 죽더라도 메시지 손실은 방지하는 강한 신뢰형(트렌젝션이 필요한 경우 필수적 )  | RDBMS(분산 처리가 안된다)


CAP이론

-----------------------------------------------------------------------
CAP 이론

Consistency(일관성) - 각각의 사용자가 같은 데이터를 볼 수 있다 == 모든 노드가 같은 시간에 같은 데이터를 보여줘야 한다
Availability(가용성) - 모든 사용자가 항상 읽고 쓸 수 있다 == 몇몇 노드가 다운되어도 다른 노드들에 영향을 주지 않아야 한다
Partition Tolerance(분산 가용성) - 물리적으로 분리된 분산 환경에서도 작동한다 == 일부 메시지를 손실하더라도 시스템은 정상 동작을 해야 한다

CA - 시스템이 죽을지언정 메시지 손실은 방지하는 강한 신뢰형(RealTime)
   ex) 전통적인 RDBMS가 해당, 트랜잭션이 필요한 경우 필수적
CP - 모든 노드가 함께 퍼포먼스를 내야하는 성능형
   ex) 구글의 BigTable과 HBase, MongoDB 등
AP - 비동기화된 서비스 스토어에 적합(Batch)
   ex) Dynamo, Apache Cassandra, CouchDB 등

RDBMS
장점 : 데이터 무결성과 정합성 보장, 정규화된 테이블 지원, 트랜잭션 지원
단점 : 확장성에 한계 존재, 클라우드 분산 환경에 적합하지 않음.
NoSQL
장점 : 웹 환경에서 다양한 정보를 검색하고 저장할 수 있음
단점 : 데이터에 대한 무결성과 정합성을 보장하지 않음.

RDBMS와 NoSQL의 사용시기

RDBMS
중대형 데이터베이스(10~100GB), ACID 특성을 엄격히 만족, 데이터가 밀접하게 연관, 높은 사양의 하드웨어 사용
NoSQL
높은 확장성을 지원해야하고, 동시에 접근이 일어날 수 있는 경우, 반드시 ACID가 보장될 필요는 없음. 낮은 예산을 가지고 있지만, 확장성이 높은 경우를 고려할 때 필요(웹 사이트나 소셜 서비스 구성등)


------------------------------------------------------------------------------

yarn이 분산처리를 어떻게 해라고 명령을 내린다? 구글링
Flume : cloudera 에서 2010년에 공개한 오픈소스 로그 수집 프레임워크로서
	대량의 로그데이터를 효율적으로 수집 및 모니터링이 가능하고
	실시간 전송을 지원함

	Agent + Collect 구조의 이벤트 Data 수집이 목표

zookeeper 

- 빅데이터 처리 기술
- 하둡의 분산 상호조정 서비스를 이용하여 일반적인 분산 응용프로그램을 구축

collecting > store > analysis > reporting/searching

 Batch : 일괄처리 - MapReduce, SPARK
   * RealTime : 실시간 - Flume, Kafka, splunk
   //ex) IoT, 버스, 날씨 등

pig
빅데이터 처리기술
대규모 데이터셋 탐색용 데이터 흐름 언어와 실행환경
하이브에 대비해서 프로그래밍 기능 제공
pig Latin이라는 데이터셋 플로우 제어 언어를 제공하며, 내부 컴파일러에 의해 맵리듀스 잡들로 변환
신속한 hdfs 데이터 분석시 활용됨

RAN
Data Lake 관리 플랫폼, Data Warehouse


그냥 키-값으로 이루어진 데이터가 정형 데이터 나머지는 다 비정형 데이터


wordcount , wordcount2
                             wordcount2 는 입력으로 다른형태의 텍스트 파일인 위키디피아 페이지를 사용함
                             컴바이너를 사용하여 
하둡 hdfs의 파일은 리눅스에 저장된 파일과 다르기 때문에 ls input하면 보이지 않는다
hadoop fs -mkdir /input               input 디렉토리 만들기
hadoop fs -mkdir /input/wex        
hadoop fs -rmr /output  << output 디렉토리 삭제, -r처럼 옵션을 -빼고 바로 붙혀서 쓸 수 있다
hadoop -fs -ls /output/..  output 디렉토리 view
hadoop -fs -cat /output/... 디렉토리 파일    <<Output 디렉토리 파일
hadoop fs -coptFromLocal /input/    < input 디렉토리에 data 복사

hdfs에 저장해서 효과적으로 자료를 활용하기
hdfs에 있는 input폴더의 자료를 mapreduce로 처리 하여 hdfs에 있는 output디렉토리에 다시 저장한다

hadoop fs -copyToLocal R.txt /input
hadoop fs -copyFromLocal R.txt /input
hadoop fs -ls /input/
파일 비교 diff README.txt.R.txt


--------------------------4일차

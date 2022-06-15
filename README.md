1 채용공고를 등록합니다
회사와 사용자 등록절차는 생략되므로 seed로 더미데이터를 생성하여 작성

2 채용공고를 수정합니다
post의 해당 공고문 내용을 수정
채용공고를 저장하는 post모델을 생성하여 여러 데이터를 seed로 생성
해당 공고문을 수정해야하므로 params로 접근하여 해당 공고문을 수정
이때 params로 받는 값은 post의 id와 같아야함

3 채용공고를 삭제합니다.
post의 해당 공고문 내용을 삭제
이것또한 해당 공고문을 삭제해야하므로 params를 이용하여 삭제
마찬가지로 params로 받는 값은 post의 id와 같아야함

4-1 채용공고 목록을 가져옵니다.
post의 모든 공고문을 불러옴
포스트를 매핑하여 detail(해당 기업의 다른 공고문아이디)과 message(공고문 내용)를 제외한 값을 응답

4-2 채용공고 검색 기능 구현
검색할 만한 키워드를 가지고 query를 이용하여 응답
query를 이용하여 name(회사이름), country(나라), position(포지션), tech(기술), employer_id(회사고유아이디)를 각각 응답
name과 employer_id 하나밖에 존재할 수 밖에 없으므로 findOne을 사용하여 query값과 비교
나머지는 여러개가 존재할 수 있으므로 findAll사용하여 query값과 비교
query로 넘어오는 값이 잘못된 값을 넣고 데이터베이스에 존재하지 않는다면 404 응답

5 채용 상세 페이지를 가져옵니다.
일반 공고문에는 포함시키지 않은 것들을 가져옴
detail과 message를 포함을 시켜 응답
params에 employer_id(회사고유아이디)를 입력하여 해당 회사 공고문 응답

6 사용자는 채용공고에 지원합니다
한명의 사용자는 한 공고문에만 한번 지원할 수 있도록 구현
지원자와 해당 회사고유아이디가 있는 공고문을 저장할 applicant(지원자)모델을 만듬
지원자가 지원한 회사는 회사고유아이디로 구분
지원자와 회사고유아이디는 params로 받아서 사용
지원이 완료된 사실을 알기위해 applicant 모델 컬럼에 defaultValue로 is_apply에 false를 저장
만약 지원자가 해당 회사의 공고문에 지원한다면 지원자와 회사고유아이디를 참인지 비교하고 is_apply가 참인지 비교
둘 다 참이면 해당지원자는 해당 공고문에 이미 지원했으므로 400응답 처리
거짓이면 지원을 할 수 있으므로 is_apply를 true로 update
지원자와 회사고유아이디를 응답해줌

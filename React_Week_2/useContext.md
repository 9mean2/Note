
# useContext 란

## (1) react context의 필요성 

#### 일반적으로 부모 컴포넌트 ➡  자식 컴포넌트로 데이털를 전달할 떄  ``Props`` 를 사용했습니다

#### 부모 ➡ 자식 ➡ 그 자식 ➡ 그자식의 자식 이런 현상들을 ``Prop drilling`` 현상이 일어난다


## ``Prop drilling``의 문제점은

#### 1. 깊이가 너무 깊어지면 이 prop이 어떤 컴포넌트로 부터 왔는지 파악이 어려워 진다.

#### 2. 어떤 컴포넌트에서 오류가 발생할 경우 추적이 힘들어지니 대처가 늦어질 수 밖에 없다

![[contextAPI.png]]

### 그래서 등장한 것이 바로 ``react context API`` 이며,  ``useContext hook``을 통해 우리가 쉽게 ``전역 데이터를 관리`` 할 수 있게 됐습니다.

## (2) context API  필수개념

#### - ``createContext`` : context 생성
#### - ``Consumer`` : context 변화 감지
#### - ``Provider`` : ㅏcontext 전달(to 하위 컴포넌트)
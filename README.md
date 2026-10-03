# hdac-smoking-abdominal-obesity
# 남경민봉수영 / 2023년 국민건강영양조사 기준 현재 흡연과 복부비만 연관성 분석
- 연구질문: 2023년 20세 이상 성인에서 현재 흡연은 복부비만 유병 여부와 관련이 있는가??
- 팀 구성 및 역할: 봉수영- 저장소 만들기 , 남경민 - 연구 제목 만들기
B1:비음주 상태는 알코올로 인한 간 질환, 심혈관계 손상, 일부 암종의 발병 위험 및 음주 관련 사고 위험을 낮추는 이점이 있을 것으로 예상됩니다. 그러나 비음주군을 분석할 때는 과거에 심각한 질환이나 건강 악화로 인해 술을 끊은 집단이 포함되는 '아픈 비음주자 효과(sick quitter effect)'를 반드시 고려해야 합니다. 이로 인해 단순 관찰 연구에서는 비음주군이 적당한 음주군에 비해 오히려 건강 지표가 불리하게 나타나는 'J-형' 또는 'U-형'관계를 보일 수 있습니다. 따라서 비음주와 건강 결과 간의 관계를 분석할 때는 과거 음주력, 연령, 기저 질환 등의 교란변수를 통제한 도메인 분석이 필수적입니다.
B2:
import numpy as np
import pandas as pd

# 1. 결측치 확인 및 코드 결측 처리 (income==9 등 NaN 처리 완료 전제)
ok_drink = df['drink'].notna().to_numpy()

# 2. 도메인 지시변수 생성 (자료를 잘라내지 않고 전체 길이 유지)
nodrink = ((df['drink'] == 1) & ok_drink).to_numpy()  # 노출군: 비음주
drinker = ((df['drink'] != 1) & ok_drink).to_numpy()  # 비노출군: 음주자 (drink 2, 3)

# 3. 층화 분석용 DOMS 딕셔너리 설정
DOMS = {
    '전체': np.ones(len(df), bool),
    '비음주(노출군)': nodrink,
    '음주(비노출군)': drinker,
}


# 4. Table 1 생성 함수 정의
def row_cont(label, var):
  r = {'특성': label, 'n': int(df[var].notna().sum())}
  for name, dom in DOMS.items():
    th, se = svymean_domain(df[var], w, ST, PS, dom)
    r[name] = f'{th:.1f} ({se:.2f})'
  return r


def row_cat(label, mask):
  mask = np.asarray(mask, float)
  r = {'특성': label, 'n': int(mask.sum())}
  for name, dom in DOMS.items():
    th, se = svymean_domain(mask, w, ST, PS, dom)
    r[name] = f'{th * 100:.1f}'
  return r


# 5. Table 1 조립
t1_team = pd.DataFrame([
    row_cont('연령 (세)', 'age'),
    row_cat('65세 이상', df.age >= 65),
    row_cat('남성', df.sex == 1),
    row_cat('읍면 거주', df.urban == 2),
    row_cont('체질량지수 (kg/m²)', 'bmi'),
    row_cat('비만 (BMI ≥ 25)', df.bmi >= 25),
    row_cont('수축기혈압 (mmHg)', 'sbp'),
    row_cat('고혈압 유병', df.htn == 1),
    row_cont('공복혈당 (mg/dL)', 'glucose'),
    row_cat('현재흡연', df.smk == 1),
    row_cat('규칙적 운동', df.exercise == 2),
])


| 이름 | 역할 | 기술 스택 |
| --- | --- | --- |
| 홍길동 | 프론트엔드 | React |
| 김철수 | 백엔드 | Spring |





| 이름 | 역할 | 사용 기술 | 사용기술
| --- | --- | --- | --- |
| 홍길동 | 팀장 | Python |
| 김철수 | 팀원 | JavaScript |

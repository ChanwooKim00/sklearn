# 사이킷런
## 교차검증 (KFold, stratifiedKfold)

1. KFold
    - KFold 란? 
        * 세트 개수를 설정하면 해당 개수로 학습_데이터, 테스트_데이터 로 나눠서 학습과 테스트를 진행한다.
    - KFold 문제점
        * 학습_데이터와 테스트_데이터 의 세트에 타겟 값이 골고루 분포하지 않을 경우가 발생할 수 있다
        * 예를 들어, 3가지 타겟(0,1,2)이 있는 데이터를 3 세트로 나눌 경우 학습 데이터에 타겟 2 가 포함 되지 않으면 2를 예측 할 수 없다.
    - 사용 예)
    ~~~python
        # kfold 선언 및 세트 개수 설정
        kfold = KFold(n_split=3)
        # 교차 검증 진행
        for train_idx, test_idx in kfold.split(features) : 
            # 학습 데이터, 테스트 데이터 추출
            # 데이터
            X_train, X_test = features[train_index], features[test_index]
            # 타겟(=라벨)
            Y_train, Y_test = label[train_index], label[test_index]

            # 학습
            ${검증모델}.fit(X_train, Y_train)
            # 예측
            pred = ${검증모델}.predict(X_test)
            # 정확도 측정
            acc = accuracy_score(y_test,pred)
    ~~~

2. StratifiedKFold
    - StratifiedKFold 란?
        * 데이터의 세트 분할 시 타겟(=라벨)의 속성값의 개수를 동일하게 나눠 세트를 구성한다.
        * 따라서 학습 데이터 세트와 테스트 데이터 세트에 라벨이 몰리거나 누락되는 경우를 방지한다.
    - 사용 예)
    ~~~ python
        # StratifiedKFold 선언 및 세트 개수 설정
        skfold = StratifiedKFold(n_split=3)
        # KFold 와 달리 교차 검증 진행에 features와 label을 같이 넣어준다.
        # label 에 따라 세트를 나누기 때문에
        for train_idx, test_idx in skfold.split(features, label) : 
            # 학습 데이터, 테스트 데이터 추출
            # 데이터
            X_train, X_test = features[train_index], features[test_index]
            # 타겟(=라벨)
            Y_train, Y_test = label[train_index], label[test_index]

            # 학습
            ${검증모델}.fit(X_train, Y_train)
            # 예측
            pred = ${검증모델}.predict(X_test)
            # 정확도 측정
            acc = accuracy_score(y_test,pred)
    ~~~
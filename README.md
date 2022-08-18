# AI_Section4_Project

## Repository 설명

- AI_11_노희섭.ipynb ⇒ 프로젝트에 사용한 코드
- 깃허브 업로드 용 발표 자료
    - 프로젝트를 발표할 때 사용한 PPT 파일을 수정하여 GitHub에서 바로 볼 수 있게 PDF로 수정
    - 아래 내용보다 더 자세하게 설명이 되어 있음.

## 프로젝트에서 풀고자 하는 문제

- 필사로 ‘갓생’을 사는 이들을 위해 필사 문장을 만들어내는 딥러닝 모델 생성

## 프로젝트 진행 과정

- 데이터 수집
    - 상실의 시대.txt
        - 무라카미 하루키의 장편 소설
        - txt 파일로 구할 수 있었던 소설 중 가장 긴 분량
- 데이터 전처리
    - 문장이 끝나지 않았지만 물리적인 공간의 부족(인쇄)으로 줄이 바뀌는 것을 바뀌지 않게 수정
- 딥러닝 모델 활용
    - Mini-GPT
        - 문장에서 벡터로 바꾸는 작업 진행
        - 단어 벡터 구성
        - 임베딩 레이어 구현
        - 트랜스포머 블록을 레이어로 구현
        - 모델 구현
    - LSTM(ver1)
        - LSTM 모델 구현
    - LSTM(ver2)
        - 노드 수, Dropout, optimizer 조정
    - LSTM(ver3)
        - 좀 더 복잡하게 수정
- 딥러닝 모델 별 결과 비교

## 데이터셋 설명

- 데이터 출처: 무라카미 하루키의 ‘상실의 시대’
- 전체 데이터 셋: 6713 * 1

## 문제 상황 해결 과정(분석 기법, 모델 등)

- 필사 문장 생성에 적절하도록 문장을 생성할 수 있는 딥러닝 모델 선정
    - mini-GPT
        - model
            ![image](https://user-images.githubusercontent.com/88868181/185322525-a5b35e4c-5e52-4559-b7ad-00f6df3ce779.png)

        - epoch
            - 최대 500회로 설정하였으나 데이터의 부족으로 유의미한 성능의 향상이 이루어지지 않았음.
            - 그래서 학습이 이루어지는 와중에 학습을 중단시켰음.
    - LSTM(여러 모델로 수정 학습)
        - ver1
            
            ![image](https://user-images.githubusercontent.com/88868181/185322722-2e8c1950-fd4d-4de1-aba1-eaf1359c2dff.png)
            
            - epoch 20, bath_size 128
            
        - ver2
            
            ![image](https://user-images.githubusercontent.com/88868181/185323070-9c113943-7f2a-42a8-b1de-f275a520f0b3.png)

            
            - 멈출 때까지 임의의 시작 텍스트로 다양한 문장 자동 생성(batch_size 128)
            - 사용되는 문자의 수: 1,359
            - 학습할 구문의 수: 123,441
        - ver3
            
            ![image](https://user-images.githubusercontent.com/88868181/185323262-230acd12-299b-4144-8a2d-cc41620f84b4.png)

            
            - 멈출 때까지 임의의 시작 텍스트로 다양한 문장 자동 생성(batch_size 128)
            - 사용되는 문자의 수: 1,348
            - 학습할 구문의 수: 123,443

## 결과 정리

- mini-GPT
    
    ![image](https://user-images.githubusercontent.com/88868181/185323407-292d89ae-e62d-4f97-815b-c22f8548e47d.png)

    
- LSTM(ver1)
    
    ![image](https://user-images.githubusercontent.com/88868181/185323572-837b143a-d16b-4493-b2a3-f4f454d5a504.png)

    
- LSTM(ver2)
    
    ![image](https://user-images.githubusercontent.com/88868181/185323683-37237155-6290-46a4-ad58-d5e344a8aef0.png)

    
- LSTM(ver3)
    
    ![image](https://user-images.githubusercontent.com/88868181/185323818-e902cf4e-7401-4f5d-9019-84a9bb3d9524.png)

    

## 한계점 및 느낀점

- 한계점: 학습 데이터가 매우 부족했음.
    - 이번 프로젝트를 위해 참고한 다른 프로젝트의 경우 아래와 같은 데이터를 사용하였음.
        - mini-GPT는 800만 자(박경리 ‘토지’)
        - LSTM 논문은 100만 자(구약 성경)
    - 하지만 이번 프로젝트 상실의 시대는 37만 자로 절대적으로 부족했기에 말이 안되는 문장이 많이 나왔음.
- 느낀점: 도서출판 시장이 도서 정가제, 도서 인구 감소, OTT 등으로 경쟁력을 잃어가고 있는 상황에서 작가들과의 협업을 통해 MZ세대에 접근하여 새로운 비즈니스 모델을 시도하는 것은 어떨까? 하는 생각이 들었음.

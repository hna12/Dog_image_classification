# Dog Image Classification

## 🐶Introduction
Purpose: 총 14종의 강아지 품종 이미지를 분류하는 모델 만들기
<br/>
species | label | species | label
---|---|---|---|
코카스파이니엘 | 1 | 삽살개 | 8
푸들 | 2 | 시베리안 허스키 | 9
그레이하운드 | 3 | 말라뮤트 | 10
말티즈 | 4 | 닥스훈트 | 11
퍼그 | 5 | 웰시코기 | 12
비숑 | 6 | 리트리버 | 13
진도개 | 7 | 포메라니안 | 14

</br>

## 🐶Methods and Materials
1. Materials
- NAVER, GOOGLE Image
- 총 11,289 장
2. Methods
- Crawling method: Selenium library
- Preprocessing: Resizing(crawling한 이미지 사이즈가 제각각이라 resizing 작업으로 동일하게 만듬), Zero centering, Gray scale
- Modeling
    - ResNet50
    - Transfer learning
      - conv layer 일부 재학습(12층, 15층, 30층) + 분류기 학습
      - Dropout
    - Fine-tuning

## 🐶Results
* TABLE 1) 이미지 사이즈변화에 따른 성능 변화 (gray scale처리, conv layer 15층 + 분류층 학습)
<br/>

. | 150x150, 10e | 200x200, 10e | 220x220, 8e
---|---|---|---|
train accuracy | 0.9260 | 0.9387 | 0.9312
test accuracy | 0.8136 | 0.8441 | 0.0.8539
after fine tuning |  | 0.8565 |  |

</br>

* TABLE 2) Model 수정에 따른 성능 변화 (data int화처리, 180x180, no gray scale)
<br/>

. | 12층, Drpout(0.5) 1번 | 12층, Dropout(0.5) 2번 | 30층, Dropout(0.5) 1번
---|---|---|---|
train accuracy | 0.7837 | 0.9633 | 0.9922
test accuracy | 0.8667 | 0.8940 | 0.8887
after fine tuning | 0.8760 | 0.8920 | 0.8920

</br>

## 🐶Discussion
1. TABLE1) 
- 이미지가 커짐에 따라 확실히 정확도가 높아지는것을 확인
- RAM에 부담이 안되는 크기에 정확도가 가장 컸던 200x200, 10e만 fine tuning 실행해보니 accuracy가 조금 상승되는것을 확인할 수 있었다.
2. TABLE2) 
- gray scale 처리를 하지 않고 color image를 사용하고 drop out수, conv layer학습하는 층 수를 변경했더니 최대 89%까지 증가시켰다.
- Model을 바꿔도 accuracy가 같다는건 데이터 측면에서 손봐야한다는 것
3. 성능을 높이기위해 
   1. overfitting 방지: augmentation기법을 사용해 양 늘리거나 FC층 변경
   2. dataset 품질 개선: 잘못된 데이터 삭제
4. Resize의 경우 1차원을 3차원으로 변경 후 resize를 한다면 data가 너무커서 오류가 발생한다. 그러므로 repeat이전 1차원에서 resize를 하고나서 그 다음 3차원으로 하는 순으로 변경하니 오류가 해결되었다.
5. 크롤링한 이미지들을 pickle파일로 저장했다. 이를 다시 불러와 resize를 하면 tensor형식으로 저장되는데 이때 train & test로 split을 하게되면 오류가 발생한다. 이를 통해 train 과 test는 array형식만 넣을 수 있다는 것을 알게되었다. 그러므로 tensor 형식을 numpy array형식으로 형변환을 해야 train & test로 split이 가능하다.

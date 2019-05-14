## NMT
Neural Machine Translation

190128, 이대 영한 번역 자문

![2](https://user-images.githubusercontent.com/38748880/51825474-2f418d80-2328-11e9-8c17-c6fe8dc60ded.png)

김기헌의 https://github.com/kh-kim/simple-nmt

코드를 customize 시킨 코드.

기존의 python ~ 식으로 돌리는 코드를 jupyter notebook 으로 돌려서 그래프를 찍을 수 있게 함


# 1. 데이터 split

데이터는 data 파일에, [corpus.en, corpus.ko] 식으로 병렬 코퍼스 상을 넛고
python data/build_corpus 를 이용하여 훈련, 검증 셋을 만든다
ex) [corpus.en, corpus.ko] -> [corpus.train.en, corpus.train.ko, corpus.valid.en, corpus.valid.en]

Split corpus to train-set and valid-set
```
$ python ./data/build_corpus.py -h
```
usage: build_corpus.py [-h] --input INPUT --lang LANG --output OUTPUT
                       [--valid_ratio VALID_RATIO] [--test_ratio TEST_RATIO]
                       [--no_shuffle]
example usage:
```
$ ls ./data
corpus.en  corpus.ko
$ python ./data/build_corpus.py --input ./data/corpus --lang enko --output ./data/corpus
total src lines: 384105
total tgt lines: 384105
write 7682 lines to ./data/corpus.valid.en
write 7682 lines to ./data/corpus.valid.ko
write 376423 lines to ./data/corpus.train.en
write 376423 lines to ./data/corpus.train.ko
```

# 2. Train
```
train_custom.ipynb
```

커스터마이즈 한 코드는, train -> train_custom, translate -> translate_customize, 
simple_nmt/rl_trainer->simple_nmt/rl_trainer_custom, simple_nmt/_custom -> simple_nmt/trainer_custom

훈련 시 train_custom을 쥬피터로 열어서 돌린다. 하이퍼 파라미터는 class 형식으로 지정되어있어서 바꾸면 된다

주로 바꿀 부분은 아래 2 파라미터다, 근데 그래프를 보니 훈련은 20에서 끊으면 될거같고, 강화학습 그래프는 들쭉날쭉이라 그래프를 보고 몇번째 epoch의 모델을 사용할지 결정해야 할 거 같다
self.n_epochs       = 40  #22  # Number of epochs
self.rl_n_epochs    = 20  #15  # Number of epochs for reinforcement

# 3. Test
```
translate_customize.ipynb
```
테스트는 translate_customize.ipynb로 한다. 결과를 txt로 출력하는 부분도 추가했다

![1](https://user-images.githubusercontent.com/38748880/51825385-03bea300-2328-11e9-853d-dcdb01459e37.png)

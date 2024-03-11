## 이미지 스프라이트 최적화

### 실험 1. JPG와 PNG 파일들이 단일 파일로 존재 할 때 (총 20MB)

![resultOne.PNG](https://i.imgur.com/hfHmRqX.png)

![resultOne2.PNG](https://i.imgur.com/mIoYIXw.png)

### 실험 2. PNG 이미지 스프라이트로 파일들을 하나의 파일로 만들 때 (총 90MB)

![resultSprite.PNG](https://i.imgur.com/mmOq2MB.png)

![resultSprite2.PNG](https://i.imgur.com/RPMhfAY.png)

### 실험 3. JPG 이미지 스프라이트로 파일들을 하나의 파일로 만들 때 (총 20MB)

![resultSpriteJpg.PNG](https://i.imgur.com/V9gvd1k.png)

![resultSpritepg2.PNG](https://i.imgur.com/C1b8UOE.png)

1차 결론 : 파일을 40개를 하나의 이미지 스프라이트로 만들어 사용 했을 때 오히려 높은 LCP를 기록하였다. LCP는 가장 큰 컨텐츠가 로딩되는데 걸리는 시간이고 이미지 스프라이트가 20mb, 90mb의 경우 매우 큰 용량을 나타내므로 시간이 오래 걸릴 수 밖에 없다.

### 실험 4. 100x100의 작은 사이즈를 이미지 스프라이트로 만들기

![100Image.PNG](https://i.imgur.com/7thAExH.png)

![100ImageSprite.PNG](https://i.imgur.com/0cpi5Wr.png)

(위 : 45개의 100x100 사이즈의 개별파일. 아래 : 1개의 100x100 사이즈의 이미지 스프라이트 파일)

2차 결론 : 작은 이미지의 경우 CLS가 개별파일의 경우 0.7로 이미지 스프라이트를 사용 했을 때 보다 훨씬 많이 걸린것을 알 수 있다. 100x100 사이즈르 매우 작은 크기의 이미지 스프라이트는 성능 향상에 유의미한 결과를 줄 수 있다는 것을 확인 할 수 있다.

### 실험 6. 500x500의 작은 사이즈를 이미지 스프라이트로 만들기

![500result.PNG](https://i.imgur.com/N9OLjC3.png)

![500result2.PNG](https://i.imgur.com/MyBIHIj.png)

4차 결론 : 500x500의 사이즈의 경우 이미지 스프라이트가 LCP가 0.2 더 크고 CLS의 경우 단일 파일이 0.32가 더 높다. 100,200 사이즈의 경우 모든 면이 이미지 스프라이트가 유리했지만 500의 경우 LCP는 단일 파일이 더 유리하고 CLS는 이미지 스프라이트가 더 유리하다

### 이미지 스프라이트 최종 결론

- 사이즈가 커질수록 이미지 스프라이트의 효율은 떨어지며 **2024년 03월 11일 기준** 500x500의 사이즈가 넘어가면 이미지 스프라이트를 사용하는 것을 고려해보는것이 좋다.

## WEBP를 이용한 최적화

200x200 사이즈의 png파일 45개의 `크기` : 1.05MB, `디스크 할당 크기` : 1.05M

200x200 사이즈의 webp파일 45개의 `크기` : 130KB, `디스크 할당 크기` : 360KB

png로 45개의 파일의 성능을 측정한 경우 LCP가 `1.9s` CLS가 `0.994s`가 나왔다.

webp으로 파일의 성능을 측정한 경우 LCP가`1.6s` CLS가 `0.504s`가 나왔다.

이미지 스프라이트의 경우 0.2 정도의 LCP만 차이가 났다.

![Mqb1Bep.png](https://i.imgur.com/Mqb1Bep.png)

화질 차이의 경우 위와 같은 차이를 보였다 (좌 : png, 우 :webp)

WEBP의 경우 많은 압축을 시켜주었지만 그만큼 화질의 손상이 가기 때문에 잘 판단하여야한다.

# Project : 개선된 U - Net 모델 만들기
U-Net을 통한 시맨틱 세그멘테이션 결과가 충분히 만족스러우신가요? 어느정도 동작하는 것 같긴 하지만 좀더 개선할 여지도 보일 것입니다.  

2018년에 U-Net++라는 논문이 나왔습니다. 이 논문은 기존에 아주 단순하면서도 세그멘테이션에서 효과를 발휘했던 U-Net의 네트워크 구조에 DenseNet의 아이디어를 가미하여 성능을 개선한 모델입니다.  

그래서 모델의 구조 자체는 아래 그림에서 보는 것처럼 별다른 설명이 없이도 직관적으로 이해가 가능한 수준입니다. 오늘 소개되었던 U-Net의 모델 코드를 조금만 수정 확장하면 충분히 구현할 수 있을 것입니다. 그래서 오늘의 과제는 바로 U-Net++ 모델을 스스로의 힘으로 직접 구현해 보고, U-Net을 활용했던 도로 세그멘테이션 태스크에 적용하여 U-Net을 썼을 때보다 성능이 향상되었음을 확인해 보는 것입니다. 정성적으로는 두 모델의 세그멘테이션 결과를 시각화해서 비교해 볼 수 있을 것이고, 정량적으로는 동일 이미지에 대한 IoU값을 비교해 보면 될 것입니다.  


## 회고


##### 발생한 에러1:  ResourceExhaustedError: OOM when allocating tensor with shape
해결방법은 크게 세가지이다. 첫째, 저장한 후에 jupyter notebook을 다시 시작한다. 둘째, Memory 자원의 부족으로 생긴 문제이기 때문에 batch_size을 줄여준다. 일반적으로 batch_size는 2^n이므로 지수 하나를 줄인다. 이 문제로 해결하였다. 기존의 배치 사이즈가 16이었으나, 이를 4로 줄인 결과 에러가 발생하지 않았다. 이 밖에 사용하는 프로그램 이외에 다 종료해서 Memory 사용을 줄여서 다른 GPU Memory 사용에 대한 소스를 없애는 방법이 있다고 한다.


##### 발생한 에러2:  PermissionDeniedError: Read-only file system
model.save()에서 PermissionDeniedError: Read-only file system 에러가 발생하였다. 파일 경로를 os.getenv('HOME')+'/aiffel/data/training/semantic_segmentation/model_unet_pp.h5'에서 os.getenv('HOME')+'/aiffel/semantic_segmentation/model_unet_pp.h5'으로 바꾼 결과 에러가 해결되었다.(갓상현님이 도와주셨다)  
에러가 발생한 이유는 잘 모르겠다.

##### 결과 
원인은 아직 발견하지 못했으나, U-Net++ 모델의 IoU 가 더 낮게 나왔다.

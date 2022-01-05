##### 발생한 에러1:  ResourceExhaustedError: OOM when allocating tensor with shape
해결방법은 크게 세가지이다. 첫째, 저장한 후에 jupyter notebook을 다시 시작한다. 둘째, Memory 자원의 부족으로 생긴 문제이기 때문에 batch_size을 줄여준다. 일반적으로 batch_size는 2^n이므로 지수 하나를 줄인다. 이 문제로 해결하였다. 기존의 배치 사이즈가 16이었으나, 이를 4로 줄인 결과 에러가 발생하지 않았다. 이 밖에 사용하는 프로그램 이외에 다 종료해서 Memory 사용을 줄여서 다른 GPU Memory 사용에 대한 소스를 없애는 방법이 있다고 한다.


##### 발생한 에러2:  PermissionDeniedError: Read-only file system
model.save()에서 PermissionDeniedError: Read-only file system 에러가 발생하였다. 파일 경로를 os.getenv('HOME')+'/aiffel/data/training/semantic_segmentation/model_unet_pp.h5'에서 os.getenv('HOME')+'/aiffel/semantic_segmentation/model_unet_pp.h5'으로 바꾼 결과 에러가 해결되었다.(갓상현님이 도와주셨다)  
에러가 발생한 이유는 잘 모르겠다.

##### 결과 
원인은 아직 발견하지 못했으나, U-Net++ 모델의 IoU 가 더 낮게 나왔다.

- [Volumes](#volumes)
  - [volume이 bind mount보다 좋은 이유](#volume이-bind-mount보다-좋은-이유)
  - [볼륨 생성](#볼륨-생성)
  - [볼륨 목록 확인](#볼륨-목록-확인)
  - [볼륨 삭제](#볼륨-삭제)
  - [컨테이너에 볼륨 연결](#컨테이너에-볼륨-연결)

https://docs.docker.com/storage/volumes/

# Volumes

## volume이 bind mount보다 좋은 이유
- 백업이나 이동이 쉬움
- Docker CLI나 Docker API로 관리 가능
- 리눅스와 윈도우 모두에서 사용 가능
- 여러 컨테이너 간에 안전하게 공유 가능
- 볼륨 드라이버를 통한 확장성
- 컨테이너로 볼륨 미리 채우기 가능: 컨테이너가 시작될 때 필요한 데이터가 이미 볼륨에 준비되어 있어, 데이터를 로드하는 시간 단축
- Mac과 Windows에서 높은 성능 제공

![볼륨](https://docs.docker.com/storage/images/types-of-mounts-volume.webp?w=450&h=300)

## 볼륨 생성
```bash
docker volume create my-vol
```

## 볼륨 목록 확인
```bash
docker volume ls
```

## 볼륨 삭제
```bash
docker volume rm my-vol
```

## 컨테이너에 볼륨 연결
```bash
docker run -v my-vol:path/ my-image
```
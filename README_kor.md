# Samsung Galaxy M23/F23 SM-M236B/SM-E236B (m23xq)의 OrangeFox 리커버리 기기 구성

## 기기 스펙
기본    | 스펙 구성표
--------:|:----------------------
칩셋  | 퀄컴 스냅드래곤 750G
CPU      | Octa-core (6x1.8ghz Kryo 570 & 2x2.2ghz Cortex A77)
GPU      | Adreno 619
메모리   | 6GB RAM (LPDDR4X)
저장공간  | 128GB
출시 당시 Android 버전 | Android 12, OneUI 4.1
배터리  | Li-ion 5000mAh, non-removable
디스플레이  | LCD, 120Hz, 525 nits, 6.6인치, 1080 x 2408픽셀, 20:9 ratio

## 기기 사진
<img src="https://images.samsung.com/is/image/samsung/p6pim/br/sm-m236bzglzto/gallery/br-galaxy-m23-5g-sm-m236-422397-422397-sm-m236bzglzto-532669053?$1300_1038_PNG$" width="100%"/>

## 커널 소스
순정 ROM에서
```
m23xqxx-user 14 UP1A.231005.007 M236BXXU5DWL1 release-keys
```

## 빌드
자세한 내용은 https://wiki.orangefox.tech/en/dev/building 을 참조하세요.

## 컴파일 방법
먼저 twrp-12.1 트리를 저장소에 초기화합니다:

```
mkdir ~/OrangeFox_sync
cd ~/OrangeFox_sync
git clone https://gitlab.com/OrangeFox/sync.git # (or, using ssh, "git clone git@gitlab.com:OrangeFox/sync.git")
cd ~/OrangeFox_sync/sync/
./orangefox_sync.sh --branch 12.1 --path ~/fox_12.1
mkdir -p .repo/local_manifests
```

그런 다음 로컬 매니페스트에 추가합니다(만약 .repo/local_manifest 디렉토리가 없다면 해당 디렉토리를 만들고 빈 파일을 생성한 후 twrp.xml과 같은 이름으로 저장하세요):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote name="me" 
        fetch="https://github.com/BoomboxRapsody" />
  <project name="android_device_samsung_m23xq_ofrp" path="device/samsung/m23xq" remote="me" revision="ofox_12.1"/>
</manifest>
```
이제 소스를 동기화할 수 있습니다:
```
repo sync
```
마지막으로 다음을 실행합니다:
```
source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
lunch twrp_m23xq-eng
mka adbd recoveryimage
```

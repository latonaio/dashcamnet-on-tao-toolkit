# dashcamnet-on-tao-toolkit
dashcamnet-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて DashCamNet の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- DashCamNet
- Docker
- TensorRT Runtime

## DashCamNetについて
DashCamNet は、移動カメラから画像内の車、人、道路標識、および二輪車を検出し、カテゴリラベルを返すAIモデルです。  
DashCamNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順

### engineファイルの生成
DashCamNet のAIモデルをデバイスに最適化するため、ResNet18 における DashCamNet の .etlt ファイルを engine file に変換します。  
現時点におけるNVIDIAの仕様では、GPUのアーキテクチャごとに engine file の生成が必要です。  
本レポジトリに格納された dashcamnet.engine は、実際に生成される engine file の参考例です。  
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。

```
tao-convert:
	docker exec -it dashcamnet-tao-toolkit tao-converter -k tlt_encode -d 3,544,960 -e /app/src/dashcamnet.engine /app/src/resnet18_dashcamnet_pruned.etlt 
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された DashCamNet の AIモデルを Deep Stream 上で動作させる手順は、[dashcamnet-on-deepstream](https://github.com/latonaio/dashcamnet-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである dashcamnet.engine は、[dashcamnet-on-deepstream](https://github.com/latonaio/dashcamnet-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  


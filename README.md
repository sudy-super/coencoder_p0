# coencoder_p0

## 環境構築

> [!IMPORTANT]
> 注意: 記載してある手順は特に注釈がない限り全ノードで行ってください。

1. venv

```bash
python -m venv train
source train/bin/activate
```

2. レポジトリのクローン
```bash
git clone https://github.com/sudy-super/coencoder_p0.git
cd coencoder_p0
```

3. 依存ライブラリのインストール
```bash
pip install git+https://github.com/huggingface/transformers.git
pip install accelerate sentencepiece wandb packaging wheel nvitop scikit-learn datasets
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
apt-get install ninja-build
pip install numpy==1.23.5 flash-attn deepspeed==0.15.4
```
※ 後述のbashファイル実行時にcpu_adamが初期化できないエラーが発生する可能性があります。ninja-buildのインストールで発生可能性を低減できますが、確実ではないので発生した場合は以下のリンクを参考に対処してください。

[参考になりそうなdeepspeedのissueページ](https://github.com/microsoft/DeepSpeed/issues/1846)

## 実行 (マスターノードのみでの操作)

マスターノードや使用するノードを変えたい場合はbashファイル・ホストファイルを個別に編集してください。

また、wandbにログを記録したい場合はfinetune_default.pyまたはfinetune_ori_loader.pyの31行目に初期化処理を記述してください。

* RoCEオフ、nvlinkオフ、独自データローダーを使用する場合:
```
bash train_normal.sh
```

* RoCEオン、nvlinkオフ、独自データローダーを使用する場合:
```
bash train_r.sh
```

* RoCEオン、nvlinkオン、独自データローダーを使用する場合:
```
bash train_r_n.sh
```

* RoCEオン、nvlinkオン、デフォルトのデータローダーを使用する場合:
```
bash train_r_n_d.sh
```
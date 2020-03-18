# poodl-client
以下、POODL-Client のセットアップ方法について


## python2系のセットアップ
### pyenvがある場合
```
pyenv install 2.7.16
pyenv virtualenv 2.7.16 2.7.16_poodl-client
pyenv local 2.7.16_poodl-client
python -V
```

### Windows Anaconda
```
conda install --name 2.7.16 python=2.7.16
conda activate 2.7.16
# unix系の場合は source activate 2.7.16 
```


## Electronアプリの開発・ビルド
### 準備
```
cd project
npm install
```

### ホットリロード付きの開発モード
```
npm run electron:serve
```

### ビルド
```
npm run electron:build
```

ビルドしたアプリケーションは、`project/dist_electron`フォルダに出力されます。

- WindowsではZIPファイル、またはNSISインストーラが出力されます(デフォルト設定はZIPファイル)
    - `electron-builder.yml` 内の`win` の `target` を `zip` するとZIPで、何も指定しないとNSISになります
    - NSISインストーラについて
        - `{アプリケーション名} Setup {バージョン}.exe` が出力されます
        - 実行すると、アプリケーションが `Programfiles` フォルダにインストールされます
- Macでは、そのまま実行可能ファイルの形で出力されます

#### ビルドオプション
ビルドの際に、アプリアイコンやインストーラ等のオプションが追加できます。  
`electron-builder.yml` を変更することで反映されます。

以下、オプションのキーについて  
(一部のみ紹介。その他詳細は[こちら](https://www.electron.build/configuration/configuration))
- `productName` ：実行可能ファイルの名前
- `appId` ：WindowsでのAUMID(ストアアプリの識別子)、MacでのCFBundleIdentifier
- `copyright` ： コピーライト記述。Copyright © year ${author}
- `mac`、`win`、`linux` ：OS別オプション
    - `icon` ：アプリケーションアイコン( `256×256` サイズ以上の画像)
    - `target` : ビルドしたアプリケーションの形式。ないとインストーラになる
        - `zip` : アプリケーションのフォルダがZIP圧縮されたものが出力される
Kind（Kubernetes in Docker）は、マルチノードなKubernetesクラスタをローカル環境で簡単にセットアップするためのツール。<br>
以下は、Kindを使用してKubernetesクラスタを構築するための基本的な手順。

### 必要なツールのインストール

1. **Dockerのインストール**:
   - KindはDockerコンテナを使用してクラスタを作成します。まず、Dockerをインストールしてください。
   - [Dockerの公式サイト](https://www.docker.com/get-started)からインストールできます。

2. **Kindのインストール**:
   - KindはGoで書かれているため、Goがインストールされている場合は以下のコマンドでインストールできます。
   ```bash
   GO111MODULE="on" go install sigs.k8s.io/kind@v0.20.0
   ```
   - または、バイナリを直接ダウンロードしてインストールすることもできます。
   ```bash
   curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
   chmod +x ./kind
   mv ./kind /usr/local/bin/kind
   ```

3. **kubectlのインストール**:
   - Kubernetesクラスタを操作するためにkubectlが必要です。
   - [kubectlの公式ドキュメント](https://kubernetes.io/ja/docs/tasks/tools/)に従ってインストールしてください。

### Kindクラスタの作成

1. **シングルノードクラスタの作成**:
   - Kindを使用してクラスタを作成します。以下のコマンドを実行してください。
   ```bash
   kind create cluster
   ```

2. **クラスタの確認**:
   - クラスタが正しく作成されたか確認するために、以下のコマンドを実行します。
   ```bash
   kubectl cluster-info --context kind-kind
   ```
   - さらに詳細に知りたい場合
   ```bash
   kubectl cluster-info dump
   ```

### クラスタの操作

- クラスタが作成されたら、通常のKubernetesクラスタと同様にkubectlを使用して操作できます。

### `kubectl`コマンドを使用するための環境変数の設定

`kind`で作成したKubernetesクラスタを操作するために、`KUBECONFIG`環境変数を設定する必要があります。<br>
デフォルトでは、クラスタ名は`kind`になります。そのため、本サンプルでは`--name`オプションに`kind`を指定します。

以下のコマンドを実行して、`KUBECONFIG`を設定してください。
```bash
export KUBECONFIG="$(kind get kubeconfig --name="kind")"
```

### クラスタの削除

クラスタを削除するには、以下のコマンドを実行します。

```bash
kind delete cluster --name kind
unset KUBECONFIG
```
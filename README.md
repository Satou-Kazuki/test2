# チーム開発感ある環境を整える（暇だったら）
# 最初にやること
# Githubのアカウント作成 
- 参考:https://www.sejuku.net/blog/73468
# gitインストール
- https://git-scm.com/
- 参考:https://kitsune.blog/engineer/git
# VSCodeインストール 
- https://azure.microsoft.com/ja-jp/products/visual-studio-code/
- 参考github連携：https://breezegroup.co.jp/202102/vscode-github-windows/
- 参考Docker連携：https://qiita.com/Yuki_Oshima/items/d3b52c553387685460b0
# Dockerインストール
- https://www.docker.com/
- 参考：https://www.pasonatech.co.jp/workstyle/column/detail.html?p=2675
- 使ってるイメージファイル：https://hub.docker.com/r/jupyter/datascience-notebook/tags?page=1&ordering=last_updated
- 　補足：DockerがBIOSのCPUの仮想化設定がDisableだとかで起動しない場合。https://mrkmyki.com/docker%E3%82%92%E8%B5%B7%E5%8B%95%E3%81%97%E3%82%88%E3%81%86%E3%81%A8%E3%81%97%E3%81%9F%E3%82%89%E3%80%8Chardware-assisted-virtualization-and-data-execution-protection-must-be-enabled-in-the-bios
- 　ちなみに、AMDのCPUの場合BIOS設定でSVMをEnableにすると動くかもしれないし動かないかもしれない。

# 上記インストールが終わったら、下記参考ページ
- Docker + VSCode + Remote Containerで作る快適Jupyter Lab(Python)分析環境
- https://qiita.com/sho-hata/items/02ad47f67bce6816a69a
- VSCode Remote Containerが良い
- https://qiita.com/d0ne1s/items/d2649801c6f804019db7
- docker-compose.yml の内容を理解しよう（Dockerで作るコンテナの設定ファイル）
- https://futureys.tokyo/lets-understand-contents-of-docker-compose-yml/
- dockerfileの作り方
- https://kitsune.blog/dockerfile-summary
- Python, pipでrequirements.txtを使ってパッケージ一括インストール
- https://note.nkmk.me/python-pip-install-requirements/
- Linuxを体系的に勉強するまとめ（linuxがからんでくるので、都度確認する用）
- https://kitsune.blog/engineer/linux

# ゼロから作る流れ（Windows環境を想定・・・がどれでも同じような気がする）
- 1.最初に、【Git、Docker、VSCode】をダウンロードおよびインストールを行い、【Githubのアカウントを作る。】
```
VSCode内、拡張機能にて各種インストールする。タイルみたいなアイコンのやつ。
【Japanese Language Pack , Python , Remote Development , Docker】 （いらないものもありそうだけれども・・）
上記色々設定項目あるが、基本デフォルト設定で連打インストールで善いと思われる。
```
- 2.githubの【リポジトリ（保管場所）】から【ローカル環境へクローン（丸ごとコピー）】
- ※クローンする先は、指定なければユーザー配下になると思われる。
- 本リポジトリtest2のURL
```
https://github.com/Satou-Kazuki/test2.git
```
```
  クローンを作るにあたって、【git Bash：linux版コマンドプロンプトみたいなもの】からコマンドカチカチして行うパターンと
  VScode内機能から行うパターンがあるが、今回はVSCodeから行う。
  特に何もなしで適当にしていたら、gitのカレントディレクトリ、クローン保管場所等、ユーザーフォルダ配下になる。
```
- VSCodeの玉紐みたいなアイコンを押下すると、リポジトリをクローンというのがあるので、URL入れてクローンする。
```
  クローンしたtest2には、Dockerのコンテナファイルが入っているので、VScodeでのクローンが終わった段階で
  コンテナ作成の案内が来る。OKすると、イメージを元にコンテナが作成されていくのでしばし待つ。
  →今回使うイメージは【jupyter/datascience-notebook】で【DockerHub】に公開されているもの。
  【コンテナのイメージ】
  LinuxOSを元に、必要なアプリをインストールした仮想環境といった感じの物と思われる。
  今回使っているイメージのものでいえば、
  【OS:Linuxのubuntu-20.04】の環境に
  【anaconda, python:3.9.6 , JupyterLab ,各種ライブラリ】がインストールされているもの。
  上記マイクロOSのようなものがホストOS（ローカルのWINDOWS）上でゲストOSとして稼働しているようなイメージ。
```
- コンテナの作成及び実行が問題なく行われれば、VScodeとコンテナの相互が連携している状態になる。
```
  うまくいっていたら、【VSCode下部タスクバーみたいなところ】、【><】の横に【Dev Container:Jupyter Project】と表示される。
  【><】のアイコンからコンテナを停止させる等操作が行える。
  ※このタスクバーみたいなところに、現在利用してるインタプリタ等表示される。
  ※タスクバー内、【玉紐と↑↓】は【githubへpull,commit,push】するための物。
```
```
　コンテナ Linux環境下あるJupyterLabとpythonコンパイラへ　ローカルのVScodeからリモートでアクセスを行い、
  ローカルで作業している感覚で、リモート環境での開発が行える。
  VSCodeのpythonコンパイラの選択画面に何個かpythonのインタープリタが表示されていたら、コンテナとの連携がうまくいっている。
  表示されない場合、画面の内容に従ってインストールやらなんやらガチャガチャしていたらたぶん動くと思われる。
  【ローカルのインタプリタと仮想環境上のインタプリタ見分け方】
  【/opt/conda/bin/python】 とPython 3.9.6のインタプリタのディレクトリを表示しているが、このディレクトリ構造は
  【Linux　ubuntuのディレクトリ】になるので必然仮想環境へアクセスできていることがわかる。
```
- ここまでくればgithub　リポジトリからコードもらったり上げたり、チームでの開発が行えるようになっている・・・はず。

  
  

# 化学反応ネットワーク自動設計シミュレーションツール(PEN toolbox + PPsystem)

# 概要

PEN toolboxの三つの反応（活性化、自己触媒反応、阻害）に加えて捕食反応(Predator Prey=PP)も使用できる化学反応ネットワーク設計・シミュレーションシステムを実装した。
PEN toolboxは、任意の化学反応ネットワークを作るためのフレームワークである。
化学反応ネットワークは分子群ロボットのコントローラの設計に使われる。


# 開発背景

先行研究としてPENのみのシミュレーション(Aubert et al., 2014 )やPEN＋PPの常微分方程式構築（Aubert-Kato, Cazenille, 2020)があったが、PEN+PPの両方を使ってかつ、入力された化学反応ネットワークからの中間反応体の生成から、常微分方程式に基づいたシミュレーションまで全て自動化するツールは今まで実装されていなかった。

<img width="360" alt="スクリーンショット 2022-11-14 0 20 08" src="https://user-images.githubusercontent.com/93179388/201529358-c1b8e6e1-8688-47f3-8db3-ec66e280be98.png">

# 使い方
以下にあるように、OligaterとBistable Switchの入力は既に実装済みである。

(a)Oligatorの化学反応ネットワークに基づくシミュレーションをしたい場合

以下の332行〜337行までの各化学物質のパラメータ（名前、濃度、拡散定数、安定性）を適宜変更、Bistable Switchの場合は以下の383行〜388行を変更すればシミュレーションが可能だ。

(b)それ以外の化学ネットワークを使いたい場合。

自分でEdge(反応タイプ(PEN or PP)、入力、最終生成物）を設定する必要がある。


<img width="830" alt="スクリーンショット 2022-11-14 1 15 04" src="https://user-images.githubusercontent.com/93179388/201532163-28f3c9f0-f6f0-4678-b3b1-6c9816b54669.png">

<img width="738" alt="スクリーンショット 2022-11-14 1 22 23" src="https://user-images.githubusercontent.com/93179388/201532437-ef5cfa58-92fe-4599-96e0-3b00be781308.png">


# 実行環境
・Jupyter Notebook 6.4.11

・Python 3.10.4

# 目的

シミュレーションツールを開発している目的はWetな実験のデメリット(時間、費用）を補うためである。
このシミュレーションシステムのメリットとしてはユーザーが化学反応ネットワークを入力しただけで簡単に、二つの反応タイプ(PEN,PP)に応じた反応中間体の生成から、微分方程式に基づいたシミュレーションを自動で行うことができる。すべてのコードはPythonで作成した。
プログラミングの知識があまりなくてもPEN＋PPを使ったシミュレーションを行うことができる。

# 方法

PPシステムやPEN toolboxに基づく抽象的な化学反応ネットワークを入力として受け取り、自動的に常微分方程式に組み込み、中間反応体を含めた全ての反応を自動的にシミュレーションさせた。
<img width="423" alt="スクリーンショット 2022-11-14 0 22 38" src="https://user-images.githubusercontent.com/93179388/201529490-0b30c8cb-2082-4c3f-8230-9ab457ce4d6e.png">

# 検証

今回Oligater(Montagne et al., 2011)とBistable　Switch(Fauste-Gay et al., 2022)のモデルを化学反応ネットワークとして入力した。
実行結果は以下の通りだ。

・Oligater　→三つのPEN反応で構成
1つの分子(青)が自己触媒反応で濃度を増やして、もう１つの分子（オレンジ)を増やす。また、オレンジが抑制分子を増やして、青の触媒反応を抑制する。
参考文献と同じく、テンプレート分子の濃度により、安定性、減衰振動、振動を確認できた。

<img width="435" alt="スクリーンショット 2022-11-14 0 00 26" src="https://user-images.githubusercontent.com/93179388/201528408-24f08d9f-f266-4a41-84e7-ec7a9abb9782.png">


・Bistable Switch(双安定性スイッチ）→PEN+PP反応で構成
Nが自己触媒反応で濃度を増やすが、同時にP2が捕食して抑制分子のP1を増やす。
NとP2の初期濃度により、Nが二つの安定状態になる可能性を確認できた。
<img width="523" alt="Bistable" src="https://user-images.githubusercontent.com/93179388/201527889-b656225d-18f0-4e7a-963c-d90d3c071be7.png">

文責：お茶の水女子大学大学院　人間文化創成科学研究科理学専攻情報科学コース　吉田瑠華



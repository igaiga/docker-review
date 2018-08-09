# README

Re:VIEW 2.5 用を使うための Dockerfile。
イメージ名は「kauplan/review2.5」。


## 作成理由

Dockerイメージ「vvakame/review」だと、reviewstarter で生成した
プロジェクトがコンパイルできないことがある。

原因：

* インストールされているフォントが足りない (beramono 等)。
* インストールされているスタイルファイルが足りない (ulem 等)。
* LaTeX のバージョンが少し古いため、一部のマクロが動かない。

そのため、次のような変更を行った。

* フォントとスタイルファイルを追加でインストール。
* Ubuntu18.04を使うことで、LaTeX (TeXLive) のバージョンを更新。
* おまけ：combine_pdf gem を追加 (PDF にノンブルをつけるのに必要)。


## ベースイメージ

* https://github.com/vvakame/docker-review/blob/master/review-2.5/Dockerfile


## ベースイメージからの変更点

* use base image 'ubuntu:18.04' instead of 'debian:stretch-slim'
* remove maintainer label and add description label
* install 'texlive-fonts-extra' package (necessary for 'beramono.sty')
* install 'texlive-generic-recommended' package (necessary for 'ulem.sty')
* install Noto font from standard package, not backport package
* use 'gem install -N' instead of 'gem install --no-rdoc --no-ri'
* add 'gem install combine_pdf' (necessary for 'rake pdf:nombre')

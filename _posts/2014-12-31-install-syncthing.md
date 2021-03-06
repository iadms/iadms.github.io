---
layout: post
title: 서버에 syncthing 설치하고 gui 접속 가능하게 만들기 
---

dh8.kr:8080 

일반 리눅스서머에 syncthing build하여 설치하고 외부에서 syncthing gui 설치하도록 하는것을 기록 해보았다.

환경 우분투 12.04

## 1. 최신 패키지로 업데이트!

{% highlight bash %}
sudo apt-get update
{% endhighlight %}

## 2. 빌드를 위한 gcc 설치

{% highlight bash %}
sudo apt-get install curl git mercurial make binutils bison gcc
{% endhighlight %}

## 3. gvm 설치. 

gvm으로 golang 설치하는것이 우분투 내부에 있는 패키지는 버전이 낫다. 현재 syncthing은 go1.3부터 사용 가능하다.

{% highlight bash %}
bash < <(curl -s https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
{% endhighlight %}

## 4. gvm으로 go1.4설치

{% highlight bash %}
gvm install go1.4
gvm use go1.4 [--default]
gvm list
{% endhighlight %}

## 5. syncthing 저장소 가져오기. 

{% highlight bash %}
go version
mkdir -p ~/src/github.com/syncthing
cd ~/src/github.com/syncthing
git clone https://github.com/syncthing/syncthing
{% endhighlight %}

## 6. syncthing build

{% highlight bash %}
export GOPATH=~ 
cd syncthing
go run build.go
{% endhighlight %}

## 7. web gui 외부에서 접속 가능하도록 수정

syncthing config gui address 주소 바꾸기

{% highlight bash %}
vim /home/donghee/.config/syncthing/config.xml 
{% endhighlight %}


{% highlight xml %}
<gui enabled="true" tls="false">
  <!-- <address>127.0.0.1:8080</address> -->
  <address>0.0.0.0:8080</address>
  <apikey>PzZVg6slKF9MQ7n9-XGNwWI5e3ZWLffg</apikey>
</gui>
{% endhighlight %}

## 8. syncthing 실행

{% highlight bash %}
bin/syncthing
{% endhighlight %}

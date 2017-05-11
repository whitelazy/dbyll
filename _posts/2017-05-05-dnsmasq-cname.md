---
layout: post
title: Dnsmasq에 cname 설정하기
categories: [general, linux, server]
tags: [linux, server, dns, cname, dnsmasq]
description: 리눅스 dnsmasq에서 cname 추가
---

#Dnsmasq 에 cname 추가하기

nginx 로 reverse proxy 구성하려니까 cname 구성이 필요해져서 필요한 내용만 정리

* ubuntu 14.04 기준

## dnsmasq 설정파일

* /etc/dnsmasq.d/파일이름.conf 설정파일 추가

> address=/proxy.domain.com/xxx.xxx.xxx.xxx
> cname=a.domain.com,proxy.domain.com

## /etc/hosts 파일

> xxx.xxx.xxx.xxx  proxy.domain.com

## dnsmasq 재시작

## 확인

* nslookup a.domain.com

---
layout: single
title:  "JavaError 정리"
categories: Java
tags: 
  - [Error, Java]
toc: true
toc_sticky: true
---

## Tomcat Server Error - Port 8080 already in use

1. cmd창을 관리자 권한으로 열어 프로세스 id 찾기

   `netstat -ano | findstr 8080`

2. 프로세스 kill 하기

   `taskkill /F /pid (pid)`

참조사이트: [stackoverflow](https://stackoverflow.com/questions/34253779/tomcat-server-error-port-8080-already-in-use)

## The superclass "javax.servlet.http.HttpServlet" was not found on the Java Build Path

1. 프로젝트 우클릭 - Properties
2. Project Facets - Runtimes에 톰캣서버 체크
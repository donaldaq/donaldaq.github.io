---
layout: post
title: Tensorflow Installing Offline
excerpt: "Machine Learning"
categories: [Machine Learning]
comments: true
---

## Tensorflow 및 keras Offline 설치 순서

1. 먼저 Python 3.5.1을 설치한다.
2. 시스템 환경변수 추가한다. 
3. vc_redist.x64 파일도 설치한다. [링크]([https://www.microsoft.com/ko-kr/download/details.aspx?id=48145)
4. pip-19.0.3(폴더) 설치하여 pip 최신버전로 업그레이드 하여 사용 가능하도록 한다. [링크](https://pypi.org/project/pip/#files)  압축파일 다운받고 설치하면 된다.

### 오프라인 패키지(라이브러리) 설치 및 검색 사이트 

	- www.pypi.org 
	
### 설치 명령어 

	- 폴더(압축파일) 경우 : python setup.py install
	- whl파일 경우: pip install 파일명.whl


* 유의사항 *
  예) Pillow-5.4.1-cp35-cp35m-win_amd64.whl
     중간 부분: cp35-cp35m 은 파이썬 버전을 의미한다 파이썬 3.5버전을 설치했으므로 cp35가 설치되야 정상 동작한다. 
          **꼭 맞춰주어야 한다.** 
     마지막: win_amd64는 운영체제를 의미한다. 예) 운영체제: 윈도우 64비트

5. 패키지 순서: 패키지마다 **dependency**가 있기 때문에 순서를 지켜야 tensorflow까지 설치가 된다. 
   꼭 순서가 맞는 것은 아니지만 이 순서대로 하면 설치가 끊김없이 진행된다.

 - soupsieve-1.8-py2.py3-none-any.whl 
 - beautifulsoup4-4.7.0 폴더
 - google-2.0.1 폴더
 - pytz-2018.9-py2.py3-none-any.whl
 - six-1.12.0-py2.py3-none-any.whl  
 - protobuf-3.7.0-cp35-cp35m-win_amd64.whl
 - wheel-0.33.1-py2.py3-none-any.whl
 - astor-0.7.1-py2.py3-none-any.whl
 - grpcio-1.19.0-cp35-cp35m-win_amd64.whl
 - numpy-1.16.2-cp35-cp35m-win_amd64.whl
 - h5py-2.9.0-cp35-cp35m-win_amd64.whl
 - python_dateutil-2.8.0-py2.py3-none-any.whl
 - pandas-0.24.1-cp35-cp35m-win_amd64.whl
 - Markdown-3.0.1-py2.py3-none-any.whl
 - absl-py-0.7.0 폴더
 - gast-0.2.2 폴더
 - googlecloud-0.34.0 폴더
 - termcolor-1.1.0 폴더
 - setuptools-40.8.0
 - urllib3-1.24.1-py2.py3-none-any.whl
 - scipy-1.2.1-cp35-cp35m-win_amd64.whl
 - PyYAML-3.13-cp35-cp35m-win_amd64.whl
 - Django-2.1.7-py3-none-any.whl
 - image-1.5.27-py2.py3-none-any.whl
 - Keras_Applications-1.0.7-py2.py3-none-any.whl 
 - Keras_Preprocessing-1.0.9-py2.py3-none-any.whl
 - Keras-2.2.4-py2.py3-none-any.whl
 - Werkzeug-0.14.1-py2.py3-none-any.whl
 - tensorboard-1.12.0-py3-none-any.whl
 - tensorflow-1.12.0-cp35-cp35m-win_amd64.whl
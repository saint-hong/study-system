# 아나콘다를 사용한 가상환경 셋팅하기
- 개발 프로세스는 각각에 맞는 가상 환경을 만들고 필요한 패키지들의 버전관리를 하는 것이 안전하고 효율적이다. 따라서 가상환경을 만들고 필요한 패키지들을 설치하는 과정을 정리한다.
- 특히 jupyter notebook 설치할 때 딥러닝 프레임워크인 tensorflow의 버전문제를 방지하기 위한 설치 과정을 중점적으로 요약하였다. 

## 아나콘다 특징
- `파이썬 패키지 매니저 + 개발환경 매니저 기능이 들어 있음`
   - pip + venv의 기능
- venv는 python3에 포함되어 있는 가상환경 기능
- 콘다는 아나콘다의 툴
   - 아나콘다는 데이터 사이언스 용 패키지들이 들어있어서 용량이 큰 편
   - 간단하게 사용할 때는 miniconda를 사용해서 패키지 매니저 + 개발환경 매니저를 사용해도 됨
- 대부분의 개발은 가상환경에서 이루어진다.
   - 프로젝트 마다 사용하는 패키지의 버전이 다른 경우가 많기때문
- 우분투나 윈도우에서 아나콘다(또는 미니콘다)를 설치해서 사용
   - anaconda 또는 미니콘다 설치 스크립트 url 주소 복사 ===> wget <url 주소> ===> 다운로드 (.sh 파일) ===> 콘다가 설치될 디렉토리로 파일 이동 ===> 설치 (bash ./Miniconda~.sh) ===> 설치 완료 되면 conda list 로 설치 결과 확인

## 간단한 명령어
- 아나콘다 설치 후 버전 확인 : conda --version
- 명령어 도움말 : conda --help
   - 모든 명령어에 --help를 치고 검색해볼 수 있다.
- 가상환경 목록 : conda env list
- 가상환경 생성 : conda create -n <이름> python=3.10
   - 설치할 패키지를 추가 입력 해도 된다
- 가상환경 활성화 : conda activate dev_env
   - 가상환경 비활성화 : conda deactivate dev_env
- 가상환경 삭제 : conda env remove -n dev_env
   - 다른 가상환경을 활성화 한 후 지우려는 가상환경 이름을 입력하여 제거한다.
- 콘다 설치 목록 : conda list
   - 특정 패키지만 검색 : conda list -f python, conda list -f tensorflow
   - 정규표현식 사용 : " " 안에 정규표현식을 넣는다. (윈도우인 경우)
      - sci로 시작하는 문자열 검색 : conda list "^sci"
      - sci 또는 num 으로 시작하는 문자열 검색 : conda list "^(sci | num)"
   - 다른 가상환경의 패키지 검색 : conda list -n new_env "^ipy"
- 콘다 패키지 설치 : conda install python=3.10
- 콘다 패키지 삭제 : conda uninstall python
- 콘다 패키지 업데이트 (최신버전으로) : conda update python
- 명령줄 깨끗하게 : cls
- github 설치
   - sudo apt update ===> sudo apt install git ===> git --version 확인
   - git은 코드의 버전관리 시스템
   - tig 설치 : sudo apt install tig
      - it 커밋 히스토리를 터미널에서 보여주는 툴
      
## 개발용 가상환경 생성 및 패키지 설치
- 기본적으로 모든 패키지 설치는 conda로 하고, 예외적으로 pip를 사용한다.
   - conda 가 더 패키지 관리에 유용하다.
   - conda로 설치가 안되거나, 설치가 되어도 실행에서 이상한 경우가 있다. 이러한 경우 pip로 설치
- 새로운 가상 환경 생성 : {"name": "dev_env"}
   - `conda create -n dev_env python`
   - python, pip 등 기본 패키지 설치 됨
   - 버전을 지정하지 않으면 python은 3.12 최신 버전이 설치 됨
   - 해당 가상환경의 프로젝트 성격에 따라서 중심적으로 설치해야하는 것을 기준으로 설치한다.
   - 특수한+중요한 패키지의 버전에 맞춰서 범용성이 높은 패키지들을 설치한다. (scikit-learn, python 등은 어떤 버전이어도 사실상 사용하는데 문제가 없다.)

## 설치 순서
- 각 오픈소스별로 설치 매뉴얼에 conda나 pip별로 설치 명령어가 나와있다.
   - `conda create -n dev_env python=3.10`
   - `conda install nb_conda_kernels`
      - jupyter notebook과 관련 패키지들이 똑같이 설치된다.
      - conda install notebook, pip install notebook 명령어를 실행하면 "nb_conda_kernels"가 설치되지 않을 수 있다.
      - "nb_conda_kernels" 가 설치 되지 않으면 notebook 화면이 구형 버전으로 나온다.
   - `pip install jupyter_nbextensions_configurator` : 
      - jupyter notebook의 화면구성과 다양한 패치기능을 사용할 수 있도록 한다.
      - conda로 설치하는 것보다 pip로 설치하는 것이 좋다.
   - `conda install autopep8`
   - `conda install tensorflow` 
      - conda로 설치. python 버전, openssl 버전 변경 된다.
   - scikit-learn 설치 : `pip install scikit-learn`
   - matplotlib 설치 : `pip install matplotlib`
   - pandas 설치 : `pip install pandas`
   - statsmodels 설치 : `pip install statsmodels`
   - pgmpy 설치 : `pip install pgmpy`
   - autopep8 설치 : `pip install autopep8`

## 텐서플로우 설치 에러 정리
- 텐서 플로우 설치
   - conda install tensorflow
   - 텐서플로우 파이썬 버전 호환 : tensorflow -> python[version='3.10.*|3.9.*|3.8.*|3.7.*|3.6.*|3.5.*']
- 텐서플로우 재설치
   - conda install tensorflow 또는 pip install tensorflow
   - 다만 python 설치한 패키지 관리자와 같은 방법으로 설치해야 버전 충돌이 생기지 않는다.
   - keras, tensorboard 등 필요한 패키지들이 함께 설치된다.
   - python도 3.10 버전에서 호환되는 것으로 자동 다운그레이드 된다.
   - sicipy는 자동 설치 목록에 있는데, scikit-learn은 없음
- `python과 tensorflow 둘다 conda로 설치할 것`
   - conda로 python 설치하고 pip로 tensorflow 설치하면 버전이 일치가 안되는 것 같다.
   - conda install tensorflow 하면 버전 조정 메시지가 뜬다.
      - openssl   3.0.13-h2bbff1b_0 --> 1.1.1w-h2bbff1b_0
      - python    3.10.13-he1021f5_0 --> 3.10.13-h966fe2a_0
- jupyter notebook 과 충돌 남
   - jupyter notebook 을 먼저 설치하고 tensorflow를 설치하는게 좋다.


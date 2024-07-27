# 아나콘다를 사용한 가상환경 셋팅하기
- 개발 프로세스는 각각에 맞는 가상 환경을 만들고 필요한 패키지들의 버전관리를 하는 것이 안전하고 효율적이다. 따라서 가상환경을 만들고 필요한 패키지들을 설치하는 과정을 정리한다.
- 특히 jupyter notebook 설치할 때 딥러닝 프레임워크인 tensorflow의 버전문제를 방지하기 위한 설치 과정을 중점적으로 요약하였다. 

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


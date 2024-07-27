# jupyter notebook 초기 setting
- jupyter notebook을 완전하게 설치 후 원활하게 사용하기 위한 초기 세팅 정리
   - jupyter notebook의 설치 과정은 패키지 버전 관리와 함께 고려해야 하므로 따로 정리함.

## jupyter_nbextensions_configurator 설치
- pip install jupyter_nbextensions_configurator

## autopep8 설치
- pip install autopep8

## 스타트 파일 설정
- jupyter notebook이 시작 될때 실행되는 여러가지 프로세스들을 세팅할 수 있는 파일
   - 사용자 ---> 사용자이름 폴더 ---> .ipython ---> profile_default ---> startup
   - 00.py 파일 생성 (ipython 실행시 00 번으로 실행되는 py 파일)
   - 자주 사용하는 패키지 임포트 등 기본 셋팅

### 경고 무시 설정

```
import warnings
warnings.simplefilter('ignore')
```

### 자주 사용하는 패키지를 임포트

```
import matplotlib as mpl
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
import seaborn as sns
import numpy as np
import scipy as sp
import pandas as pd
import statsmodels.api as sm
import sklearn as sk
```
### matplotlib 설정
- ipython 콘솔에 직접 환경 설정 : ipython_config 파일
- 사용자 ---> 사용자이름 폴더 ---> .ipython ---> profile_default ---> ipython_config
   - 해당 라인에 mpl.rc 계열의 설정을 입력한다.
```
mpl.use('Agg')
```

### seaborn 설정

```
sns.set()
sns.set_style("whitegrid")
sns.set_color_codes()
```

### 주피터 노트북 한글 폰트 설정
- lines of code to run at IPython startup.
- 한글 폰트를 설정하기 위해서 rc 설정의 family 인수에 폰트 이름을 입력한다.
- matplotlib의 figure의 dpi 설정
   - 이 값을 100보다 크게 하면 plot 출력시 figure가 크게 확대되어서 출력된다.

```
c = get_config()
c.InteractiveShellApp.exec_lines = [
    "mpl.rc('font', family='Malgun Gothic')",  #  맑은고딕 폰트 사용
    #"mpl.rc('font', family='NanumGothic')"   # 나눔고딕 폰트 사용
    "mpl.rc('axes', unicode_minus=False)", # 유니코드 음수 기호 사용
    "mpl.rc('figure', figsize=(6, 4))",  # 그림 크기 (단위: 인치)
    "mpl.rc('figure', dpi=100)",  # 그림 해상도
]
```


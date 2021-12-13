# KpfSBERT HDBSCAN Clustering

## 모델 소개

### KpfSBERT HDBSCAN Clustering

뉴스기사의 주제별 클러스터링 테스크에서 좋은 성능을 보여주는 Sentence BERT의 한국언론진흥재단 버전인 kpfSBERT를 활용하여 클러스터링 테스크에서 높은 성능을 기록한 HDBSCAN을 이용해서 클러스터링하는 과정을 보여주는 예제이다.
여기서는 간단하게 하루분량의 뉴스기사(1만2천개)의 제목을 가지고 각 카테고리별로 클러스터링 하는 예제를 보여준다.
한국언론진흥재단에서 구축한 방대한 뉴스기사 코퍼스로 학습한 kpfBERT를 이용하여 특히 뉴스기사에 특화된 모델이다.

- 본 예제에 사용된 kpf-SBERT는 [kpfSBERT](https://github.com/KPFBERT/kpfbert)에 제작방법이 공개되어 있다.

- 뉴스 데이터 셈플은 한국언론진흥재단에서 제공하는 서비스인 [뉴스트러스트](http://newstrust.kr/)에서 가공하여 사용하였다.


### HDBSCAN을 이용한 클러스터링 관련 코드

- 코드 : https://hdbscan.readthedocs.io/en/latest/index.html

- 참고 : https://towardsdatascience.com/topic-modeling-with-bert-779f7db187e6


## 실행하기 위한 환경

1. 라이브러리

    ```
    python = 3.7
    PyTorch >= 1.6.0
    transformers >= 4.6.0
    sentence_transformers == 2.1.0
    
    ```
    
2. GPU

    ```
    NVIDIA - 2080 SUPER (8G) 환경에서 작성되었음
    ```

## Usage

1. 데이터 Preprocessing

   `./data/` 디렉토리에 데이터 화일이 위치한다.

   - `data/newstrust_20210601_samlple.json`: 하루분량의 11개 카테고리 1만2천개 뉴스기사의 제목 데이터.

   
2. Clustering  

    kpfSBERT의 문장embedding을 Umap으로 차원축소 후 HDBSCAN으로 클러스터링.
    hdbscan_process의 파라미터 중
    - `umap=False` umap 차원축소 실행여부. 기본은 True
    - `n_components=15` umap 차원축소 할 목표 차원. 기본은 5
    - `method='leaf'` HDBSCAN의 클러스터 방법. 기본은 'eom'
    - `min_cluster_size=5` HDBSCAN시 기본적으로 지정해주어야 하는 설정 파라미터. HDBSCAN 문서 참조
    - `min_samples=5` HDBSCAN시 추가적으로 지정하는 설정 파라미터. HDBSCAN 문서 참조
    
3. Topic

    부가적으로 클러스터링 된 묶음별 주제어를 추출하여 확인하는 코드 추가

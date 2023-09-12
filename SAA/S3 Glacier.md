
>[!info] 자주 사용되지 않는 데이터, 즉 '콜드 데이터'에 최적화된 스토리지 서비스

- [[S3]]와 비교해서 보면 좋다. 아카이브 백업을 위한 스토리지
- Glacier는 [[S3]]에 비해 비용이 저렴한데, 단순 가격만 보면 약 1/3 정도 (서울 리전 기준)
- 안정성과 가격 면에서는 [[S3]]에 비해 훨씬 장점으로 다가온다.
- 마음대로 검색이 불가능 (데이터 사용보다 저장에 목적)
- 마음대로 삭제가 불가능 (저장 기간을 기본적으로 몇 달~몇 년 단위로 생각, 3개월 이전에 조기 삭제하는 경우 비용 청구)
- 데이터 업로드 및 검색에 따로 UI 제공 X, 업로드는 무조건 API로만!

>[!note]
>백업을 위해 존재하는 스토리지
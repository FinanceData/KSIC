# Introductions
KSIC (Korea Standard Industry Code) dataset and using in Python.

# KSIC 한국표준산업분류 데이터셋
KSIC (Korea Standard Industry Code), 한국표준산업분류

생산단위(사업체단위, 기업체단위 등)가 주로 수행하는 산업 활동을 그 유사성에 따라 체계적으로 유형화한 표준 코드이다. 코드는 대분류(알파벳 1자리), 중분류(2자리), 소분류(3자리), 세분류(4자리), 세세분류(5자리) 종류가 있다. 금융감독원 전자공시(DART)에서 회사(종목)의 산업분류에 소분류(3자리)를 사용하고 있다.

통계청 한국표준산업분류코드(KSIC)
* http://kssc.kostat.go.kr/ksscNew_web/link.do?gubun=001#

코드의 내용과 항목을 상세하게 보려면,
* http://kssc.kostat.go.kr/ksscNew_web/kssc/common/ClassificationContent.do?gubun=1&strCategoryNameCode=001

(2018년 9월 현재) 9차 개정안이 주로 사용되고 있다(전자공시 등)
* KSIC 9차 개정(2008년) - 항목수 1,931개
* KSIC 10차 개정(2017년) - 항목수 2,000개

## Dataset
KSIC 9차 https://github.com/FinanceData/KSIC/raw/master/KSIC_09.csv.gz
* 1,931 rows
* 2 columns

KSIC 10차 https://github.com/FinanceData/KSIC/raw/master/KSIC_10.csv.gz
* 2,000 rows
* 2 columns


## Usage

```python
import pandas as pd

url = 'https://github.com/FinanceData/KSIC/raw/master/KSIC_09.csv.gz'

df_ksic = pd.read_csv(url, dtype='str')
df_ksic.head(10)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Industy_code</th>
      <th>Industy_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01</td>
      <td>농업</td>
    </tr>
    <tr>
      <th>1</th>
      <td>011</td>
      <td>작물 재배업</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0111</td>
      <td>곡물 및 기타 식량작물 재배업</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01110</td>
      <td>곡물 및 기타 식량작물 재배업</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0112</td>
      <td>채소, 화훼작물 및 종묘 재배업</td>
    </tr>
    <tr>
      <th>5</th>
      <td>01121</td>
      <td>채소작물 재배업</td>
    </tr>
    <tr>
      <th>6</th>
      <td>01122</td>
      <td>화훼작물 재배업</td>
    </tr>
    <tr>
      <th>7</th>
      <td>01123</td>
      <td>종자 및 묘목 생산업</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0113</td>
      <td>과실, 음료용 및 향신용 작물 재배업</td>
    </tr>
    <tr>
      <th>9</th>
      <td>01131</td>
      <td>과실작물 재배업</td>
    </tr>
    <tr>
      <th>10</th>
      <td>01132</td>
      <td>음료용 및 향신용 작물 재배업</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0114</td>
      <td>기타 작물 재배업</td>
    </tr>
    <tr>
      <th>12</th>
      <td>01140</td>
      <td>기타 작물 재배업</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0115</td>
      <td>시설작물 재배업</td>
    </tr>
    <tr>
      <th>14</th>
      <td>01151</td>
      <td>콩나물 재배업</td>
    </tr>
    <tr>
      <th>15</th>
      <td>01152</td>
      <td>채소, 화훼 및 과실작물 시설 재배업</td>
    </tr>
    <tr>
      <th>16</th>
      <td>01159</td>
      <td>기타 시설작물 재배업</td>
    </tr>
    <tr>
      <th>17</th>
      <td>012</td>
      <td>축산업</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0121</td>
      <td>소 사육업</td>
    </tr>
    <tr>
      <th>19</th>
      <td>01211</td>
      <td>젖소 사육업</td>
    </tr>
  </tbody>
</table>


### 코드 패딩
중분류(2자리)~세세분류까지(5자리) 코드인데 뒤쪽에 0으로 채워서 사용하는 경우가 더 편리한 경우가 있다. 다음과 같이 pad 하여 사용할 수 있다.

```python
df_ksic['Industy_code'] = df_ksic['Industy_code'].str.pad(width=5, side='right', fillchar='0')
df_ksic.head(10)
```
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Industy_code</th>
      <th>Industy_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01000</td>
      <td>농업</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01100</td>
      <td>작물 재배업</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01110</td>
      <td>곡물 및 기타 식량작물 재배업</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01110</td>
      <td>곡물 및 기타 식량작물 재배업</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01120</td>
      <td>채소, 화훼작물 및 종묘 재배업</td>
    </tr>
    <tr>
      <th>5</th>
      <td>01121</td>
      <td>채소작물 재배업</td>
    </tr>
    <tr>
      <th>6</th>
      <td>01122</td>
      <td>화훼작물 재배업</td>
    </tr>
    <tr>
      <th>7</th>
      <td>01123</td>
      <td>종자 및 묘목 생산업</td>
    </tr>
    <tr>
      <th>8</th>
      <td>01130</td>
      <td>과실, 음료용 및 향신용 작물 재배업</td>
    </tr>
    <tr>
      <th>9</th>
      <td>01131</td>
      <td>과실작물 재배업</td>
    </tr>
  </tbody>
</table>


##### 2018 FinanceData.KR

## 언어설정 방법 

```
C:\Program Files (x86)\gnucash\etc\gnucash\environment
```

```
LANG=ko_KR
LANGUAGE=en
```



## 활용 방법

1. **백엔드 관리 방법**  

   설치하고 나서 새로운 장부를 생성하고 Mariadb로 관리할 수 있다.  MySQL로 연동후 MariaDB로 관리하면 된다.

   향후에 book_yr, book_gr, book_mo, portfolio_ko, portfolio_us를 연동하기 위해서 guid가 일치되는 것이 좋다. 하지만 내용 자체로 Hash를 만드는 것이 아니라 그냥 그때 그때 무작위로 만들기 때문에 (Boost라이브러리) CSV로 연동하면 안된다. 거래내역 연동을 시킬 때는 GNUCash 자체의 Export기능보다는 직접 SQL로 해주는 것이 좋다. 

2. **Online Quote 설정 방법**
   
   (1) Pearl 설치 
   
   (2) Finance::Quote tar파일을 받아오고 압축해제한 후에 관리자권한 파워쉘에서 Makefile을 실행한다.
   (3) https://www.alphavantage.co/ 에서 API키를 받아온다. 
   
   (4) 시스템 환경 변수에서 ALPHAVANTAGE_API_KEY의 값을 해당 API키 값으로 생성한 다.
   (5) C\Program (x86)\gnucash\bin으로 cd하고 install-fq-mods.cmd를 관리자권한 파워쉘로 실행한다.
   (6) 미국주식의 경우, alphavantage, 그냥 그 코드를 입력하고, (7) 국내 주식의 경우, Yahoo finance, {코드}.KS 형태로 입력한다.
   
3. **유가증권관련**
   
   **유가증권 목록 관리**
   
    메뉴바에서 Tools의 Security Editor를 통해 할 수 있다. Namesapce는 변경 가능하니 KOSPI 등으로 설정해서 쓰면 된다. 이 목록은 MariaDB의 commodities 테이블에서 관리되며, price 테이블에 Online Quotes의 결과가 저장된다. (원데이터는 JSON형태이고 자동으로 관리되어 RDBMS에 저장된다)
   
   **임시생성항목**
   
   가격이 업데이트 될 때 이 것은 현금이 아닌데 현금으로 측정한 것이기 때문에 현금표시된 값을 일종의 부채라고 간주하는 것 같다. 따라서 추가된 값을 커버하기 위해 자동으로 -내역이 만들어진다. 이 계정은 Hidden으로 설정해놓고 보이지 않게 할 수 있다. 결산할 때 혹은 분기나 월별로 유가증권평가이익에으로 인식하거나 향후 매도시에 유가증권처분이익 등으로 인식하여 처리하면 된다.  
   
   **유가증권거래내역입력방법**
   
   e.g. 두산중공업 (주당19850원)을 50주 매수한다면 <이체>를 해당 증권계좌로 설정하고 <구매 계좌수>를 50, 그리고 <가격>을 현재가 19850원으로 입력한 후에 엔터를 클릭한다.
   e.g. 두산중공업 (주당19850원)을 50주 매도한다면 <이체>를 해당 증권계좌로 설정하고 <구매 계좌수>를 -50, 그리고 <가격>을 현재가 19850원으로 입력한 후에 엔터를 클릭한다. 
   
   

## 버전관련

가능하면 2.6.21을 쓰는 것이 호환성이 좋은 것 같다. 소스포지에서 받으면 된다. 

**SHA256 Hashes:**

- 2c3bed2a9366ac0def3e1abf39e148b2850f5ef34c99d0497acd2643db4ffa58  gnucash-2.6.21.tar.bz2
- c6d78471253f06e701198ac27a613d08e2d74ead7f723ab98f5988b3ffc591df  gnucash-2.6.21.tar.gz
- 159bdd06b11535c569c6fccb0a44c5052e428ea64ea365118675431b2836ed06  gnucash-2.6.21-setup.exe
- 9cd8334dfe75026121ade36740fb6a2c30ce0dc0d59e0f35d360667fd3b1e8fa  Gnucash-Intel-2.6.21-3.dmg
- 137fd4692a116de88300fcb1e8694ff52d80f4e199103c461725ec1ebb349d56  Gnucash-PPC-2.6.21-1.dmg
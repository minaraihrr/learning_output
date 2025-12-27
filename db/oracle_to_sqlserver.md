# Oracle → SQL Server SQL修正覚え書き  
ユーザー作成の Oracle + Access アプリを SQL Server に移行する案件で、アプリ内のSQLを書き換えたときの覚え書き
## SQL修正箇所一覧  
| No. | Oracle | SQL Server | 備考 |
|-----|-----|-----|-----|
| 1 | SYSDATE | GETDATE() | |
| 2 | NVL | ISNULL | |
| 3 | DECODE | CASE | |
| 4 | TO_DATE('20251225', 'YYYY-MM-DD') | CAST('20251225' AS DATE) | |
| 5 | TO_CHAR('1', '0000') | FORMAT('1', '0000') | |
| 6 | RPAD / LPAD | LEFT / RIGHT | まれに空白埋めに使用 |
| 7 | TRUNC(数値) | ROUND | |
| 8 | TRUNC(日付) | FORMAT | |
| 9 | ADD_MONTHS | DATEADD | |
| 10 | LAST_DAY | EOMONTH | |
| 11 | NEXTVAL | NEXT VALUE | |
| 12 | A \|\| B | CONCAT(A, B) | A + B は片方にNULLを含む場合<br> NULLになるため避ける |
| 13 | (+) 外部結合 | LEFT JOIN | |
| 14 | , 内部結合 | INNER JOIN | |
| 15 | UPDATE テーブル名 別名 | UPDATE 別名 FROM テーブル名 別名 | |
| 16 | UPDATE (A,  B) = (SELECT ...) | UPDATE A = (SELECT ...), B = (SELECT ...) | 単純な場合はFROM句にJOIN |
| 17 | DELETE FROM テーブル名 別名 | DELETE 別名 FROM テーブル名 別名 | |
| 18 | ORDER BY A | ORDER BY <br> CASE WHEN A IS NOT NULL THEN 0 <br> ELSE 1 <br> END, A | NULLを含むORDER BY の仕様差への対応。<br> 普通にORDER BY した場合 <br> Oracle → NULLが最下位 <br> SQL Server → NULLが最上位  |

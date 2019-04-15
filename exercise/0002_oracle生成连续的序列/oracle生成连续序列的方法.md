# oracle生成连续序列的方法
方法一： 利用 connect by 关键字生成连续的序列。 
demo:根据当前年份，生成当前年份的前五年，后五年的年份列表
	SELECT extract(YEAR FROM SYSDATE)-5 + ROWNUM ID,
	extract(YEAR FROM SYSDATE) + 5 + ROWNUM TEXT
	FROM DUAL CONNECT BY ROWNUM <= 9;

利用序列快速填充一个表格多少行的主键：
	INSERT TEST_TABLE(TID) SELECT TEST_SEQ.NEXTVAL FROM DUAL CONNECT BY ROWNUM < 1000;



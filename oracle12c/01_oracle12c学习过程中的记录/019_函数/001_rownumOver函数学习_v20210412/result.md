# 测试oracle的 row_number over() 函数的使用



## 1.  测试数据

![alt](D:\04github\tramplpf\oracle\oracle12c\01_oracle12c学习过程中的记录\019_函数\001_rownumOver函数学习_v20210412\01_测试的数据集.png)





## 2. 通过order by 语句根据工资 salary 进行降序排列

SELECT * FROM L_ROW_NUMBER_OVER T ORDER BY T.SALARY DESC 

![alt](D:\04github\tramplpf\oracle\oracle12c\01_oracle12c学习过程中的记录\019_函数\001_rownumOver函数学习_v20210412\02_利用orderBy语句将salary进行降序排列.png)



## 3. 将所有数据看成一组，然后进行排序 

SELECT T.USER_TYPE, T.NAME, T.AGE, T.SALARY, ROW_NUMBER() OVER( ORDER BY SALARY DESC) RN 
FROM L_ROW_NUMBER_OVER T;



![alt](D:\04github\tramplpf\oracle\oracle12c\01_oracle12c学习过程中的记录\019_函数\001_rownumOver函数学习_v20210412\03_将所有数据分为一组数据然后按照salary降序排列.png)



## 根据userType分组然后进行排序

SELECT T.USER_TYPE, T.NAME, T.AGE, T.SALARY, ROW_NUMBER( ) OVER (partition by t.user_type order by T.SALARY DESC) RN FROM L_ROW_NUMBER_OVER T ; 

![alt](D:\04github\tramplpf\oracle\oracle12c\01_oracle12c学习过程中的记录\019_函数\001_rownumOver函数学习_v20210412\04_将数据按照userType排分组后对每一组数据进行排序.png)



## 测试row_number over 的排序的时机 

SELECT  T.NAME, T.AGE, T.SALARY, ROW_NUMBER() OVER( ORDER BY T.SALARY DESC)  RANK FROM L_ROW_NUMBER_OVER T WHERE T.AGE >= 13 AND T.AGE <= 16 ;



![alt](D:\04github\tramplpf\oracle\oracle12c\01_oracle12c学习过程中的记录\019_函数\001_rownumOver函数学习_v20210412\05_测试row_numerbOvery中排序的执行顺序和where条件的过滤条件的执行先后顺序.png)



这里查询出来的结果rank的取值是从1到4， 说明，row_number over 中的排序的顺序是在 where 条件执行完之后进行排序的。 





注意： 在使用over 等窗口函数的时候，over 里面的分组以及排序的执行晚于 where， group by， order by 的执行。 





create by lpf at 2021年4月12日17:57:14






















































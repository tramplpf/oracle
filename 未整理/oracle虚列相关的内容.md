# oracle序列相关的内容



## 相关的术语
oracle序列中CURRVAL 和NEXTVAL 专业术语叫做 虚列(pseudocolumn)



create table PDB_INFO 
(
   TID                  NUMBER(18)           not null,
   PDB_SERVICE_NAME     VARCHAR2(56),
   PDB_NAME             VARCHAR2(56),
   PDB_ADMIN_USER       VARCHAR2(56),
   PDB_ADMIN_USER_PASSWD VARCHAR2(32),
   CREATE_USER          VARCHAR2(32),
   LAST_UPDATE          DATE,
   constraint PK_PDB_INFO primary key (TID)
);


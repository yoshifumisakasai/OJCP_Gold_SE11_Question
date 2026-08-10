設問41

JDBCを利用してデータベースに接続するためのURLとして、正しいものを選べ（１つ）



A. jdbc:postgresql://localhost:5432/test


B. http://localhost.postgresql.com::5432/test


C. http://localhost.postgresql.jdbc:5432/test


D. jdbc.postgresql.com://localhost:5432/test



#JDBC URL の基本形式

`jdbc:<サブプロトコル>:<サブネーム>`

〇PostgreSQL の場合：  
`jdbc:postgresql://<host>:<port>/<database>`  

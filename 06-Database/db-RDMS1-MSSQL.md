



     <Resource name="jdbc/ds_sqlserver"
         auth="Container"
         type="javax.sql.DataSource"
         driverClassName="net.sourceforge.jtds.jdbc.Driver" 
         url="jdbc:jtds:sqlserver://localhost:1433;DatabaseName=abab;"
         username="tests"
         password="tests"
         maxActive="20"
         maxIdle="3"
         maxWait="12000"
         validationQuery="select 1 "
         removeAbandoned="true"
         removeAbandonedTimeout="60"
         testOnBorrow="true"
         logAbandoned="true" />
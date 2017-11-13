
import org.slf4j.Logger; 
private static final Logger LOG = LoggerFactory.getLogger(Test.class);   


### jdbc直连mysql ###
 public static void testJdbc2MySQL() throws Exception {
  Class.forName("com.mysql.jdbc.Driver");
  String url="jdbc:mysql://192.168.222.133:3306/test?user=tests&password=tests";
  Connection conn = DriverManager.getConnection(url);
  Statement stmt = conn.createStatement();
  String query = "select current_date as fa, current_timestamp as fb "; //"select * from test";
  ResultSet rs=stmt.executeQuery(query);
  while(rs.next()) System.err.println("@@@ "+rs.getString(1)+" ### "+rs.getString(2));
  rs.close();
  stmt.close();
  conn.close();
 }


### jdbc[odbc]直连sqlexpress ###
http://blog.csdn.net/zhouhuan965/article/details/6258087
 public static void testOdbc2SQLEXPRESS() throws Exception {
  Class.forName("sun.jdbc.odbc.JdbcOdbcDriver");
  String url = "jdbc:odbc:myDSN";
  //Class.forName("net.sourceforge.jtds.jdbc.Driver");
  //String url="jdbc:jtds:sqlserver://localhost:1433/abab;tds=8.0;lastupdatecount=true;integratedSecurity=true;";
  Connection conn = DriverManager.getConnection(url); //(url, null, null)
  Statement stmt = conn.createStatement();
  String query = "select user, GETDATE(), SUSER_SID() ";
  ResultSet rs=stmt.executeQuery(query);
  while(rs.next()) System.err.println("@@@ "+rs.getString(1)+" ### "+rs.getString(2));
  rs.close();
  stmt.close();
  conn.close();
 }


### jdbc[jtds]直连sqlexpress ###
 //先将jtds-1.3.1-dist.zip\x86\SSO\ntlmauth.dll放入jdk目录jre/bin/下
 public static void testJdbc2SQLEXPRESS() throws Exception {
  Class.forName("net.sourceforge.jtds.jdbc.Driver");
  String url="jdbc:jtds:sqlserver://localhost:1433/abab;integratedSecurity=true;";
  String url="jdbc:jtds:sqlserver://localhost:1433/abab;tds=8.0; lastupdatecount=true;integratedSecurity=true;";
  
  Connection conn = DriverManager.getConnection(url); //(url, null, null)
  Statement stmt = conn.createStatement();
  String query = "select GETDATE(), SUSER_SID() ";
  ResultSet rs=stmt.executeQuery(query);
  while(rs.next()) System.err.println("@@@ "+rs.getString(1)+" ### "+rs.getString(2));
  rs.close();
  stmt.close();
  conn.close();
 }

  String driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver"; 
  String url = "jdbc:sqlserver://localhost:1433; DatabaseName=sample";
  String usr = "sa";
  String pwd = "123456";
  Connection conn;
  try {
   Class.forName(driver);
   conn = DriverManager.getConnection(url, usr, pwd);
   System.out.println("Connection Successful!");
   conn.close();
  } catch (Exception ex) {
   ex.printStackTrace();
  }
  

  jdbc:jtds:sqlserver://localhost:1433/dbname;user=username;password=s3cr3t

  String url = "jdbc:sqlserver://127.0.0.1:1368;databaseName=mydb;user=sa;password=qiaoning";// sa身份连接
  String url2 = "jdbc:sqlserver://127.0.0.1:1368;databaseName=mydb;integratedSecurity=true;";// windows集成模式连接
  String driver = "com.microsoft.sqlserver.jdbc.SQLServerDriver";
  // String url ="jdbc:sqlserver://192.168.0.74;databaseName=wakeup";
  String sDBUrl = "jdbc:sqlserver://192.168.2.28\\JONSE;databaseName=wakeup";
  Class.forName(driver);
  conn = DriverManager.getConnection(sDBUrl, usr, pwd);
  conn.close();
  String driver = "net.sourceforge.jtds.jdbc.Driver";
  String url = "jdbc:jtds:sqlserver://BHX:1433/Forecast;instance=SQLEPXRESS";
  java.sql.Connection con = DriverManager.getConnection(url);
  conn.close();
 
  Class.forName("net.sourceforge.jtds.jdbc.Driver");
  String url="jdbc:jtds:sqlserver://localhost:1433/abab;tds=8.0;lastupdatecount=true;integratedSecurity=true;";
  Connection conn = DriverManager.getConnection(url); //(url, null, null)
  Statement stmt = conn.createStatement();
  String query = "select GETDATE(), SUSER_SID() ";
  ResultSet rs=stmt.executeQuery(query);
  while(rs.next()) System.err.println("@@@ "+rs.getString(1)+" ### "+rs.getString(2));
  rs.close();
  stmt.close();
  conn.close();


@After  
public void tearDown() {  
    jdbcTemplate.execute("DROP FUNCTION FUNCTION_TEST");  
    jdbcTemplate.execute("DROP PROCEDURE PROCEDURE_TEST");  
    String dropTableSql = "drop table test";  
    jdbcTemplate.execute(dropTableSql);  
}  
@Test  
public void testCallableStatementCreator1() {  
    final String callFunctionSql = "{call FUNCTION_TEST(?)}";  
    List<SqlParameter> params = new ArrayList<SqlParameter>();  
    params.add(new SqlParameter(Types.VARCHAR));  
    params.add(new SqlReturnResultSet("result",  
       new ResultSetExtractor<Integer>() {  
           @Override  
           public Integer extractData(ResultSet rs) throws SQLException,  
               DataAccessException {  
               while(rs.next()) {  
                   return rs.getInt(1);  
               }  
              return 0;  
       }));  
    Map<String, Object> outValues = jdbcTemplate.call(  
       new CallableStatementCreator() {  
            @Override  
            public CallableStatement createCallableStatement(Connection conn) throws SQLException {  
              CallableStatement cstmt = conn.prepareCall(callFunctionSql);  
              cstmt.setString(1, "test");  
              return cstmt;  
    }}, params);  
    Assert.assertEquals(4, outValues.get("result"));  
}  
@Test  
public void testCallableStatementCreator2() {  
    JdbcTemplate mysqlJdbcTemplate = new JdbcTemplate(getMysqlDataSource);  
    //2.创建自定义函数  
String createFunctionSql =  
    "CREATE FUNCTION FUNCTION_TEST(str VARCHAR(100)) " +  
     "returns INT return LENGTH(str)";  
String dropFunctionSql = "DROP FUNCTION IF EXISTS FUNCTION_TEST";  
mysqlJdbcTemplate.update(dropFunctionSql);         
mysqlJdbcTemplate.update(createFunctionSql);  
//3.准备sql,mysql支持{?= call …}  
final String callFunctionSql = "{?= call FUNCTION_TEST(?)}";  
//4.定义参数  
List<SqlParameter> params = new ArrayList<SqlParameter>();  
params.add(new SqlOutParameter("result", Types.INTEGER));  
params.add(new SqlParameter("str", Types.VARCHAR));  
Map<String, Object> outValues = mysqlJdbcTemplate.call(  
new CallableStatementCreator() {  
    @Override  
    public CallableStatement createCallableStatement(Connection conn) throws SQLException {  
      CallableStatement cstmt = conn.prepareCall(callFunctionSql);  
      cstmt.registerOutParameter(1, Types.INTEGER);  
      cstmt.setString(2, "test");  
        return cstmt;  
    }}, params);  
   Assert.assertEquals(4, outValues.get("result"));  
}  
public DataSource getMysqlDataSource() {  
    String url = "jdbc:mysql://localhost:3306/test";  
    DriverManagerDataSource dataSource =  
        new DriverManagerDataSource(url, "root", "");
     dataSource.setDriverClassName("com.mysql.jdbc.Driver");  
    return dataSource;  
}  
   
@Test  
public void testCallableStatementCreator3() {  
    final String callProcedureSql = "{call PROCEDURE_TEST(?, ?)}";  
    List<SqlParameter> params = new ArrayList<SqlParameter>();  
    params.add(new SqlInOutParameter("inOutName", Types.VARCHAR));  
    params.add(new SqlOutParameter("outId", Types.INTEGER));  
    Map<String, Object> outValues = jdbcTemplate.call(  
      new CallableStatementCreator() {  
        @Override  
        public CallableStatement createCallableStatement(Connection conn) throws SQLException {  
          CallableStatement cstmt = conn.prepareCall(callProcedureSql);  
          cstmt.registerOutParameter(1, Types.VARCHAR);  
          cstmt.registerOutParameter(2, Types.INTEGER);  
          cstmt.setString(1, "test");  
          return cstmt;  
    }}, params);  
    Assert.assertEquals("Hello,test", outValues.get("inOutName"));  
    Assert.assertEquals(0, outValues.get("outId"));  
}  
   
@Test  
public void testResultSet2() {  
  jdbcTemplate.update("insert into test(name) values('name5')");  
  String listSql = "select * from test";  
  final List result = new ArrayList();  
  jdbcTemplate.query(listSql, new RowCallbackHandler() {  
      @Override  
      public void processRow(ResultSet rs) throws SQLException {  
          Map row = new HashMap();  
          row.put(rs.getInt("id"), rs.getString("name"));  
          result.add(row);  
  }});  
  Assert.assertEquals(1, result.size());  
  jdbcTemplate.update("delete from test where name='name5'");  
}  


@Test  
public void testPpreparedStatement1() {  
  int count = jdbcTemplate.execute(new PreparedStatementCreator() {  
     @Override  
     public PreparedStatement createPreparedStatement(Connection conn)  
         throws SQLException {  
         return conn.prepareStatement("select count(*) from test");  
     }}, new PreparedStatementCallback<Integer>() {  
     @Override  
     public Integer doInPreparedStatement(PreparedStatement pstmt)  
         throws SQLException, DataAccessException {  
         pstmt.execute();  
         ResultSet rs = pstmt.getResultSet();  
         rs.next();  
         return rs.getInt(1);  
      }});      
   Assert.assertEquals(0, count);  
}  
      
@Test  
public void testPreparedStatement2() {  
  String insertSql = "insert into test(name) values (?)";  
  int count = jdbcTemplate.update(insertSql, new PreparedStatementSetter() {  
      @Override  
      public void setValues(PreparedStatement pstmt) throws SQLException {  
          pstmt.setObject(1, "name4");  
  }});  
  Assert.assertEquals(1, count);      
  String deleteSql = "delete from test where name=?";  
  count = jdbcTemplate.update(deleteSql, new Object[] {"name4"});  
  Assert.assertEquals(1, count);  
}  
 

/javax.naming.Context initContext = new javax.naming.InitialContext();
//Context ctx = (Context)initContext.lookup("java:/comp/env");
//DataSource ds = (DataSource)ctx.lookup("jdbc/mysql");
String inf = "{X}";
String sql = " select count(1) as cnt from information_schema.tables where table_name=upper('tx1') ";
//javax.sql.DataSource ds = (javax.sql.DataSource)(new javax.naming.InitialContext().lookup("java:/comp/env/jdbc/ds_sqlite"));
javax.naming.Context ctx = new javax.naming.InitialContext();
javax.sql.DataSource ds = (javax.sql.DataSource)ctx.lookup("java:/comp/env/jdbc/ds_hsql");
java.sql.Connection conn = ds.getConnection();
conn.setAutoCommit(false);
java.sql.Statement stmt = conn.createStatement();
java.sql.ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) inf = rs.getString(1);
rs.close();
if (inf.equals("0")) {
   sql = " create table tx1 (kid integer not null primary key identity, kws varchar(90), kvs varchar(90) ) ";
   stmt.execute(sql);
}
sql = "insert into tx1 (kws, kvs) values ('xxx_"+conn.hashCode()+"', 'faf_"+conn.hashCode()+"') ";
stmt.execute(sql);
sql = " select kid as cnt, 'HSQLDB' as db from tx1 order by kid desc limit 1 ";
rs = stmt.executeQuery(sql);
if (rs.next()) inf = new StringBuilder(32).append(rs.getString(1)).append("@").append(rs.getString(2)).toString();
rs.close();
stmt.close();
conn.commit();
conn.setAutoCommit(true);
conn.close();
out.println("HSQLDB:"+inf);

out.println("<hr/>uri="+request.getRequestURI()+"<br />url="+request.getRequestURL());
javax.naming.InitialContext ctx = new javax.naming.InitialContext();
javax.sql.DataSource ds = (javax.sql.DataSource)ctx.lookup("java:comp/env/jdbc/ds_h2db");
java.sql.Connection conn = ds.getConnection();
String inf = conn.getMetaData().getDatabaseProductName();
java.sql.Statement stmt = conn.createStatement();
String sql = "create table if not exists sysUser (userId integer primary key auto_increment, users varchar(50), passw varchar(50), birth integer, email varchar(50), mobile varchar(50), phone varchar(50)) ";
stmt.execute(sql);
sql = "insert into sysUser (users, passw, birth, email, mobile, phone) values ('user-#', 'pass_#', 1990222, 'email-#', 'mobile-#', 'phone-#') ";
stmt.execute(sql.replaceAll("#", ""+sql.hashCode())); //request.getRequestedSessionId())
sql = "create table if not exists sysUser (uid integer primary key auto_increment, usr varchar(50), pwd varchar(50) ) "; 
stmt.execute(sql);
sql = " select userId from sysUser order by userId desc limit 1";
java.sql.ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) inf = new StringBuilder().append(rs.getInt(1)).toString();
rs.close();
stmt.close();
conn.close();
out.println("<hr/>### h2db max = "+inf);

out.println("### uri="+request.getRequestURI()+"<br />url="+request.getRequestURL()+"<hr/>");
javax.naming.InitialContext ctx = new javax.naming.InitialContext();
javax.sql.DataSource ds = (javax.sql.DataSource)ctx.lookup("java:comp/env/jdbc/ds_mysql");
java.sql.Connection conn = ds.getConnection();
String inf = conn.getMetaData().getDatabaseProductName();
java.sql.Statement stmt = conn.createStatement();
String sql = "create table if not exists myUser (userId integer primary key auto_increment, users varchar(50), passw varchar(50), birth integer, email varchar(50), mobile varchar(50), phone varchar(50)) ";
stmt.execute(sql);
sql = "insert into myUser (users, passw, birth, email, mobile, phone) values ('user-#', 'pass_#', 1990222, 'email-#', 'mobile-#', 'phone-#') ";
stmt.execute(sql.replaceAll("#", request.getRequestedSessionId()));
sql = " select userId from myUser order by userId desc limit 1";
java.sql.ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) inf = new StringBuilder().append(rs.getInt(1)).toString();
rs.close();
stmt.close();
conn.close();
out.println("### mysql max = "+inf+"<br />");




http://www.zuidaima.com/share/2188755504335872.htm
http://www.wubiaoblog.com/archives/1425
下载地址：版本：probe-2.2.3.zip
https://code.google.com/p/psi-probe/downloads/list
https://oss.sonatype.org/content/repositories/snapshots/com/github/psi-probe/psi-probe-web/3.0.0-SNAPSHOT/
https://oss.sonatype.org/content/repositories/snapshots/com/github/psi-probe/psi-probe-web/3.0.0-SNAPSHOT/psi-probe-web-3.0.0-20160206.024220-1.war


https://bitbucket.org/xerial/sqlite-jdbc/downloads download SQLite3 jdbc 
http://my.oschina.net/yaolifei/blog/146898 Dao层系列-5-Hibernate JPA
http://blog.csdn.net/feng88724/article/details/7164983 Tomcat Realm
导入java.sql包 
一、加载要连接数据库的驱动程序 
//Jdbc-Odbc桥 和 Microsoft Access 数据库 
Class.forName("sun.jdbc.odbc.JdbcOdbcDriver"); 
// SQL Server 驱动程序: 
Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver"); 
注：Class.forName()方法将给定的类加载到JVM，如果系统中不存在给定的类，则会引发异常
二、通过驱动程序管理器得到连接实例 
Connection conn=null; 
//1. 
//1.1建立数据源 
conn=DriverManager.getConnection("jdbc:odbc:MyDataSource"); //MyDataSource是数据源名称 
//1-2、不建立数据源 
conn=DriverManager.getConnection("jdbc:odbc:;Driver=Microsoft Access Driver (*.mdb);DBQ=C:\\VBTest.mdb"); 
//2.SQL Server 
conn=DriverManager.getConnection("jdbc:microsoft:sqlserver://127.0.0.1:1433;databasename=mydb","sa",""); 
注：DriverManager类跟踪已注册的驱动程序，通过getConnection(URL)方法, 找到一个能够连接至URL中指定的数据库驱动程序 
它接收三个参数, 分别表示1 数据源的名称、类型 2 用户名（可选） 3 密码（可选） 
三、基于连接对象建立处理器对象 
Statement stmt=conn.createStatement(); 
四、准备sql命令 
String sql="select * from Student"; 
五、执行命令返回结果集 
ResultSet rs=stmt.executeQuery(sql); 
六、显示结果集 
while(rs.next())//只要后面有记录 
{ 
//对当前行的所有字段遍历 
for(int i=1;i<=rs.getMetaData().getColumnCount();i++) 
{ 
System.out.print(rs.getMetaData().getColumnName(i)+": ");//显示字段名 
System.out.println(rs.getString(i));//显示字段当前值 
} 
System.out.println(); 
} 
七、关闭资源 
rs.close(); //关闭记录集 
stmt.close(); //关闭处理器对象 
conn.close(); //关闭连接对象 
预处理器的应用： 
//3.基于连接对象建立预处理器对象 
PreparedStatement pstmt=conn.prepareStatement("insert into student values(?,?,?,?)"); 
//4.给预处理对象的参数赋值 
pstmt.setString(1,"8888"); 
pstmt.setString(2,"nemo"); 
pstmt.setString(3,"accp"); 
pstmt.setString(4,"sanxianglu"); 
//5.执行预处理命令 
int i=pstmt.executeUpdate(); 
System.out.println(i+"条记录已成功插入！");
@Before  
public void setUp() {  
    String createTableSql = "create memory table test" +  
    "(id int GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY, " +  
    "name varchar(100))";  
    jdbcTemplate.update(createTableSql);  
         
    String createHsqldbFunctionSql =  
      "CREATE FUNCTION FUNCTION_TEST(str CHAR(100)) " +  
      "returns INT begin atomic return length(str);end";  
    jdbcTemplate.update(createHsqldbFunctionSql);  
    String createHsqldbProcedureSql =  
      "CREATE PROCEDURE PROCEDURE_TEST" +  
      "(INOUT inOutName VARCHAR(100), OUT outId INT) " +  
      "MODIFIES SQL DATA " +  
      "BEGIN ATOMIC " +  
      "  insert into test(name) values (inOutName); " +  
      "  SET outId = IDENTITY(); " +  
      "  SET inOutName = 'Hello,' + inOutName; " +  
    "END";  
    jdbcTemplate.execute(createHsqldbProcedureSql);  
}  



//javax.naming.Context initContext = new javax.naming.InitialContext();
//Context ctx = (Context)initContext.lookup("java:/comp/env");
//DataSource ds = (DataSource)ctx.lookup("jdbc/mysql");
String inf = "{X}";
String sql = " select count(1) as cnt from information_schema.tables where table_name=upper('tx1') ";
//javax.sql.DataSource ds = (javax.sql.DataSource)(new 

javax.naming.InitialContext().lookup("java:/comp/env/jdbc/ds_sqlite"));
javax.naming.Context ctx = new javax.naming.InitialContext();
javax.sql.DataSource ds = (javax.sql.DataSource)ctx.lookup("java:/comp/env/jdbc/ds_hsql");
java.sql.Connection conn = ds.getConnection();
conn.setAutoCommit(false);
java.sql.Statement stmt = conn.createStatement();
java.sql.ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) inf = rs.getString(1);
rs.close();
if (inf.equals("0")) {
   sql = " create table tx1 (kid integer not null primary key identity, kws varchar(90), kvs varchar(90) ) ";
   stmt.execute(sql);
}
sql = "insert into tx1 (kws, kvs) values ('xxx_"+conn.hashCode()+"', 'faf_"+conn.hashCode()+"') ";
stmt.execute(sql);
sql = " select kid as cnt, 'HSQLDB' as db from tx1 order by kid desc limit 1 ";
rs = stmt.executeQuery(sql);
if (rs.next()) inf = new 

StringBuilder(32).append(rs.getString(1)).append("@").append(rs.getString(2)).toString();
rs.close();
stmt.close();
conn.commit();
conn.setAutoCommit(true);
conn.close();
out.println("HSQLDB:"+inf);


out.println("<hr/>uri="+request.getRequestURI()+"<br />url="+request.getRequestURL());
javax.naming.InitialContext ctx = new javax.naming.InitialContext();
javax.sql.DataSource ds = (javax.sql.DataSource)ctx.lookup("java:comp/env/jdbc/ds_h2db");
java.sql.Connection conn = ds.getConnection();
String inf = conn.getMetaData().getDatabaseProductName();
java.sql.Statement stmt = conn.createStatement();
String sql = "create table if not exists sysUser (userId integer primary key auto_increment, users varchar(50), 

passw varchar(50), birth integer, email varchar(50), mobile varchar(50), phone varchar(50)) ";
stmt.execute(sql);
sql = "insert into sysUser (users, passw, birth, email, mobile, phone) values ('user-#', 'pass_#', 1990222, 

'email-#', 'mobile-#', 'phone-#') ";
stmt.execute(sql.replaceAll("#", ""+sql.hashCode())); //request.getRequestedSessionId())
sql = "create table if not exists sysUser (uid integer primary key auto_increment, usr varchar(50), pwd 

varchar(50) ) "; 
stmt.execute(sql);
sql = " select userId from sysUser order by userId desc limit 1";
java.sql.ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) inf = new StringBuilder().append(rs.getInt(1)).toString();
rs.close();
stmt.close();
conn.close();
out.println("<hr/>### h2db max = "+inf);

out.println("### uri="+request.getRequestURI()+"<br />url="+request.getRequestURL()+"<hr/>");
javax.naming.InitialContext ctx = new javax.naming.InitialContext();
javax.sql.DataSource ds = (javax.sql.DataSource)ctx.lookup("java:comp/env/jdbc/ds_mysql");
java.sql.Connection conn = ds.getConnection();
String inf = conn.getMetaData().getDatabaseProductName();
java.sql.Statement stmt = conn.createStatement();
String sql = "create table if not exists myUser (userId integer primary key auto_increment, users varchar(50), 

passw varchar(50), birth integer, email varchar(50), mobile varchar(50), phone varchar(50)) ";
stmt.execute(sql);
sql = "insert into myUser (users, passw, birth, email, mobile, phone) values ('user-#', 'pass_#', 1990222, 

'email-#', 'mobile-#', 'phone-#') ";
stmt.execute(sql.replaceAll("#", request.getRequestedSessionId()));
sql = " select userId from myUser order by userId desc limit 1";
java.sql.ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) inf = new StringBuilder().append(rs.getInt(1)).toString();
rs.close();
stmt.close();
conn.close();
out.println("### mysql max = "+inf+"<br />");



### java Tomcat JDNI DataSource Sample ###   
  <Resource name="jdbc/ds_mysql" 
       auth="Container" 
       type="javax.sql.DataSource" 
       driverClassName="com.mysql.jdbc.Driver" 
       url="jdbc:mysql://localhost:3306/tests?useUnicode=true&amp;characterEncoding=UTF-8" 
       username="tests" 
       password="tests" 
       maxActive="30" 
       maxIdle="2" 
       maxWait="12000" 
       removeAbandoned="true" 
       removeAbandonedTimeout="60" 
       testOnBorrow="true" 
       validationQuery="select 1 " 
       logAbandoned="true" 
    />

   <Resource name="jdbc/ds_mysql2"
       auth="Container" 
       type="javax.sql.DataSource" 
       factory="com.alibaba.druid.pool.DruidDataSourceFactory" 
       url="jdbc:mysql://localhost:3306/tests?useUnicode=true&amp;characterEncoding=UTF-8" 
       username="tests" 
       password="tests" 
       maxActive="30" 
       maxIdle="2" 
       maxWait="12000" 
       removeAbandoned="true" 
       removeAbandonedTimeout="60" 
       validationQuery="select 1 " 
       testOnBorrow="true" 
       logAbandoned="true" 
     /> 


@Service("testJdbcService")
public class TestJdbcServiceImpl implements TestJdbcService {
	
	@Resource(name="jdbcTemplate")
	private JdbcTemplate jdbcTemplate;

	public void insertTest1() {
		String sql = "create table if not exists sysUser (userId integer primary key auto_increment, 

users varchar(50), passw varchar(50), birth integer, email varchar(50), mobile varchar(50), phone varchar(50)) 

";
		jdbcTemplate.execute(sql);
		long rand = Math.round(Math.random()*1000l)+1000l;
		sql = "insert into sysUser (users, passw, email, mobile, phone) values (?, ?, ?, ?, ?)";
		jdbcTemplate.update(sql, "liujy"+rand,"passw"+rand,"email"+rand,"mobile"+rand,"phone"+rand); 
		jdbcTemplate.update(sql, "liujy01","passw"+rand,"email"+rand,"mobile"+rand,"phone"+rand);
	}

	public void updateTest1() {
		long rand = Math.round(Math.random()*1000l)+1000l;
		String sql = "update sysUser set passw=?, email=?, mobile=?, phone=? where users=? ";
		jdbcTemplate.update(sql, "passw"+rand,"email"+rand,"mobile"+rand,"phone"+rand, "liujy01");
	}

	public void selectTest1() {
		StringBuilder inf = new StringBuilder(20480);
		String sql = "select * from sysUser where users=? order by 1 desc limit 5 ";
		jdbcTemplate.query(sql, new MyResultSetExtractor(inf), "liujy01");
		System.err.println("### (111) MyResultSetExtractor inf=\n"+inf); inf.delete(0, inf.length());
		jdbcTemplate.query(sql, new MyResultSetExtractor(inf), "liujy012");
		System.err.println("### (222) MyResultSetExtractor inf=\n"+inf); inf.delete(0, inf.length());
		jdbcTemplate.query(sql, new MyRowCallbackHandler(inf), "liujy012");
		System.err.println("### (333) MyRowCallbackHandler inf=\n"+inf); inf.delete(0, inf.length());
		jdbcTemplate.query(sql, new MyRowMapper(inf), "liujy012");
		System.err.println("### (444) MyRowMapper inf=\n"+inf); inf.delete(0, inf.length());

		MyRowMapper2 aa = new MyRowMapper2(inf);
		jdbcTemplate.query(sql, aa, "liujy01");
		System.err.println("### (555) MyRowMapper2 inf=\n"+inf); inf.delete(0, inf.length());
		System.err.println("### (555) list=\n"+aa.getList());
		
		//jdbcTemplate.query()
	}
	
	
	private class MyRowMapper2 implements RowMapper<Object> {
		private StringBuilder inf = null;
		public MyRowMapper2(StringBuilder inf) {
			this.inf = inf;
		}

		private java.util.List<Object> list = new java.util.ArrayList<Object>();
		public java.util.List<Object> getList() {
			return list;
		}
		
		@Override
		public Object mapRow(ResultSet rs, int idx) throws SQLException {
			ResultSetMetaData rmd = rs.getMetaData();
			int cnt = rmd.getColumnCount()+1; 
			inf.append("mapRow-").append(idx).append("\t");
			for (int i=1; i<cnt; i++) inf.append(rmd.getColumnLabel(i)).append("\t");
			inf.append("\n");
			for (int i=1; i<cnt; i++)
				

inf.append(rmd.getColumnLabel(i)).append("=").append(rs.getString(i)).append("\t");
			inf.append("\n");
			java.util.Map<String,Object> map = new java.util.HashMap<String,Object>();
			for (int i=1; i<cnt; i++) map.put(rmd.getColumnLabel(i), rs.getString(i));
			list.add(map);
			return map;
		} 
	}
	
	private class MyRowCallbackHandler implements RowCallbackHandler {
		private StringBuilder inf = null;
		public MyRowCallbackHandler(StringBuilder inf) {
			this.inf = inf;
		}
		@Override
		public void processRow(ResultSet rs) throws SQLException {
			ResultSetMetaData rmd = rs.getMetaData();
			int cnt = rmd.getColumnCount()+1; 
			inf.append("processRow~").append("\n");
			for (int i=1; i<cnt; i++) inf.append(rmd.getColumnLabel(i)).append("\t");
			inf.append("\n");
			for (int i=1; i<cnt; i++)
				

inf.append(rmd.getColumnLabel(i)).append("=").append(rs.getString(i)).append("\t");
			inf.append("\n");
		}
	}
	
	private class MyRowMapper implements RowMapper<Object> {
		private StringBuilder inf = null;
		public MyRowMapper(StringBuilder inf) {
			this.inf = inf;
		}
		@Override
		public Object mapRow(ResultSet rs, int idx) throws SQLException {
			ResultSetMetaData rmd = rs.getMetaData();
			int cnt = rmd.getColumnCount()+1; 
			inf.append("mapRow-").append(idx).append("\n");
			for (int i=1; i<cnt; i++) inf.append(rmd.getColumnLabel(i)).append("\t");
			inf.append("\n");
			for (int i=1; i<cnt; i++)
				

inf.append(rmd.getColumnLabel(i)).append("=").append(rs.getString(i)).append("\t");
			inf.append("\n");
			return null;
		} 
	}
	
	private class MyResultSetExtractor implements ResultSetExtractor<Object> {
		private StringBuilder inf = null;
		public MyResultSetExtractor(StringBuilder inf) {
			this.inf = inf;
		}
		
		@Override
		public java.lang.Object extractData(java.sql.ResultSet rs) 
				throws java.sql.SQLException {
			ResultSetMetaData rmd = rs.getMetaData();
			int cnt = rmd.getColumnCount()+1; 
			for (int i=1; i<cnt; i++) inf.append(rmd.getColumnLabel(i)).append("\n");
			inf.append("\n");
			while (rs.next()) {
				for (int i=1; i<cnt; i++)
				

inf.append(rmd.getColumnLabel(i)).append("=").append(rs.getString(i)).append("\t");
				inf.append("\n");
			} 
			return null;
		}
	}
	
}


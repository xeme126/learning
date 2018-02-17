



InitialContext ctx = new InitialContext();
DataSource dataSource = (DataSource)ctx.lookup("java:comp/env/jdbc/DSTest");

Context context = new InitialContext();
DataSource dataSource = (DataSource)context.lookup("java://comp/env/jdbc/mydb");
Connection conn = dataSource.getConnection();

    
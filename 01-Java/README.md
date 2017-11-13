Java开发


# rmd.getColumnLabel rs.getString 索引从一开始
cnt = rmd.getColumnCount()+1;
while (rs.next()) {
	for (int i=1; i<cnt; i++)
		LOG.debug("{}[{}]={}\t", rmd.getColumnLabel(i), rmd.getColumnName(i), rs.getString(i));
}
rs.close();

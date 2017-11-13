LBS应用

假设有如下功能需求：
    显示我附近的人
    由近到远排序
    显示距离

几种方案：
    基于MySQL数据库
    采用GeoHash索引，基于MySQL
    MySQL空间存储（MySQL Spatial Extensions）
    使用MongoDB存储地理位置信息


方案1：基于MySQL数据库
SELECT id, ( 6371 * acos( cos( radians(37) ) * cos( radians( lat ) ) * cos( radians
( lng ) - radians(-122) ) + sin( radians(37) ) * sin( radians( lat ) ) ) ) AS distance
 FROM places HAVING distance &lt; 25 ORDER BY distance LIMIT 0 , 100;

注：这条SQL查询的是在lat,lng这个坐标附近的目标，并且按距离正序排列，SQL中的distance单位为公里。
但使用SQL语句进行查询的缺点也显而易见，每条SQL的计算量都会非常大，性能将会是严重的问题。
先别放弃，我们尝试对这条SQL做一些优化。 http://www.putaor.com/?p=586
可以将圆形区域抽象为正方形，SQL语句可以简化如下：
SELECT * FROM places WHERE ((lat BETWEEN ? AND ?) AND (lng BETWEEN ? AND ?))




# postgis_LayerTransform
gis开发者常常因为要叠加百度，高德，谷歌等等在线或离线的web底图，由于中国特殊国情，这些底图都是加了各自的偏移量，导致自身的矢量数据与底图
叠加常常发生或多或少的偏移不齐的样子。  
通过该sql脚本在postgis中对gis矢量数据进行偏移增加或纠正。当前支持主流几种坐标的加偏或纠偏，（并非严格精准，只是让数据叠加非常整齐的视觉效果），如百度与84转换，高德，谷歌，esri的火星坐标系与84等。
# 安装：
  在postgresql-postgis空间数据库中，执行sql文件中语句即可。
# 使用：
select LayerTransform(
	in inputlayer text,--输入图层名字
	in transformtype transform_type--转换类型枚举型。
)   
如在psql中输入: select LayerTransform('road','GCJ2WGS'); 回车执行该语句即可，等待完成。该示例代码是将 road表从火星坐标系转往84坐标系。
## 参数说明：
  inputlayer：输入的表名称，是个要加/纠偏的table名称，table是个空间表。  
  transformtype：加/纠偏方式，支持以下6种'BD2GCJ', 'GCJ2BD', 'WGS2GCJ','GCJ2WGS','BD2WGS','WGS2BD'，分别代表 百度转谷歌高德，谷歌高德转百度，84转火星，火星转84，百度转84,84转百度。
## 效果图
  gcs坐标，转换前与osm叠加  
  ![转换前](http://img.blog.csdn.net/20151203104302079)  
  ![转换中](http://img.blog.csdn.net/20151203104420291)   
  ![转换后](http://img.blog.csdn.net/20151203104452730)

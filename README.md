<h1>第一步 - 在elk host主机上修改虚拟内存。<h1>
运行命令：nano /etc/sysctl.conf 
添加配置：vm.max_map_count=262144，保存退出
官方说明：https://www.elastic.co/guide/en/elasticsearch/reference/5.2/vm-max-map-count.html

<h1>第二步 - 克隆当前代码到docker主机。<h1>
运行命令：git clone https://github.com/lean-soft/elk.git

<h1>第三步 - 通过Compose命令运行elk以及对应组建。<h1>
运行命令：cd elk，进入代码根目录。
运行命令：compose up -d，运行所有elk组件

<h1>第四步 - 打开kibana查看是否运行成功。<h1>
打开浏览器,输入http://ip:5601

<h1>第五步 - 配置logstash索引<h1>
1.点击Manaement -> Index Patterns -> Add New
2.输入logstash-*
3.Time-field name选择@timestamp
4.点击create

<h1>第六步 - 配置dockbeat索引<h1>
1.点击Manaement -> Index Patterns -> Add New
2.输入dockbeat-*
3.Time-field name选择@timestamp
4.点击create

<h1>第七步 - 查看数据<h1>
点击Discover查看数据

<h1>第八步 - 将logstash以及dockbeat部署到更多的docker主机上<h1>
1. 运行logspout收集container日志
docker run -d --name="logspout" --volume=/var/run/docker.sock:/var/run/docker.sock harbor-bj.devopshub.cn/elastic/logspout:latest syslog://ip:5000
2. 运行dockbeat收集服务器性能数据
docker run -d --hostname [DockerHostName]--name dockerbeat --volume=$PWD/dockerfiles/dockbeat/dockbeat.yml:/etc/dockbeat/dockbeat.yml --volume=/var/run/docker.sock:/var/run/docker.sock harbor-bj.devopshub.cn/elastic/dockbeat:latest

<h1>第九步 - 通过kibana查看其他数据数据是否已经收集到<h1>

<h1>第十步 - 通过kikana配置图表<h1>

<h1>第十一步 - 配置仪表盘<h1>



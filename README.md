<h3>第一步 - 在elk host主机上修改虚拟内存。</h3>
运行命令：

    nano /etc/sysctl.conf 

添加配置：vm.max_map_count=262144，保存退出


<h3>第二步 - 克隆当前代码到docker主机。</h3>
运行命令：

    git clone https://github.com/lean-soft/elk.git

<h3>第三步 - 通过Compose命令运行elk以及对应组建。</h3>
进入代码根目录

    cd elk

运行ELK所有组建：

    compose up -d

<h3>第四步 - 打开kibana查看是否运行成功。</h3>
打开浏览器,输入http://ip:5601

<h3>第五步 - 配置logstash索引</h3>

 1. 点击Manaement -> Index Patterns -> Add New 
 2. 输入logstash-* 
 3. Time-field name选择 @timestamp 
 4. 点击create

<h3>第六步 - 配置dockbeat索引</h3>

 1. 点击Manaement -> Index Patterns -> Add New 
 2. 输入dockbeat-* 
 3. Time-field name选择@timestamp 
 4. 点击create

<h3>第七步 - 查看数据</h3>
点击Discover查看数据

<h3>第八步 - 将logstash以及dockbeat部署到更多的docker主机上</h3>
运行logspout收集container日志

    docker run -d --name="logspout"
    --volume=/var/run/docker.sock:/var/run/docker.sock harbor-bj.devopshub.cn/elastic/logspout:latest syslog://ip:5000

运行dockbeat收集服务器性能数据

    docker run -d --hostname [DockerHostName]--name dockerbeat --volume=$PWD/dockerfiles/dockbeat/dockbeat.yml:/etc/dockbeat/dockbeat.yml --volume=/var/run/docker.sock:/var/run/docker.sock harbor-bj.devopshub.cn/elastic/dockbeat:latest

<h3>第九步 - 通过kibana查看其他数据数据是否已经收集到</h3>

<h3>第十步 - 通过kikana配置图表</h3>

<h3>第十一步 - 配置仪表盘</h3>





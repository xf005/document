### 防火墙配置位置：
/etc/firewalld/zones/public.xml

### 内容如下：
```
<?xml version="1.0" encoding="utf-8"?>
<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <port protocol="tcp" port="80"/>
  <port protocol="tcp" port="8080"/>
  <port protocol="tcp" port="8090"/>
  <rule family="ipv4">
    <source address="10.100.119.145/32"/>
    <port protocol="tcp" port="22"/>
    <accept/>
  </rule>
  <rule family="ipv4">
    <source address="10.100.119.231/32"/>
    <port protocol="tcp" port="22"/>
    <accept/>
  </rule>
  <rule family="ipv4">
    <source address="10.0.101.186/32"/>
    <port protocol="tcp" port="22"/>
    <accept/>
  </rule>
  <rule family="ipv4">
    <source address="10.200.87.15/32"/>
    <port protocol="tcp" port="9100"/>
    <accept/>
  </rule>
</zone>
```

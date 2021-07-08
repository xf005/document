# document
应用场景：我们有台WINDOWS服务器为于法国巴黎(op)，国内直接连接卡顿的很严重，PING值差不多是350MS，为了加速访问这台远程桌面我们想到了使用端口转发来加速。
原理：我们用于转发加速的机器位于美国圣何塞（VIRMACH），我这里到圣何塞PING值150MS，圣何塞到法国巴黎PING值50MS，所以我们用圣何塞进行端口转发，全程PING值也就在200MS，PING减少了150MS，同理RDP协议也一起得到了加速。

方法：

首先：登录我们用于转发的机器，在这里案例中就是圣何塞的机器，查看firewall防火墙是否开启。

firewall-cmd --state
第二：开启防火墙伪装，开启后才能转发端口：

firewall-cmd --add-masquerade --permanent
第三：添加转发规则：

firewall-cmd --add-forward-port=port=3389:proto=tcp:toport=3389:toaddr=我的法国巴黎WIN主机IP --permanent
第四：重载防火墙配置，让它生效

firewall-cmd --reload
到这里就完成了，可以直接在远程桌面登录mstsc上输入圣何塞的机器IP，打开连接，登录，看看是不是能登录进去法国巴黎的机器了

查看反代端口转发情况：

firewall-cmd --list-all
 

如果需要移除端口转发：

使用以下命令：

firewall-cmd --remove-forward-port=port=3389:proto=tcp:toport=3389:toaddr=我的法国巴黎WIN主机IP --permanent
firewall-cmd --remove-masquerade --permanent
firewall-cmd --reload
备注：本人已经验证过了可行。

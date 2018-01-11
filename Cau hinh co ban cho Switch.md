# Switching - Chuyển mạch

## 1.Cấu hình cơ bản chung cho một Switch

Reset tất cả cấu hình của Switch và reload lại.


Switch#delete flash:vlan.dat
Switch#erase startup-config
Switch#reload


## 2.Cấu hình về Security và management



Switch(config)#hostname tên switch
Switch(config)#line console 0
Switch(config-line)#password mật khẩu
Switch(config-line)#login

Switch(config)#line vty 0 4
Switch(config-line)#pass mật khẩu
Switch(config-line)#login

## 3.Thiết lập địa chỉ IP và default gateway cho Switch

Switch(config)#interface vlan1
Switch(config-int)#ip address địa chỉ subnetmask
Switch(config)#ip default-gateway địa chỉ

## 4.Thiết lập tốc độ và duplex của cổng

Switch(config-int)#speed tốc độ
Switch(config-int)#duplex full

## 5.Thiết lập dịch vụ HTTP và cổng

Switch(config)#ip http server
Switch(config)#ip http port 80

## 6.Thiết lập, quản lý địa chỉ MAC

Switch(config)#mac-address-table static địa chỉ MAC interface fastethernet số vlan
Switch#show mac-address-table
Switch#clear mac-address-table

## 7.Cấu hình bảo mật cho cổng

Switch(config-if)#switchport mode acess
Switch(config-if)#switchport port-security

**Cấu hình Static:** Switch(config-if)#switchport port-security mac-address địa chỉ Mac

**Cấu hình Sticky:** Switch(config-if)#switchport port-security mac-address sticky (thông dụng nhất)

Switch(config-if)#switchport port-security maximum value
Switch(config-if)#switchport port-security violation shutdown

## 8.Tạo Vlan

#### Cách 1.

Switch#vlan database
Switch(vlan)#vlan number

#### Cách 2. Khi gán các cổng vào vlan, dù vlan chưa tồn tại nhưng Switch vẫn tự tạo.

Switch(config)#interface fastethernet 0/0
Switch(config-int)#switchport access vlan vlan-id

Muốn xoá vlan ta làm như sau:

Switch(config-if)#no switchport access vlan vlan-id
Switch#clear vlan vlan_number (xoá toàn bộ vlan )

## 9.Gán nhiều cổng vào trong vlan cùng một lúc, cấu hình Range

Đối với dãy cổng không liên tục.
Switch(config)#interface range cổng 1 , cổng 2 , cổng 3

Đối với một dãy liên tục.
Switch(config)#interface range cổng 1-n
Switch(config-range)#switchport access vlan vlan-id


#### Ví dụ:
Switch(config)#interface range f0/0 , f0/2 , f0/4
Switch(config)#interface range f0/0-10
Switch(config-range)#switchport access vlan 10

10.Cấu hình Trunk

Switch(config-if)#switchport mode trunk
Switch(config-if)#switchpor trunk encapsulation encapsulation-type
Switch#show trunk

## 11.Cấu hình VTP

Switch#vlan database
Switch(vlan)#vtp v2-mode
Switch(vlan)#vtp domain tên domain
Switch(vlan)#vtp {server/client/transperant}
Switch(vlan)#vtp password password (Tạo pass cho domain)
Switch#show vtp status

## 12.Cấu hình Inter-Vlan trên Router

Router(config)#interface fastethernet 0/0.1
Router(config-subif)#encapsulation type
Router(config-subif)#ip address địa chỉ subnetmask



## Link bài lab

https://protechgurus.com/configure-syslog-server-cisco-packet-tracer/
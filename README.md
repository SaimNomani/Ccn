# Ccn
‎DHCP:
‎- [DHCP-Server] interface GigabitEthernet 0/0/0
- ‎[DHCP-Server-GigabitEthernet0/0/0] ip address 192.168.1.1 24  # Set gateway IP
‎- [DHCP-Server-GigabitEthernet0/0/0] dhcp select global          # Enable DHCP on the interface
- ‎[DHCP-Server-GigabitEthernet0/0/0] quit
- ‎[DHCP-Server] ip pool LAN-POOL  # Create DHCP pool named "LAN-POOL"
- ‎[DHCP-Server-ip-pool-LAN-POOL] network 192.168.1.0 mask 255.255.255.0  # Subnet to assign IPs from
‎- [DHCP-Server-ip-pool-LAN-POOL] gateway-list 192.168.1.1                # Default gateway
- [DHCP-Server-ip-pool-LAN-POOL] dns-list 8.8.8.8 4.4.4.4                # DNS servers
‎- [DHCP-Server-ip-pool-LAN-POOL] lease day 1 hour 0 minute 0             # Lease time (1 day)
- ‎[DHCP-Server-ip-pool-LAN-POOL] quit
- ‎[DHCP-Server] display ip pool name LAN-POOL
‎
‎- [5/22, 10:29 AM] Ahmed Ali Khan: FTP
‎- [5/22, 10:30 AM] Ahmed Ali Khan: <Huawei> system-view
‎- [Huawei] sysname FTP-Server
- ‎[FTP-Server] ftp server enable  # Start FTP service
- ‎[FTP-Server] set default ftp-directory flash:  # Set storage directory (default is router's flash)
‎
‎
‎- [FTP-Server] aaa  # Enter AAA view
- ‎[FTP-Server-aaa] local-user ftpuser password cipher Huawei@123  # Create user 'ftpuser'
- ‎[FTP-Server-aaa] local-user ftpuser service-type ftp  # Assign FTP access
- ‎[FTP-Server-aaa] local-user ftpuser ftp-directory flash:  # Restrict to flash directory
‎- [FTP-Server-aaa] local-user ftpuser privilege level 15  # Full permissions (read/write/delete)
- ‎[FTP-Server-aaa] quit
‎- [5/22, 10:33 AM] Ahmed Ali Khan: <Huawei> system-view
- ‎[Huawei] sysname Telnet-Server  # Rename router (optional)
‎- [Telnet-Server] telnet server enable  # Enable Telnet service
‎
- ‎[Telnet-Server] aaa  # Enter AAA configuration mode
- ‎[Telnet-Server-aaa] local-user admin password cipher Huawei@123  # Create user 'admin'
‎- [Telnet-Server-aaa] local-user admin service-type telnet  # Assign Telnet access
- ‎[Telnet-Server-aaa] local-user admin privilege level 15  # Highest privileges (read/write)
- ‎[Telnet-Server-aaa] quit
‎
‎- [Telnet-Server] user-interface vty 0 4  # Configure virtual terminal lines (0 to 4)
‎- [Telnet-Server-ui-vty0-4] authentication-mode aaa  # Use AAA for login
- ‎[Telnet-Server-ui-vty0-4] protocol inbound telnet  # Allow Telnet only
‎- [Telnet-Server-ui-vty0-4] idle-timeout 15  # Set timeout to 15 minutes (optional)
‎- [Telnet-Server-ui-vty0-4] quit
‎
- ‎<Telnet-Client> telnet 192.168.1.1
‎- Username: admin
- ‎Password: Huawei@123  # Authenticate
‎<Telnet-Server>  # Successfully logged in!
- ‎[5/22, 10:34 AM] Ahmed Ali Khan: Telnet
  - Lacp
‎- Interface eth trunk 1
‎ - Port link-type trunk
‎ - Mode lacp-static
‎ - Max active-linknumber 2
‎

# SYN-FLOOD

## Executing attacker_code

First, while connected to a network, run this command:

```
sudo apt install hping3
```


In attacker_code, the format of the hping3 command is:

```
sudo hping3 -S <source-ip> -a <destination-ip> -p 80 --flood
```

The default values for source-ip and destination ip are 192.168.56.103 and 192.168.56.101 respectively. These values need to be altered depending on the ip address of the client device and the ip address of the server device. The client device is the source-ip, and the server device is the defending side. 

## Executing defender_code

If the defending device does not have iptables installed, run the command:

```
sudo apt install iptables
```

There are two defender codes, defender_code_1 and defender_code_2. defender_code_1 is the defense that drops packets from a specific ip address, which may need to be altered depending on what the ip address of the attacker is. 

In defender_code_1, the variable line here is line 2, which has the format:
```
sudo iptables -A -INPUT -s <attacker-ip> -j DROP
```

The default value for attacker-ip is 192.168.56.103. This value needs to be altered to the attacking device IP. 

defender_code_2 is the heuristic defense against syn-flood packets, and does not need any altering. 

For both defense codes, the command 
```
sudo iptables -L -v
```

is run both before and after the defenses are implemented. This command shows the rules that are implemented at the current time. The first ruleset are the rules active before rule implementation, and the second ruleset are the rules active after rule implementation. After the file is run, the second ruleset is the one currently active. 

To clear the ruleset, run the file clear_iptables. This will set the ruleset back to the default rule implementation. 

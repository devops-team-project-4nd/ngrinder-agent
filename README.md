# ngrinder-agent

### agent-controller 연결 방법
1. port fowarding

2. agnet.conf content update
```conf
common.start_mode=agent
#start.mode=agent
#agent.console.ip=192.168.0.25
# If you want to monitor bind to the different local ip not automatically selected ip. Specify below field.
#monitor.binding_ip=hostname_or_ip
##monitor.binding_port=13243
#agent.controller_host=http://192.168.0.25/
agent.controller_host=192.168.0.25
agent.controller_port=16001
#agent.console.port=8080
#monitor.binding_ip=192.168.0.25
#monitor.binding_port=8080
agent.subregion=
agent.owner=admin
#agent.host_id=
#agent.server_mode=true
```
꼭, 16001의 포트번호를 줄 것. 8080은 UI 접속 포트이기 때문이다.

### error 문제 해결
1. agent-controller connect error
```sh
2024-02-28 15:30:56,861 INFO  starter: connecting to controller 192.168.0.25:8080
2024-02-28 15:30:56,927 INFO  agent controller daemon: The agent controller daemon is started.
2024-02-28 15:30:57,030 INFO  agent controller: Connected to agent controller server at /192.168.0.25:8080
2024-02-28 15:30:57,031 INFO  agent controller: Waiting for agent controller server signal
2024-02-28 15:30:57,090 INFO  agent controller: agent controller communication is shutdown
2024-02-28 15:30:57,096 ERROR agent controller: Exception whilst sending message. This error is not critical if it doesn't occur much.
```
agent는 controller에서 작업을 할 때 8080 port가 아니라 16000포트로 접속해야 한다. <br>
따라서, agent.controller_port=16001로 변경하여 문제를 해결했다.

2. agent-port connect error
```sh
2024-02-28 17:18:37,353 ERROR agent daemon: Failed to connect to '/192.168.0.25:12003'
2024-02-28 17:18:37,354 INFO  agent daemon: Test shuts down.
```
ip주소는 연결이 가능 하나 포트 번호 연결의 문제가 생긴 상태. <br>
network.ps1 파일에 12003 포트 번호를 추가해줌으로써 문제를 해결했다.

3. 
